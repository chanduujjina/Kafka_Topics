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

## 6. What are the main annotations used?
- @EnableBinding

- @StreamListener

- @SendTo

- @Input, @Output

- @Bean (for function-style)


## 7. What is a consumer group?
-  A Kafka consumer group is a group of consumers that cooperate to read data from a topic, ensuring each message is only processed once. Configurable via:
```yml
spring.cloud.stream.bindings.input.group=my-group
```

## 8. How does error handling work?
- Spring Cloud Stream allows:

- Automatic retries

- Error channels (binding.errors)

- Dead Letter Queues (DLQ)

```yml
  spring.cloud.stream.bindings.input.consumer:
  maxAttempts: 3
  defaultRetryable: true
```

##  9. What is a Dead Letter Queue (DLQ)?
- A DLQ is a Kafka topic where failed messages are sent after exhausting retry attempts. It allows post-mortem analysis and reprocessing.

 ## 10. How do you test Spring Cloud Stream apps?

 - Use @SpringBootTest

- Use embedded Kafka (e.g., EmbeddedKafkaRule)

- Use MessageCollector or StreamBridge for assertions
