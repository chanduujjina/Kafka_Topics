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
```
## 4. How do you configure Kafka in Spring Cloud Stream?
```yaml
spring:
  cloud:
    stream:
      bindings:
        output:
          destination: my-topic
      kafka:
        binder:

          brokers: localhost:9092
```
## 5. How do you define an input and output binding?
```java
public interface MyProcessor {
    @Input("input")
    SubscribableChannel input();

    @Output("output")
    MessageChannel output();
}
```
