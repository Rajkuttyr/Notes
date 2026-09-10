---
title: JARVIS Prototype — How It Works and How to Test It
tags:
  - jarvis
  - spring-boot
  - ollama
  - testing
status: Prototype guide
---

# JARVIS Prototype — Simple Testing Guide

## The simple idea

JARVIS has two different jobs:

1. **Chat** — answer a normal question using the local Ollama AI model.
2. **Plan an action safely** — inspect a requested task, decide which tools may be needed, calculate risk, and ask for approval before an external action.

At this stage, JARVIS **does not call a real calendar or weather service**. That is intentional. It can create and review a safe plan, but it cannot accidentally create an event in a real calendar.

```text
You
 ↓
Spring Boot API
 ├─ normal question → Ollama → response
 └─ action request → tool selection → risk check → plan / approval request
```

## What is already working?

| Part | What it does now |
|---|---|
| Ollama chat | Sends a message to the local `qwen3:4b` model |
| Tool registry | Knows about `weather.forecast`, `calendar.read`, and `calendar.create` |
| Risk engine | Rates planned tool actions from 0 to 100 |
| Authorization gate | Requires confirmation before a calendar write |
| Audit logger | Records planning and authorization events in memory |
| Task store | Keeps each task while the Spring Boot app is running |

## Before testing

Open two terminals.

### Terminal 1 — make sure Ollama is available

```bash
ollama list
```

You should see `qwen3:4b`. If it is missing:

```bash
ollama pull qwen3:4b
```

Usually the Ollama application runs the local service automatically. If it is not running, start it:

```bash
ollama serve
```

### Terminal 2 — start JARVIS

```bash
cd /Users/rajkutty/Downloads/jarvis
./mvnw spring-boot:run
```

Wait until you see:

```text
Tomcat started on port 8080
```

JARVIS is then available at:

```text
http://localhost:8080
```

## Which API should I call first?

Start with **task planning**, not chat. It is fast, does not depend on the AI model generating an answer, and shows the important JARVIS safety flow.

### Step 1 — create a safe task plan

```bash
curl -X POST http://localhost:8080/api/jarvis/tasks \
  -H 'Content-Type: application/json' \
  -d '{"message":"Check tomorrow weather and schedule a run"}'
```

Expected important fields:

```json
{
  "status": "PENDING_AUTHORIZATION",
  "executionGraph": ["weather.forecast", "calendar.create"],
  "risk": {
    "score": 45,
    "decision": "CONFIRM"
  }
}
```

Copy the returned `taskId`. It will be different every time.

### What happened inside JARVIS?

```text
Your message: "Check tomorrow weather and schedule a run"
        ↓
ToolRegistry finds matching tools:
weather.forecast + calendar.create
        ↓
RiskEngine sees calendar.create changes an external system
        ↓
Risk score = 45, decision = CONFIRM
        ↓
Task status = PENDING_AUTHORIZATION
        ↓
No external action is performed
```

The critical point is that the AI does **not** decide it is authorized. Normal Java code in `RiskEngine` and `OrchestrationService` makes that decision.

### Step 2 — inspect the saved task

Replace `<task-id>` with the value from Step 1:

```bash
curl http://localhost:8080/api/jarvis/tasks/<task-id>
```

This returns the plan again. The data is kept in memory, so it disappears if you restart JARVIS.

### Step 3 — explicitly authorize the planned write

```bash
curl -X POST http://localhost:8080/api/jarvis/tasks/<task-id>/authorize
```

Expected result:

```json
{
  "status": "AUTHORIZED",
  "nextStep": "Authorized. Connect a real MCP adapter before execution."
}
```

This is only a safety test. It does **not** create a real calendar event because an MCP calendar adapter has not been connected yet.

## Test the chat route

After task planning works, test the local AI:

```bash
curl -X POST http://localhost:8080/api/jarvis/chat \
  -H 'Content-Type: application/json' \
  -d '{"message":"Explain what you can do in one short sentence."}'
```

Expected shape:

```json
{
  "conversationId": "...",
  "answer": "..."
}
```

The first response can be slower because Ollama may need to load the model into memory.

## Test the risk rules

### Low-risk read-only task

```bash
curl -X POST http://localhost:8080/api/jarvis/tasks \
  -H 'Content-Type: application/json' \
  -d '{"message":"What is the weather forecast tomorrow?"}'
```

Expected: `PLANNED`, risk decision `AUTO`. The tool is read-only.

### External write needs confirmation

```bash
curl -X POST http://localhost:8080/api/jarvis/tasks \
  -H 'Content-Type: application/json' \
  -d '{"message":"Schedule a meeting tomorrow at 5 PM"}'
```

Expected: `PENDING_AUTHORIZATION`, decision `CONFIRM`.

### Sensitive request is blocked

```bash
curl -X POST http://localhost:8080/api/jarvis/tasks \
  -H 'Content-Type: application/json' \
  -d '{"message":"Schedule an appointment using my medical secret"}'
```

Expected: `BLOCKED`, decision `BLOCK`.

## Where each part lives in the code

```text
API request
  JarvisController
      ↓
Task request
  OrchestrationService
      ↓
Find possible tools
  ToolRegistry
      ↓
Calculate policy decision
  RiskEngine
      ↓
Save task and audit event
  in-memory TaskSnapshot + AuditLogger
```

| File | Why it matters |
|---|---|
| `api/JarvisController.java` | Receives HTTP requests |
| `agent/JarvisChatService.java` | Sends normal chat messages to Ollama |
| `tools/ToolRegistry.java` | Defines known tools and their metadata |
| `orchestration/RiskEngine.java` | Calculates risk and policy decision |
| `orchestration/OrchestrationService.java` | Builds and saves the task plan |
| `audit/AuditLogger.java` | Keeps a record of important task events |

## Current limitations — by design

- No real weather/calendar MCP server is configured.
- Task and audit data are lost when the app restarts.
- The development API currently permits all requests; add real Spring Security login and user ownership checks before deployment.
- Authorization records approval but cannot execute an external tool yet.

## The next development step

Connect a **read-only weather MCP tool first**. Then JARVIS can run this full safe flow:

```text
Plan weather lookup
 → execute weather tool
 → validate expected response fields
 → return verified result
```

After that, add calendar reading, then calendar creation with a postcondition check: after creating an event, read the calendar again and confirm the event ID and time exist.
