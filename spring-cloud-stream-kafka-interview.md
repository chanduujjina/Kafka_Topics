# Spring Cloud Stream with Kafka - Interview Questions and Answers

## 1. What is Spring Cloud Stream?

**Answer:**  
Spring Cloud Stream is a framework for building event-driven microservices connected with shared messaging systems like Apache Kafka or RabbitMQ. It abstracts messaging details through the concept of binders.

---

## 2. What is a Binder in Spring Cloud Stream?

**Answer:**  
A Binder is a component that connects the application to messaging middleware (Kafka, RabbitMQ). It handles communication between the app and the messaging system, including message conversion, serialization, and topic resolution.

---

## 3. What is the purpose of `StreamBridge` in Spring Cloud Stream?

**Answer:**  
`StreamBridge` is used to programmatically send messages to output bindings (topics) without defining them as `@Bean` or `@StreamListener`. Example:

```java
@Autowired
private StreamBridge streamBridge;

streamBridge.send("output-topic", myMessage);
