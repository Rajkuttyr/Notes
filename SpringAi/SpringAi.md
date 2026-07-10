What is AI
mmic how the human brain process the info to solve a problem 
moder AI recocgnises data 
ml - helps a machine to learn 
-foundation of Ai learn pattern from data and allowing them to make predictio 
-supervise system use labeled data
- un labelled like lassification 
- reinforcement - sysytem learn through reccursive interaction through the system
- use case - facial recognisation abnormality on ultrasound self drive fraud detection product recomendation
- Deep learning - subset of of ml 
- neural network mimc the structure of human brain
- adjust weights automatically extract the features and learn automatically
- LLM - large language model 
- neural etwork designed for understanding langugage 
- uses attention mechanism to weight the importance of wwords in contet 
- can process all at once and understand relationship between the words
- input ->tokenisne ->neural network{pattern recognisation}-> prediction
- rawlanguage-> break into peices-> find relationship ->generate nextword
- how llm learn. ->> massive datasets 
- fine tuning specialisation of llm -> task specific datasets human eedback training
- Generarive Ai 
- gnerarive pre-trained transformer
- transformers architectur how they process data pre trained on vast amount of data
- prompt engineering - used to effectively communicate with ai 
- used to teach a 
- ![[Pasted image 20260709065055.png]]
advanced technique s - zero shopt prompting will not contain examples or demo 
one shot - provide single examplw
few shot - multiple ex
chain of thought step by step
![[Pasted image 20260709065959.png]]

prompt engineering - lee boonstra
hhtps://www.promptingguide.ai
1.0.0
signing up api key - open ai 
stat.spring.ai
LLM pricing - 
chat client is interface 
builder is another interface used to create a model and connect to model

```java
// for chatCLient autoconfigure enabled
package com.example.demo.Chat;

  

import org.springframework.ai.chat.client.ChatClient;

import org.springframework.ai.chat.model.ChatResponse;

import org.springframework.web.bind.annotation.GetMapping;

import org.springframework.web.bind.annotation.RestController;

  

import reactor.core.publisher.Flux;

  

//import org.springframework.web.bind.annotation.RequestParam;

  
  

@RestController

public class ChatController {

  

private final ChatClient chatClient;

  

public ChatController(ChatClient.Builder builder) {

this.chatClient = builder.build();

}

  

@GetMapping("/chat")

public String chat() {

return chatClient.prompt()

.user("Tell me an interesting fact about Java")

.call()

.content();//blocking calls

}

@GetMapping("/stream")

public Flux<String> stream() {

return chatClient.prompt()

.user("I am visting chennai give me 10 place to visit")

.stream()

.content();

}

@GetMapping("/c")

public ChatResponse jole(){

return chatClient.prompt()

.user("in 10 words describe mac not more than 10")

.call()

.chatResponse();

}

}
```

prompts and prompt template 
Structured output
multimodal (Text image and video)

# prompts
