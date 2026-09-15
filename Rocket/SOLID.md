
```java
package com.rag.ragex;

import java.util.List;

import java.util.stream.Collectors;

import org.springframework.ai.chat.client.ChatClient;

import org.springframework.ai.document.Document;

import org.springframework.ai.rag.advisor.RetrievalAugmentationAdvisor;

import org.springframework.ai.vectorstore.SearchRequest;

import org.springframework.ai.vectorstore.VectorStore;

import org.springframework.beans.factory.annotation.Value;

import org.springframework.core.io.Resource;

import org.springframework.web.bind.annotation.GetMapping;

import org.springframework.web.bind.annotation.RequestParam;

import org.springframework.web.bind.annotation.RestController;

  

@RestController

public class RAGCONTROLLER {

private final VectorStore vectorStore;

private final ChatClient chatClient;

private final RetrievalAugmentationAdvisor rag;

@Value("classpath:templates/t.st")

Resource st;

@Value("classpath:templates/a.st")

Resource temp;

public RAGCONTROLLER(VectorStore vectorStore,ChatClient.Builder builder,RetrievalAugmentationAdvisor rag) {

this.chatClient=builder.build();

this.vectorStore = vectorStore;

this.rag=rag;

}

@GetMapping("/rag")

public String getMethodName(@RequestParam String param) {

SearchRequest sr = SearchRequest.builder()

.query(param)

.topK(3)

.similarityThreshold(0.5)

.build();

List<Document> doc = vectorStore.similaritySearch(sr);

String d = doc.stream()

.map(Document::getText)

.collect(Collectors.joining(System.lineSeparator()));

return chatClient.prompt()

.system(u -> u.text(temp)

.param("documents",d))

.user(param)

.call()

.content();

}

@GetMapping("/rag/pdf")

public String getMethod(@RequestParam String param) {

SearchRequest sr = SearchRequest.builder()

.query(param)

.topK(3)

.similarityThreshold(0.5)

.build();

List<Document> doc = vectorStore.similaritySearch(sr);

String d = doc.stream()

.map(Document::getText)

.collect(Collectors.joining(System.lineSeparator()));

return chatClient.prompt()

.system(u -> u.text(st)

.param("documents",d))

.user(param)

.call()

.content();

}

@GetMapping("/rags/pdf")

public String getMethods(@RequestParam String param) {

return chatClient.prompt()

.user(param)

.advisors(rag)

.call()

.content();

}

  

}
```
