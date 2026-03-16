---
AWS-SQS
---
---
## 1.1 Introduction to Amazon SQS
--
![Image](https://d2908q01vomqb2.cloudfront.net/fc074d501302eb2b93e2554793fcaf50b3bf7291/2021/08/17/Fig1-queue-integration.png)

![Image](https://d2908q01vomqb2.cloudfront.net/fc074d501302eb2b93e2554793fcaf50b3bf7291/2025/01/29/Serverless-Retry-Mechanism-1-1024x677.jpg)

![Image](https://miro.medium.com/1%2ADRW4lVeUoIc2qS6Wel4Caw.png)

![Image](https://d1.awsstatic.com/legal/AmazonMessaging_SQS_SNS/product-page-diagram_Amazon-SQS.e817373cca6780f567a26cf630526f72b0b2baec.png)

### What is Amazon SQS ?

**Amazon SQS (Simple Queue Service)** is a **fully managed message queue service** provided by Amazon Web Services that allows different applications or services to **communicate with each other asynchronously**.

It helps **decouple applications**, meaning services do not need to communicate directly with each other.

Instead, they communicate through a **queue**.

---

# Simple Definition

**Amazon SQS is a service that stores messages temporarily so that another service can process them later.**

Think of it like a **message waiting line**.

---

# Real Life Example

Imagine a **restaurant order system**.

1. Customer places order
2. Order goes to **order queue**
3. Chef processes orders one by one

| Component   | AWS Equivalent                         |
| ----------- | -------------------------------------- |
| Customer    | Producer (Application sending message) |
| Order Slip  | Message                                |
| Order Queue | SQS Queue                              |
| Chef        | Consumer (Worker processing message)   |

---

# Why Amazon SQS is Used

Applications often need to handle **large workloads**.
If services communicate directly, the system may fail when traffic increases.

SQS solves this problem.

### Benefits

* Decouples microservices
* Handles high traffic
* Improves system reliability
* Prevents system overload
* Scales automatically

---

# Basic Components of SQS

### 1 Producer

Application that **sends messages to the queue**

Example

* Web application
* Payment service
* Order service

### 2 Queue

Temporary **storage for messages**

Messages wait here until processed.

### 3 Consumer

Application that **reads and processes messages**

Example

* Worker servers
* Lambda functions
* Background jobs

---

# Simple Workflow

Step-by-step flow:

1️⃣ Application sends message to **SQS Queue**
2️⃣ Message stored in queue
3️⃣ Worker service reads message
4️⃣ Worker processes task
5️⃣ Message deleted from queue

---

# Example DevOps Use Case

**E-commerce order system**

Step 1
User places order

Step 2
Order service sends message to **SQS**

Step 3
Queue stores order request

Step 4
Worker service processes order

Step 5
Shipping service receives processed order

---

# Key Characteristics

* Fully managed service
* Highly scalable
* Reliable message storage
* Supports millions of messages
* No server management required

---

# Simple Architecture

```
Application (Producer)
        │
        ▼
    Amazon SQS Queue
        │
        ▼
Worker / Lambda (Consumer)
        │
        ▼
Process Task
```

---

# Important Point

SQS uses **asynchronous communication**.

This means:

Service A does not wait for Service B to finish processing.

---
---
## 2. How Amazon SQS Works (Message Lifecycle)

### Overview

In Amazon SQS, messages move through a **simple lifecycle** from **producer → queue → consumer → deletion**.

SQS acts as a **buffer between services**, allowing them to communicate without directly depending on each other.

---

# Step-by-Step Message Lifecycle

## 1. Producer Sends Message

A **producer** (application or service) sends a message to the SQS queue.

Examples of producers:

* Web application
* Microservice
* EC2 application
* Lambda function

Example scenario:

User places an order on a website → the application sends an **order message** to the SQS queue.

```
Producer → SendMessage → SQS Queue
```

---

## 2. Message Stored in Queue

Once the message is sent, SQS **stores it securely in the queue**.

Important characteristics:

* Messages are **stored redundantly across multiple servers**
* They remain in the queue until:

  * A consumer processes them
  * The retention period expires

Default message retention: **4 days**
Maximum retention: **14 days**

---

## 3. Consumer Retrieves Message

A **consumer (worker service)** polls the queue and retrieves messages.

Consumers can be:

* EC2 worker instances
* Lambda functions
* Containers
* Microservices

The consumer uses the API:

```
ReceiveMessage
```

Example:

```
Worker → ReceiveMessage → SQS Queue
```

---

## 4. Visibility Timeout Starts

When a consumer receives a message:

* The message becomes **invisible to other consumers**
* This prevents multiple workers from processing the same message simultaneously.

This time period is called **Visibility Timeout**.

Example:

Visibility Timeout = **30 seconds**

If the worker finishes within 30 seconds → it deletes the message.

If not → the message becomes visible again.

---

## 5. Message Processing

The consumer performs the required task.

Examples:

* Process order
* Resize image
* Send email
* Update database

---

## 6. Delete Message

After successful processing, the consumer deletes the message.

API used:

```
DeleteMessage
```

This ensures the message **is not processed again**.

---

# Complete SQS Workflow

```
Producer (Application)
        │
        │ SendMessage
        ▼
     SQS Queue
        │
        │ ReceiveMessage
        ▼
Consumer / Worker
        │
        │ Process Task
        ▼
 DeleteMessage
```

---

# Real DevOps Example

**Image processing system**

User uploads image → stored in S3

Application sends message to SQS:

```
{
 "image": "photo.jpg",
 "action": "resize"
}
```

Worker service reads message and processes the image.

Services involved:

* Amazon S3
* Amazon SQS
* AWS Lambda

---

# Why This Architecture is Powerful

Benefits:

* Loose coupling between services
* Handles traffic spikes
* Fault-tolerant processing
* Scalable architecture

---

# Quick Interview Tip

**Important APIs of SQS**

| API                     | Purpose                   |
| ----------------------- | ------------------------- |
| SendMessage             | Send message to queue     |
| ReceiveMessage          | Read message from queue   |
| DeleteMessage           | Remove processed message  |
| ChangeMessageVisibility | Modify visibility timeout |

---
---
## 1.3 Types of Amazon SQS Queues

![Image](https://d2908q01vomqb2.cloudfront.net/0716d9708d321ffb6a00818614779e779925365c/2017/03/28/QueueTypes-1.jpg)

![Image](https://d2908q01vomqb2.cloudfront.net/1b6453892473a467d07372d45eb05abc2031647a/2018/05/01/sqs_fifo_blog_img5.png)

![Image](https://docs.aws.amazon.com/images/AWSSimpleQueueService/latest/SQSDeveloperGuide/images/fifo-documentation-single.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2AivcCv41pWPcBJMzwFWlV5A.png)

In **Amazon SQS**, there are **two types of queues** used to store and process messages.

1. **Standard Queue**
2. **FIFO Queue (First-In-First-Out)**

Each queue type is used for different application requirements.

---

# 1. Standard Queue

A **Standard Queue** is the **default queue type** in Amazon SQS.

It is designed for **maximum throughput and scalability**.

### Key Features

* **Unlimited throughput**
* **Best-effort ordering**
* **At-least-once message delivery**
* Very high performance

### Best-effort ordering

Messages are **usually delivered in order**, but **sometimes the order may change**.

Example:

```
Sent messages:
A → B → C

Received messages:
A → C → B
```

### Use Cases

Standard queues are used when **order is not important**.

Examples:

* Log processing
* Image processing
* Background tasks
* Data processing pipelines

---

# 2. FIFO Queue (First-In-First-Out)

A **FIFO Queue** guarantees that messages are processed **in the exact order they are sent**.

FIFO queues are used when **message order is critical**.

### Key Features

* **Strict message ordering**
* **Exactly-once processing**
* Prevents duplicate messages

Example:

```
Sent messages:
A → B → C

Received messages:
A → B → C
```

The order will **always remain the same**.

### Use Cases

FIFO queues are used for systems where **order must be preserved**.

Examples:

* Payment transactions
* Banking systems
* Order processing systems
* Inventory management

---

# Standard Queue vs FIFO Queue

| Feature            | Standard Queue     | FIFO Queue                 |
| ------------------ | ------------------ | -------------------------- |
| Message order      | Not guaranteed     | Guaranteed                 |
| Throughput         | Very high          | Limited                    |
| Duplicate messages | Possible           | Prevented                  |
| Processing type    | At-least-once      | Exactly-once               |
| Use case           | High-speed systems | Ordered processing systems |

---

# Simple Way to Remember

**Standard Queue**

Speed is important.

Example
Log processing, analytics systems.

**FIFO Queue**

Order is important.

Example
Payments, transactions.

---

# Example Architecture

### Standard Queue Example

Web application → SQS → Worker servers

### FIFO Queue Example

Payment system → SQS FIFO → Transaction processor

---

# Important Interview Tip

In **real DevOps architectures**, companies often use:

**SNS + SQS Standard Queue**

because it supports **massive scale and high throughput**.

FIFO is used only when **strict ordering is required**.

---
---
## 1.4 Key Features of Amazon SQS

![Image](https://d2908q01vomqb2.cloudfront.net/fc074d501302eb2b93e2554793fcaf50b3bf7291/2024/08/20/fig5-wesfarmers-queue-1024x482.png)

![Image](https://d2908q01vomqb2.cloudfront.net/fc074d501302eb2b93e2554793fcaf50b3bf7291/2021/04/06/Figure-2-1.png)

![Image](https://d2908q01vomqb2.cloudfront.net/fc074d501302eb2b93e2554793fcaf50b3bf7291/2025/01/29/Serverless-Retry-Mechanism-1-1024x677.jpg)

![Image](https://docs.aws.amazon.com/images/AWSSimpleQueueService/latest/SQSDeveloperGuide/images/sqs-message-lifecycle-diagram.png)

**Amazon SQS** provides several powerful features that make it a reliable **messaging service for distributed applications and microservices**.

Below are the **most important features**.

---

# 1. Fully Managed Service

SQS is a **serverless messaging service** provided by Amazon Web Services.

You **do not need to manage servers**.

AWS handles:

* Infrastructure
* Scaling
* Availability
* Maintenance

This allows developers to **focus only on application logic**.

---

# 2. Decoupling of Applications

SQS helps **separate different components of an application**.

Instead of direct communication between services, they communicate through **queues**.

Example:

```
Web Application → SQS Queue → Worker Service
```

Benefits:

* Independent services
* Easy scaling
* Fault isolation

---

# 3. High Scalability

Amazon SQS automatically **scales to handle millions of messages**.

Even during **traffic spikes**, SQS can process large volumes of messages without affecting application performance.

Example:

* E-commerce sale event
* Thousands of orders per second
* SQS queues handle all messages safely

---

# 4. Message Durability

Messages in SQS are **stored redundantly across multiple AWS servers**.

This ensures:

* No message loss
* High reliability
* Fault tolerance

Even if a server fails, the message remains available.

---

# 5. At-Least-Once Delivery

SQS guarantees that a **message will be delivered at least once** to the consumer.

This means:

* A message may sometimes be delivered **more than once**
* Applications must be designed to **handle duplicate messages**

---

# 6. Message Retention

SQS stores messages for a configurable period.

Default retention: **4 days**

Maximum retention: **14 days**

If a message is not processed within this period, it will be **automatically deleted**.

---

# 7. Visibility Timeout

When a consumer receives a message:

* The message becomes **temporarily invisible** to other consumers
* This prevents **multiple consumers from processing the same message simultaneously**

If the consumer fails to process the message:

* It becomes **visible again**
* Another consumer can process it

---

# 8. Dead Letter Queue (DLQ)

A **Dead Letter Queue** stores messages that **cannot be processed successfully** after multiple retries.

Benefits:

* Helps identify failed messages
* Useful for debugging applications
* Prevents processing loops

---

# 9. Security and Access Control

SQS supports strong security features.

Security options include:

* IAM policies
* Queue policies
* Server-side encryption using AWS KMS

These ensure that **only authorized users or services can access the queue**.

---

# 10. Integration with AWS Services

SQS integrates with many AWS services such as:

* AWS Lambda
* Amazon EC2
* Amazon SNS
* Amazon CloudWatch

This allows building **event-driven architectures**.

---

# Summary

| Feature            | Description                  |
| ------------------ | ---------------------------- |
| Managed Service    | No infrastructure management |
| Decoupling         | Independent services         |
| Scalability        | Handles millions of messages |
| Durability         | Messages stored safely       |
| Delivery           | At least once delivery       |
| Retention          | Up to 14 days storage        |
| Visibility Timeout | Prevent duplicate processing |
| Dead Letter Queue  | Store failed messages        |

---
---
## 1.5 SQS Message Components

![Image](https://miro.medium.com/1%2AOyDvDxqmqdqErL9tYQS4gQ.png)

![Image](https://d2908q01vomqb2.cloudfront.net/fc074d501302eb2b93e2554793fcaf50b3bf7291/2025/01/29/Serverless-Retry-Mechanism-1-1024x677.jpg)

![Image](https://docs.aws.amazon.com/images/AWSSimpleQueueService/latest/SQSDeveloperGuide/images/sqs-msg-attrib-md5.png)

![Image](https://docs.aws.amazon.com/images/AWSSimpleQueueService/latest/SQSDeveloperGuide/images/sqs-message-lifecycle-diagram.png)

In **Amazon SQS**, every message sent to the queue contains several **components** that help identify, process, and manage the message.

These components are important for **applications and message processing systems**.

---

# Main Components of an SQS Message

An SQS message contains **four important parts**:

1. Message Body
2. Message Attributes
3. Message ID
4. Receipt Handle

---

# 1. Message Body

The **Message Body** is the **actual data** sent to the queue.

It contains the **information that the consumer application needs to process**.

### Example

Order processing system

```json
{
 "order_id": "12345",
 "product": "Laptop",
 "quantity": 1
}
```

This data is stored inside the **message body**.

### Important Points

* Maximum size: **256 KB**
* Can contain **text, JSON, XML, or any structured data**
* Processed by the consumer application

---

# 2. Message Attributes

**Message Attributes** provide **additional metadata** about the message.

They help in **filtering, routing, and processing messages**.

Example attributes:

| Attribute | Value   |
| --------- | ------- |
| OrderType | Premium |
| Region    | Asia    |
| Priority  | High    |

Applications can use these attributes to **process messages differently**.

Example:

* High priority orders processed first
* Regional processing rules

---

# 3. Message ID

Every message sent to SQS gets a **unique Message ID** automatically generated by AWS.

Example

```
MessageID: 9f7c2a7d-1e23-4d0c-b345-6c9b8d1e6a7f
```

Purpose:

* Helps identify the message
* Used for tracking and logging
* Useful for debugging

Important:

Message ID **cannot be used to delete a message**.

---

# 4. Receipt Handle

When a consumer receives a message from the queue, SQS generates a **Receipt Handle**.

Example

```
ReceiptHandle: AQEB123456789xyz...
```

This handle is used to **delete the message from the queue**.

### Workflow

1. Consumer receives message
2. SQS provides receipt handle
3. Consumer processes message
4. Consumer deletes message using receipt handle

If the message is **not deleted**, it will appear again in the queue.

---

# Simple Message Structure

Example SQS message:

```
Message
│
├── Message Body (actual data)
├── Message Attributes (metadata)
├── Message ID (unique identifier)
└── Receipt Handle (used to delete message)
```

---

# Example Real Architecture

E-commerce system:

```
Order Service → SQS Queue → Worker Service
```

Message body:

```
Order details
```

Message attributes:

```
OrderType = Express
Priority = High
```

Worker processes the order and **deletes message using Receipt Handle**.

---

# Important Interview Tip

**Message ID ≠ Receipt Handle**

| Component      | Purpose          |
| -------------- | ---------------- |
| Message ID     | Identify message |
| Receipt Handle | Delete message   |

---
---
## 1.6 Visibility Timeout in Amazon SQS

![Image](https://docs.aws.amazon.com/images/AWSSimpleQueueService/latest/SQSDeveloperGuide/images/sqs-visibility-timeout-diagram.png)

![Image](https://docs.aws.amazon.com/images/AWSSimpleQueueService/latest/SQSDeveloperGuide/images/sqs-message-lifecycle-diagram.png)

![Image](https://miro.medium.com/1%2AkYFJFGqHWPOvSONzsMRmlw.png)

![Image](https://miro.medium.com/1%2Aae_H-gCNnJTMtux2NlY0Ow.png)

**Visibility Timeout** is one of the most important concepts in **Amazon SQS**.

It controls **how long a message stays hidden from other consumers after being received by one consumer**.

This prevents **multiple consumers from processing the same message at the same time**.

---

# Simple Definition

**Visibility Timeout = Time during which a message becomes invisible to other consumers after it is received.**

---

# Why Visibility Timeout is Needed

In distributed systems, multiple workers may read messages from the same queue.

Without visibility timeout:

* Two workers may process **the same message**
* This can cause **duplicate processing**

Visibility timeout solves this problem.

---

# Step-by-Step Working

1️⃣ Producer sends message to queue

2️⃣ Message is stored in SQS

3️⃣ Consumer reads the message

4️⃣ Message becomes **invisible to other consumers**

5️⃣ Consumer processes the task

6️⃣ Consumer deletes the message

---

# Example Workflow

```text
Application → SQS Queue → Worker 1
                         Worker 2
```

Step-by-step:

1. Message arrives in queue
2. Worker 1 receives message
3. Message becomes **invisible**
4. Worker 1 processes task
5. Worker 1 deletes message

Worker 2 **cannot see the message during this time**.

---

# What Happens if Consumer Fails

If the worker crashes or fails to process the message:

* Message is **not deleted**
* After visibility timeout expires
* Message becomes **visible again**

Another worker can then process it.

Example:

```text
Worker 1 fails
Visibility timeout ends
Worker 2 receives message
```

---

# Default Visibility Timeout

Default value:

**30 seconds**

Maximum value:

**12 hours**

You can configure it based on your application needs.

Example:

| Application           | Recommended Timeout |
| --------------------- | ------------------- |
| Image processing      | 5 minutes           |
| Video processing      | 30 minutes          |
| Large data processing | 1 hour              |

---

# Important DevOps Example

Example architecture:

```text
EC2 Worker → SQS Queue → Lambda Worker
```

If Lambda takes **20 seconds** to process the message:

Visibility timeout should be **greater than 20 seconds**.

Otherwise the message may be **processed twice**.

---

# Visibility Timeout vs Message Retention

| Feature            | Purpose                                    |
| ------------------ | ------------------------------------------ |
| Visibility Timeout | Temporary message hiding during processing |
| Message Retention  | Total time message stays in queue          |

---

# Interview Tip

Common interview question:

**What happens if a consumer receives a message but does not delete it?**

Answer:

After the **visibility timeout expires**, the message becomes visible again and can be processed by another consumer.

---
---
## 1.7 Message Retention Period in Amazon SQS

![Image](https://docs.aws.amazon.com/images/AWSSimpleQueueService/latest/SQSDeveloperGuide/images/sqs-visibility-timeout-diagram.png)

![Image](https://docs.aws.amazon.com/images/AWSSimpleQueueService/latest/SQSDeveloperGuide/images/sqs-message-lifecycle-diagram.png)

![Image](https://hidekazu-konishi.com/images/aws_history_and_timeline_amazon_sqs_001.png)

![Image](https://docs.aws.amazon.com/images/AWSSimpleQueueService/latest/SQSDeveloperGuide/images/ArchOverview.png)

The **Message Retention Period** in **Amazon SQS** defines **how long a message stays in the queue before it is automatically deleted** if it is not processed.

It ensures that messages do not remain in the queue forever.

---

# Simple Definition

**Message Retention Period = The amount of time a message remains in the queue before AWS automatically deletes it.**

---

# Default and Maximum Retention Time

| Setting           | Time         |
| ----------------- | ------------ |
| Default retention | **4 days**   |
| Minimum retention | **1 minute** |
| Maximum retention | **14 days**  |

You can configure this based on your application requirements.

---

# How Message Retention Works

Step-by-step process:

1️⃣ Producer sends message to the queue

2️⃣ Message is stored in **SQS queue**

3️⃣ Consumer reads and processes message

4️⃣ Consumer deletes message

If the message is **not deleted**, it stays in the queue until the **retention period expires**.

After that, AWS automatically **removes the message permanently**.

---

# Example Workflow

```text
Application → SQS Queue → Worker
```

Scenario:

* Message arrives in queue
* Worker fails to process message
* Message remains in queue

If retention = **4 days**

After **4 days**, the message is automatically **deleted**.

---

# Example Use Case

E-commerce order system:

```text
Order Service → SQS Queue → Order Processor
```

Scenario:

* Order message stored in queue
* Processing service temporarily down

Message stays in queue until:

* Service processes it **OR**
* Retention period expires

This prevents **data loss during system failures**.

---

# Message Retention vs Visibility Timeout

| Feature            | Purpose                                       |
| ------------------ | --------------------------------------------- |
| Visibility Timeout | Temporary hiding of message during processing |
| Message Retention  | Total lifetime of message in queue            |

Example:

| Scenario           | Value      |
| ------------------ | ---------- |
| Visibility timeout | 30 seconds |
| Message retention  | 4 days     |

---

# Important DevOps Tip

Set retention period based on **failure recovery requirements**.

Example:

| Application                | Recommended Retention |
| -------------------------- | --------------------- |
| Order processing           | 4–7 days              |
| Log processing             | 1–2 days              |
| Critical financial systems | 7–14 days             |

Longer retention allows **systems to recover messages after outages**.

---

# Important Interview Question

**What happens if a message is not processed in SQS?**

Answer:

The message remains in the queue until:

1. It is processed and deleted, or
2. The **message retention period expires**, after which AWS automatically deletes it.

---
---
## 1.8 Long Polling vs Short Polling in Amazon SQS

![Image](https://docs.aws.amazon.com/images/AWSSimpleQueueService/latest/SQSDeveloperGuide/images/ArchOverview_Receive.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/0%2AW15hvfpA4wmv2ZRv.png)

![Image](https://baselime.io/images/blog/sqs-guide/sqs-lambda.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/0%2AyXZ_wveRwy55NO_L.png)

In **Amazon SQS**, **polling** is the process by which a **consumer checks the queue to receive messages**.

There are **two types of polling** used to retrieve messages:

1. **Short Polling**
2. **Long Polling**

These affect **performance, latency, and cost**.

---

# 1. Short Polling

**Short Polling** is the default behavior when a consumer requests messages from the SQS queue.

When the consumer sends a request:

* SQS checks **only a subset of servers**
* If a message is available → it returns immediately
* If no message is found → response returns empty

### Example Workflow

```text
Consumer → SQS → No message → Empty response
```

Even if messages exist on other servers, the consumer may still receive **no messages**.

### Problems with Short Polling

* Many **empty responses**
* Higher **API request cost**
* Inefficient message retrieval

---

# 2. Long Polling

**Long Polling** improves efficiency by allowing the consumer to **wait for messages to arrive**.

Instead of immediately returning an empty response, SQS **waits for a specified time**.

Maximum wait time:

**20 seconds**

### Example Workflow

```text
Consumer → SQS → Waits for message → Returns message
```

If a message arrives during the waiting period, SQS **returns it immediately**.

---

# Comparison: Long Polling vs Short Polling

| Feature               | Short Polling  | Long Polling      |
| --------------------- | -------------- | ----------------- |
| Queue servers checked | Subset         | All servers       |
| Response time         | Immediate      | Waits for message |
| Empty responses       | More frequent  | Reduced           |
| Cost efficiency       | Lower          | Higher            |
| Performance           | Less efficient | More efficient    |

---

# Simple Example

Application architecture:

```text
Web App → SQS Queue → Worker Service
```

Scenario:

Worker requests messages.

**Short Polling**

```text
Worker → SQS → No message → Empty response
Worker → SQS → No message → Empty response
```

Many unnecessary requests.

**Long Polling**

```text
Worker → SQS → Waits → Message arrives → Returns message
```

Fewer requests and **better performance**.

---

# How to Enable Long Polling

You can enable long polling by setting:

**ReceiveMessageWaitTimeSeconds**

Example:

```bash
aws sqs receive-message \
--queue-url QUEUE_URL \
--wait-time-seconds 20
```

Maximum wait time:

**20 seconds**

---

# Benefits of Long Polling

* Reduces empty responses
* Improves efficiency
* Reduces API request cost
* Faster message retrieval

---

# DevOps Best Practice

Always use **Long Polling** for production systems.

This improves **performance and cost efficiency** when using **Amazon SQS**.

---
---
## 1.9 Dead Letter Queue (DLQ)

![Image](https://d2908q01vomqb2.cloudfront.net/1b6453892473a467d07372d45eb05abc2031647a/2020/11/17/sqs-newarch.png)

![Image](https://pubudu.dev/posts/dead-letter-queue-for-aws-step-functions/featured.png)

![Image](https://d2908q01vomqb2.cloudfront.net/1b6453892473a467d07372d45eb05abc2031647a/2020/11/13/sqs1.png)

![Image](https://d2908q01vomqb2.cloudfront.net/fc074d501302eb2b93e2554793fcaf50b3bf7291/2025/01/29/Serverless-Retry-Mechanism-1-952x630.jpg)

A **Dead Letter Queue (DLQ)** is a special queue used in **Amazon SQS** to store messages that **cannot be processed successfully after multiple attempts**.

It helps developers **identify and troubleshoot failed messages**.

---

# Simple Definition

**Dead Letter Queue (DLQ) = Queue that stores messages that fail processing multiple times.**

Instead of repeatedly retrying the same message, SQS moves it to a **DLQ for investigation**.

---

# Why Dead Letter Queue is Needed

In real systems, some messages may fail because of:

* Application errors
* Invalid message format
* Database failures
* Network issues
* Dependency failures

Without DLQ:

* Messages keep retrying forever
* System resources get wasted

DLQ helps **separate failed messages from normal processing**.

---

# How DLQ Works

Step-by-step process:

1️⃣ Producer sends message to **SQS queue**

2️⃣ Consumer receives message

3️⃣ Consumer tries to process message

4️⃣ Processing fails

5️⃣ Message is retried multiple times

6️⃣ After reaching **maximum retry limit**, message moves to **Dead Letter Queue**

---

# Example Workflow

```text
Application → Main Queue → Worker
                     │
                     │ (Processing fails)
                     ▼
               Dead Letter Queue
```

The failed message is **moved to DLQ** for debugging.

---

# Maximum Receive Count

DLQ works based on **Maximum Receive Count**.

This value defines **how many times a message can be retried** before moving to the DLQ.

Example configuration:

| Setting           | Value               |
| ----------------- | ------------------- |
| Max Receive Count | 5                   |
| Action            | Move message to DLQ |

Scenario:

```text
Attempt 1 → Fail
Attempt 2 → Fail
Attempt 3 → Fail
Attempt 4 → Fail
Attempt 5 → Fail
```

After 5 failures → message goes to **DLQ**.

---

# Example Real Use Case

E-commerce order system

```text
Order Service → SQS Queue → Order Processor
                          │
                          │ Order fails
                          ▼
                       DLQ
```

Possible issue:

* Invalid order data
* Payment failure
* Inventory error

Developers can analyze the message stored in the DLQ.

---

# Benefits of Dead Letter Queue

* Helps identify failed messages
* Prevents infinite retry loops
* Improves system reliability
* Easier debugging
* Better monitoring

---

# DLQ Monitoring

DLQ messages can be monitored using:

* Amazon CloudWatch
* Logging systems
* Alerting systems

Alerts can notify DevOps teams when **DLQ messages increase**.

---

# DevOps Best Practice

Always configure **Dead Letter Queue** for production systems.

This ensures:

* Failed messages are captured
* Systems remain stable
* Issues are easier to debug

---

# Interview Question

**What happens when a message fails multiple times in SQS?**

Answer:

After reaching the **maximum receive count**, the message is automatically moved to the **Dead Letter Queue (DLQ)**.

---
---
## 1.10 SQS Security (IAM, Policies, Encryption)

![Image](https://d2908q01vomqb2.cloudfront.net/22d200f8670dbdb3e253a90eee5098477c95c23d/2023/02/25/img1-8.png)

![Image](https://docs.aws.amazon.com/images/AWSSimpleQueueService/latest/SQSDeveloperGuide/images/AccessPolicyLanguage_Arch_Overview.png)

![Image](https://d2908q01vomqb2.cloudfront.net/22d200f8670dbdb3e253a90eee5098477c95c23d/2022/06/01/HowAndWhenWithRolesBlog.drawio.png)

![Image](https://docs.aws.amazon.com/images/IAM/latest/UserGuide/images/intro-diagram%20_policies_800.png)

Security is an important aspect of **Amazon SQS**.
It ensures that **only authorized users and services can send or receive messages from the queue**.

Security in SQS is mainly implemented using:

1. IAM Policies
2. Queue Policies
3. Encryption (KMS)
4. Network Security

---

# 1. IAM (Identity and Access Management)

AWS Identity and Access Management allows you to **control who can access SQS resources**.

Using IAM you can allow or deny permissions such as:

* Create queue
* Send message
* Receive message
* Delete message

### Example IAM Policy

```json
{
 "Effect": "Allow",
 "Action": [
   "sqs:SendMessage",
   "sqs:ReceiveMessage",
   "sqs:DeleteMessage"
 ],
 "Resource": "arn:aws:sqs:region:account-id:queue-name"
}
```

This policy allows a user or service to **send, receive, and delete messages**.

---

# 2. SQS Queue Policies

Queue policies are **resource-based policies** attached directly to an SQS queue.

They define **which services or accounts can access the queue**.

Example:

Allow **Amazon SNS** to send messages to an SQS queue.

Example policy concept:

```text
SNS Topic → SQS Queue
```

This is commonly used in **SNS fanout architectures**.

---

# 3. Encryption (Data Protection)

SQS supports **server-side encryption** to protect messages.

Encryption is handled using:

AWS Key Management Service

Encryption protects:

* Message body
* Sensitive application data
* Confidential business information

### Encryption types

| Type    | Description                           |
| ------- | ------------------------------------- |
| SSE-SQS | AWS managed encryption                |
| SSE-KMS | Customer managed encryption using KMS |

---

# 4. Network Security

SQS can be secured using:

* **VPC endpoints**
* Private communication inside AWS network
* No public internet exposure

Using **VPC endpoints** allows services like **Amazon EC2** to access SQS **securely within the VPC**.

Example architecture:

```text
EC2 Instance (VPC)
        │
        ▼
   VPC Endpoint
        │
        ▼
     Amazon SQS
```

---

# Security Best Practices

Best practices for securing SQS:

* Use **IAM roles instead of access keys**
* Enable **encryption with KMS**
* Restrict queue access using **least privilege principle**
* Monitor access using **CloudWatch and CloudTrail**

Monitoring services:

* Amazon CloudWatch
* AWS CloudTrail

---

# Real DevOps Architecture Example

Secure architecture example:

```text
Application → IAM Role → SQS Queue → Worker
                         │
                         ▼
                     Encryption (KMS)
```

Security layers:

* IAM authentication
* Queue policy authorization
* Encryption protection

---

# Important Interview Question

**How do you secure an SQS queue?**

Answer:

SQS security can be implemented using:

1. IAM policies
2. Queue policies
3. Encryption using KMS
4. VPC endpoints for network security

---
---
## 1.11 Amazon SQS Pricing Model

![Image](https://d2908q01vomqb2.cloudfront.net/fc074d501302eb2b93e2554793fcaf50b3bf7291/2025/01/29/Serverless-Retry-Mechanism-1-1024x677.jpg)

![Image](https://d2908q01vomqb2.cloudfront.net/fc074d501302eb2b93e2554793fcaf50b3bf7291/2025/02/24/archblog-1041-featurepng-1024x579.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2ArvUfSxVuRjAjp8M3YywYAQ.png)

![Image](https://awsfundamentals.com/_next/image?q=75\&url=%2Fassets%2Fblog%2Fsqs-pricing%2F601dac8e-4acc-4243-a8b1-5f3cb39f58c0.webp\&w=3840)

The pricing of **Amazon SQS** is **simple and request-based**.

You **pay only for the number of requests** your application makes to the SQS service.

There are **no charges for idle queues**.

---

# 1. Free Tier

AWS provides a **free usage tier** every month.

Free Tier includes:

* **1 million SQS requests per month**

Requests include:

* SendMessage
* ReceiveMessage
* DeleteMessage

This free tier is useful for **small applications and learning environments**.

---

# 2. Request-Based Pricing

SQS charges based on **API requests** made to the queue.

Examples of requests:

| Request Type            | Description               |
| ----------------------- | ------------------------- |
| SendMessage             | Send message to queue     |
| ReceiveMessage          | Read message from queue   |
| DeleteMessage           | Remove processed message  |
| ChangeMessageVisibility | Modify visibility timeout |

Each API call counts as **one request**.

---

# 3. Standard Queue Pricing

For **Standard Queues**, pricing is very low.

Typical pricing concept:

* **Per 1 million requests → small cost**

Example:

Application processing:

```text
Send message
Receive message
Delete message
```

This equals **3 requests** for one message.

---

# 4. FIFO Queue Pricing

**FIFO queues** are slightly more expensive than standard queues.

Reason:

* They provide **strict message ordering**
* They guarantee **exactly-once processing**

FIFO also supports **message deduplication**.

---

# 5. Payload Size Cost

SQS pricing also depends on **message size**.

* First **64 KB** = 1 request
* Every additional **64 KB** = additional request

Example:

| Message Size | Requests Charged |
| ------------ | ---------------- |
| 64 KB        | 1 request        |
| 128 KB       | 2 requests       |
| 192 KB       | 3 requests       |

Maximum message size: **256 KB**

---

# 6. Data Transfer Cost

In most cases:

Data transfer **within AWS services in the same region is free**.

Example architecture:

```text
EC2 → SQS → Lambda
```

Since all services are in the same region, **no additional transfer cost**.

Services commonly integrated with SQS:

* Amazon EC2
* AWS Lambda
* Amazon SNS

---

# Example Cost Calculation

Suppose your system processes **1 million messages**.

For each message:

1. SendMessage
2. ReceiveMessage
3. DeleteMessage

Total requests:

```text
1 million × 3 = 3 million requests
```

You would pay only for the **request count beyond the free tier**.

---

# Why SQS is Cost Efficient

Benefits:

* Pay only for requests
* No server costs
* No infrastructure maintenance
* Automatic scaling

This makes SQS ideal for:

* Microservices
* Event-driven architectures
* Serverless systems

---

# DevOps Best Practice

To reduce SQS costs:

* Use **Long Polling**
* Use **Message Batching**
* Avoid unnecessary API calls
* Optimize message size

---

# Interview Question

**How does Amazon SQS pricing work?**

Answer:

Amazon SQS uses a **request-based pricing model**, where users pay for the number of **API requests (Send, Receive, Delete)** made to the queue.

---
---
## 1.12 SQS Integration with AWS Services

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2A9z3sbaE6yGT1Ukau8iq4ew.png)

![Image](https://d2908q01vomqb2.cloudfront.net/fc074d501302eb2b93e2554793fcaf50b3bf7291/2021/02/01/Arch-Diagram2-1260x496.jpg)

![Image](https://d2908q01vomqb2.cloudfront.net/fc074d501302eb2b93e2554793fcaf50b3bf7291/2025/01/29/Serverless-Retry-Mechanism-1-952x630.jpg)

![Image](https://d2908q01vomqb2.cloudfront.net/1b6453892473a467d07372d45eb05abc2031647a/2020/11/07/scatter4.png)

**Amazon SQS** integrates with many services in **Amazon Web Services** to build **scalable and event-driven architectures**.

These integrations allow applications to process messages **asynchronously and reliably**.

Below are the most common integrations used in **real DevOps architectures**.

---

# 1. SQS + AWS Lambda

AWS Lambda can automatically process messages from SQS.

### How it works

1. Message arrives in SQS
2. Lambda is triggered automatically
3. Lambda processes the message

### Architecture

```text
Application → SQS Queue → Lambda Function → Process Task
```

### Use Cases

* Image processing
* File processing
* Data transformation
* Event-driven automation

---

# 2. SQS + EC2

Applications running on **Amazon EC2** can act as **workers** that process SQS messages.

### Workflow

```text
Web Application → SQS Queue → EC2 Worker Instances
```

Workers continuously poll the queue and process messages.

### Use Cases

* Background jobs
* Order processing
* Batch processing

---

# 3. SQS + SNS (Fanout Architecture)

Amazon SNS can send messages to **multiple SQS queues simultaneously**.

This pattern is called the **Fanout Pattern**.

### Architecture

```text
Application → SNS Topic
                   │
        ┌──────────┼──────────┐
        ▼          ▼          ▼
     SQS Queue   SQS Queue   SQS Queue
```

Each queue processes the message independently.

### Example

Order created event:

* Inventory service receives message
* Shipping service receives message
* Billing service receives message

---

# 4. SQS + Amazon S3

Amazon S3 can trigger events that send messages to SQS.

### Workflow

```text
User Upload → S3 Bucket → SQS Queue → Worker
```

### Use Cases

* Image processing
* Video processing
* Data pipelines

---

# 5. SQS + CloudWatch

Amazon CloudWatch monitors SQS performance and metrics.

Important metrics:

* Queue length
* Number of messages received
* Message processing time

Example monitoring architecture:

```text
SQS Queue → CloudWatch Metrics → Alerts
```

DevOps teams receive alerts if queue size increases.

---

# 6. SQS + Auto Scaling

SQS queue length can be used to **scale EC2 worker instances automatically**.

Architecture:

```text
Application → SQS Queue → EC2 Workers
                         │
                         ▼
                   Auto Scaling
```

If queue messages increase → more EC2 workers start.

If queue becomes empty → workers scale down.

---

# Real DevOps Architecture Example

Typical production architecture:

```text
User Request
      │
      ▼
   Web App
      │
      ▼
   SNS Topic
      │
      ├── SQS Queue → Lambda Processor
      ├── SQS Queue → EC2 Workers
      └── SQS Queue → Analytics Service
```

This architecture is **highly scalable and fault tolerant**.

---

# Why SQS Integration is Powerful

Benefits:

* Event-driven architecture
* Microservice communication
* Reliable message processing
* Scalable workloads
* Fault-tolerant systems

---

# Interview Question

**Which AWS services integrate with SQS?**

Answer:

Common integrations include:

* AWS Lambda
* Amazon EC2
* Amazon SNS
* Amazon S3
* Amazon CloudWatch

---
---
## 1.13 Real-World Use Cases of Amazon SQS

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2A9z3sbaE6yGT1Ukau8iq4ew.png)

![Image](https://assets.community.aws/a/2eUDSQraRpeohPQsfvSFVj5koCt/fano.webp)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2AEMDu5adNhAz99B9H9OXkpQ.jpeg)

![Image](https://media.licdn.com/dms/image/sync/v2/D4D27AQHDsi8GIxnWAQ/articleshare-shrink_800/B4DZqbSHHfJIAI-/0/1763541809463?e=2147483647\&t=gFhU-6ZQj3cyLMruvtdGWFFM7vzCV1ZqhZaeJowbmdY\&v=beta)

**Amazon SQS** is widely used in production systems to **decouple services and process tasks asynchronously**.
Many companies use SQS to build **scalable and reliable distributed systems**.

Below are common **real-world use cases**.

---

# 1. E-commerce Order Processing

One of the most common uses of SQS is **order processing systems**.

### Architecture

```text
User → Web Application → SQS Queue → Order Processing Worker
```

### Workflow

1. Customer places an order
2. Application sends order message to SQS
3. Worker service processes the order
4. Inventory and shipping systems are updated

### Benefits

* Handles high traffic during sales
* Prevents system overload
* Reliable order processing

---

# 2. Background Job Processing

Many applications have **time-consuming tasks** that should run in the background.

Example tasks:

* Sending emails
* Image processing
* Report generation
* Data transformation

### Architecture

```text
Application → SQS Queue → Worker Servers
```

Workers process tasks **asynchronously without slowing down the main application**.

---

# 3. Microservices Communication

In microservices architecture, services communicate through **message queues instead of direct API calls**.

### Architecture

```text
Service A → SQS Queue → Service B
```

Example:

* Payment service sends message
* Billing service processes it

Benefits:

* Loose coupling
* Better scalability
* Fault tolerance

---

# 4. Image and Video Processing

Applications that handle media often use SQS.

Example architecture with **Amazon S3**:

```text
User Upload → S3 Bucket → SQS Queue → Image Processing Worker
```

Processing tasks:

* Resize images
* Compress videos
* Generate thumbnails

Workers process files **in the background**.

---

# 5. Log Processing Systems

Large systems generate huge volumes of logs.

Instead of processing logs immediately, they are sent to SQS.

### Architecture

```text
Application Logs → SQS Queue → Log Processor
```

Log processors analyze logs and store them in analytics systems.

This prevents the main application from slowing down.

---

# 6. Batch Data Processing

Data pipelines often use SQS for batch processing.

Example workflow:

```text
Data Producer → SQS Queue → Data Processing Service
```

Examples:

* Data analytics pipelines
* ETL processing
* Machine learning data preparation

---

# 7. Event-Driven Architecture

SQS is often used with **Amazon SNS** to create event-driven systems.

### Architecture

```text
Application → SNS Topic
                │
        ┌───────┼────────┐
        ▼       ▼        ▼
     SQS Q1   SQS Q2   SQS Q3
```

Each queue processes events independently.

Example:

* Notification service
* Analytics service
* Audit service

---

# Why Companies Use SQS

Benefits in production systems:

* Handles millions of messages
* Highly reliable message storage
* Scalable architecture
* Prevents system overload
* Enables microservices communication

---

# Example Production Architecture

Typical modern cloud architecture:

```text
Users
  │
  ▼
Web Application
  │
  ▼
SNS Topic
  │
  ├── SQS Queue → Lambda Processor
  ├── SQS Queue → EC2 Worker
  └── SQS Queue → Analytics Pipeline
```

Services used:

* Amazon SQS
* Amazon SNS
* AWS Lambda
* Amazon EC2

---

# Interview Question

**Give some real-world use cases of Amazon SQS.**

Answer:

Amazon SQS is used for:

* Order processing systems
* Background job processing
* Microservices communication
* Media processing systems
* Log processing pipelines
* Event-driven architectures

---
---
## 1.14 Amazon SQS Hands-on Practical Guide

![Image](https://d2908q01vomqb2.cloudfront.net/fc074d501302eb2b93e2554793fcaf50b3bf7291/2021/08/17/Fig1-queue-integration.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1200/1%2AB2w0aHFUwYPmL-2TNi2JqQ.png)

![Image](https://d2908q01vomqb2.cloudfront.net/1b6453892473a467d07372d45eb05abc2031647a/2019/07/26/Selection_015.png)

![Image](https://miro.medium.com/1%2ADMWJ3ESTqc5Ox7EAMsxqrg.png)

This section shows a **simple practical example** of how to use **Amazon SQS**.

We will perform these steps:

1. Create an SQS Queue
2. Send a Message
3. Receive a Message
4. Delete a Message

This is the **basic workflow used in real applications**.

---

# 1. Create an SQS Queue

Steps:

1. Login to **AWS Management Console**
2. Go to **SQS service**
3. Click **Create Queue**

Choose queue type:

* **Standard Queue**
* **FIFO Queue**

Example configuration:

| Setting            | Value       |
| ------------------ | ----------- |
| Queue Name         | order-queue |
| Queue Type         | Standard    |
| Visibility Timeout | 30 seconds  |
| Message Retention  | 4 days      |

Click **Create Queue**.

Queue created successfully.

---

# 2. Send a Message to the Queue

Now we send a message from the producer application.

Steps:

1. Open the created queue
2. Click **Send and receive messages**
3. Enter message body

Example message:

```json
{
 "order_id": "1001",
 "product": "Laptop",
 "quantity": 1
}
```

Click **Send Message**.

The message is now stored in the **SQS queue**.

---

# 3. Receive Message from Queue

Now a consumer reads the message.

Steps:

1. Go to queue
2. Click **Send and receive messages**
3. Click **Poll for messages**

The message will appear in the console.

Example received message:

```json
{
 "order_id": "1001",
 "product": "Laptop",
 "quantity": 1
}
```

The worker service can now process this message.

---

# 4. Delete the Message

After processing the message, the consumer must delete it.

Steps:

1. Select the received message
2. Click **Delete**

This removes the message from the queue permanently.

If the message is **not deleted**, it will become visible again after the **visibility timeout**.

---

# CLI Example (DevOps Method)

Using **AWS CLI**.

Send message:

```bash
aws sqs send-message \
--queue-url QUEUE_URL \
--message-body "Hello from SQS"
```

Receive message:

```bash
aws sqs receive-message \
--queue-url QUEUE_URL
```

Delete message:

```bash
aws sqs delete-message \
--queue-url QUEUE_URL \
--receipt-handle RECEIPT_HANDLE
```

---

# Simple Workflow

```text
Application (Producer)
        │
        ▼
   SQS Queue
        │
        ▼
Worker (Consumer)
        │
        ▼
Process Task → Delete Message
```

---

# Real DevOps Architecture Example

Production architecture may include:

* Amazon SQS
* AWS Lambda
* Amazon EC2
* Amazon SNS

Example:

```text
Web Application → SNS → SQS → Lambda / EC2 Worker
```

This ensures **asynchronous processing and scalability**.

---

# Interview Question

**What are the basic steps to use Amazon SQS?**

Answer:

1. Create a queue
2. Send message to the queue
3. Consumer receives message
4. Process message
5. Delete message from queue

---
## 1.15 Amazon SQS Best Practices

![Image](https://d2908q01vomqb2.cloudfront.net/fc074d501302eb2b93e2554793fcaf50b3bf7291/2025/02/24/archblog-1041-featurepng-1024x579.png)

![Image](https://d2908q01vomqb2.cloudfront.net/fc074d501302eb2b93e2554793fcaf50b3bf7291/2023/07/17/Fig3-fanout.png)

![Image](https://d2908q01vomqb2.cloudfront.net/fc074d501302eb2b93e2554793fcaf50b3bf7291/2022/12/20/Figure-1.-Solution-architecture-for-S3-Glacier-object-restore-1024x665.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2AI2BvwlbD_wVlokjD9BE3Fg.jpeg)

When using **Amazon SQS** in production systems, following best practices helps ensure **reliability, scalability, and cost efficiency**.

Below are important **best practices used in real DevOps architectures**.

---

# 1. Use Long Polling

Enable **long polling** to reduce unnecessary API calls.

Benefits:

* Fewer empty responses
* Reduced cost
* Improved message retrieval efficiency

Example configuration:

```text
ReceiveMessageWaitTimeSeconds = 20
```

Maximum wait time: **20 seconds**

---

# 2. Enable Dead Letter Queue (DLQ)

Always configure a **Dead Letter Queue** to handle failed messages.

Benefits:

* Prevents infinite retry loops
* Captures problematic messages
* Makes debugging easier

Example architecture:

```text
Main Queue → Worker
      │
      ▼
   Dead Letter Queue
```

---

# 3. Delete Messages After Processing

After processing a message, always **delete it from the queue**.

If a message is not deleted:

* It becomes visible again
* Another consumer may process it again

Example workflow:

```text
Receive Message → Process Task → Delete Message
```

---

# 4. Use Message Batching

Instead of sending one message at a time, send **multiple messages in a batch**.

Batch size:

Up to **10 messages per request**

Benefits:

* Reduces API requests
* Improves performance
* Reduces cost

Example API:

```text
SendMessageBatch
```

---

# 5. Configure Visibility Timeout Properly

Visibility timeout should be **longer than the processing time**.

Example:

| Task             | Visibility Timeout |
| ---------------- | ------------------ |
| Image processing | 2 minutes          |
| Video processing | 10 minutes         |
| Data processing  | 30 minutes         |

Incorrect timeout can cause **duplicate processing**.

---

# 6. Monitor Queue Metrics

Monitor queues using **Amazon CloudWatch**.

Important metrics:

| Metric                             | Meaning                   |
| ---------------------------------- | ------------------------- |
| ApproximateNumberOfMessagesVisible | Messages waiting in queue |
| ApproximateAgeOfOldestMessage      | Processing delay          |
| NumberOfMessagesReceived           | Worker activity           |

Alerts should be configured if queue size increases.

---

# 7. Use Auto Scaling for Workers

Scale worker instances based on queue size.

Example architecture:

```text
Application → SQS Queue → EC2 Worker
                         │
                         ▼
                     Auto Scaling
```

If queue size increases → launch more workers.

Workers may run on:

* Amazon EC2
* AWS Lambda

---

# 8. Use Idempotent Message Processing

Because SQS provides **at-least-once delivery**, duplicate messages may occur.

Applications should handle duplicates safely.

Example:

If order **123** is processed twice, the system should avoid **duplicate orders**.

---

# 9. Use Encryption for Sensitive Data

Enable encryption using:

AWS Key Management Service

This protects:

* Message body
* Confidential business data
* Sensitive application information

---

# 10. Use Standard Queue for High Throughput

Choose queue type carefully.

| Queue Type     | Best Use                |
| -------------- | ----------------------- |
| Standard Queue | High throughput systems |
| FIFO Queue     | Strict ordering systems |

Most production systems use **Standard Queues**.

---

# Summary

Key best practices:

* Use **Long Polling**
* Configure **Dead Letter Queue**
* Delete messages after processing
* Use **message batching**
* Monitor queues using CloudWatch
* Configure proper **visibility timeout**
* Scale workers automatically

---

# Interview Question

**What are the best practices when using Amazon SQS?**

Answer:

Best practices include:

* Enabling long polling
* Using dead letter queues
* Monitoring queues with CloudWatch
* Deleting messages after processing
* Configuring visibility timeout properly
* Using message batching

---
---
## 1.16 Amazon SQS Monitoring

![Image](https://miro.medium.com/1%2AVdyEtjLNBBb_DzM4kWJMuQ.jpeg)

![Image](https://cdn.prod.website-files.com/681e366f54a6e3ce87159ca4/6877c688d9f8258a03d554f0_How-to-monitor-AWS-SQS-with-Prometheus-03.png)

![Image](https://www.elastic.co/guide/en/observability/8.19/images/sqs-dashboard.png)

![Image](https://cdn.prod.website-files.com/681e366f54a6e3ce87159ca4/6877c688d9f8258a03d55503_How-to-monitor-AWS-SQS-with-Prometheus-10.png)

Monitoring is essential when running **Amazon SQS** in production systems.

It helps DevOps teams **track queue performance, detect failures, and scale systems automatically**.

SQS monitoring is mainly done using **Amazon CloudWatch**.

---

# Why Monitoring SQS is Important

Monitoring helps detect problems such as:

* Message processing delays
* Worker failures
* Increasing queue backlog
* System performance issues

This allows teams to **respond quickly and maintain system reliability**.

---

# Key SQS Metrics in CloudWatch

CloudWatch automatically collects metrics from SQS.

Important metrics include:

| Metric                                | Description                      |
| ------------------------------------- | -------------------------------- |
| ApproximateNumberOfMessagesVisible    | Messages waiting to be processed |
| ApproximateNumberOfMessagesNotVisible | Messages being processed         |
| ApproximateAgeOfOldestMessage         | Age of the oldest message        |
| NumberOfMessagesSent                  | Total messages sent              |
| NumberOfMessagesReceived              | Messages received by consumers   |
| NumberOfMessagesDeleted               | Messages successfully processed  |

These metrics help identify **system performance issues**.

---

# Example Monitoring Scenario

Architecture:

```text
Application → SQS Queue → Worker Instances
                     │
                     ▼
                CloudWatch
```

Monitoring example:

* Queue size increases → workers cannot keep up
* Oldest message age increases → processing delay

This indicates **system bottleneck**.

---

# Setting CloudWatch Alarms

CloudWatch alarms notify DevOps teams when thresholds are exceeded.

Example alarm configuration:

| Metric       | Threshold       |
| ------------ | --------------- |
| Queue length | > 1000 messages |
| Message age  | > 5 minutes     |

If these limits are exceeded:

* CloudWatch sends alerts
* Auto scaling can start additional workers

---

# Auto Scaling with Monitoring

Monitoring metrics can trigger automatic scaling.

Example architecture:

```text
SQS Queue
   │
   ▼
CloudWatch Metrics
   │
   ▼
Auto Scaling
   │
   ▼
EC2 Worker Instances
```

If queue size increases → more workers launch.

Workers may run on:

* Amazon EC2
* AWS Lambda

---

# Monitoring Dead Letter Queue

Dead Letter Queues should also be monitored.

Example scenario:

```text
Main Queue → Worker
      │
      ▼
   Dead Letter Queue
```

If messages appear in DLQ:

* It indicates processing failures
* Developers need to investigate the issue

---

# Best Practices for Monitoring

Recommended monitoring practices:

* Track queue size regularly
* Monitor oldest message age
* Set CloudWatch alarms
* Monitor Dead Letter Queues
* Use auto scaling for workers

These ensure **high availability and reliability**.

---

# Real DevOps Monitoring Architecture

Production monitoring architecture:

```text
Application
     │
     ▼
  SQS Queue
     │
     ▼
Worker Instances
     │
     ▼
CloudWatch Metrics → Alerts → DevOps Team
```

This helps detect **performance issues early**.

---

# Interview Question

**How do you monitor Amazon SQS queues?**

Answer:

Amazon SQS queues are monitored using **Amazon CloudWatch**, which tracks metrics like queue length, message age, and processing activity. Alerts can be configured to notify teams or trigger auto scaling.

---
---
## 1.17 Amazon SQS vs Other Messaging Services

![Image](https://media2.dev.to/dynamic/image/width%3D800%2Cheight%3D%2Cfit%3Dscale-down%2Cgravity%3Dauto%2Cformat%3Dauto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fb5osbyu9grpfnvcy9psr.png)

![Image](https://betterdev.blog/_astro/aws-messaging-services-decision-tree.D63PXhMC_1uNHN.webp)

![Image](https://eda-visuals.boyney.io/assets/visuals/eda/queues-vs-streams-vs-pubsub.png)

![Image](https://substackcdn.com/image/fetch/%24s_%213jiz%21%2Cw_1456%2Cc_limit%2Cf_auto%2Cq_auto%3Agood%2Cfl_progressive%3Asteep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F81ccfded-9aa1-43fe-9888-aff03bc92b03_2250x2624.heic)

In cloud and distributed systems, there are multiple messaging technologies.
The most commonly compared services are:

* Amazon SQS
* Amazon SNS
* Apache Kafka
* RabbitMQ

Each service is designed for **different use cases**.

---

# 1. Amazon SQS

SQS is a **fully managed message queue service**.

Architecture:

```text
Producer → SQS Queue → Consumer
```

Messages are stored in a queue and processed **one by one by consumers**.

### Key Characteristics

* Fully managed by AWS
* Highly scalable
* Asynchronous communication
* Supports Standard and FIFO queues

### Best Use Cases

* Background jobs
* Microservices communication
* Order processing systems
* Task queues

---

# 2. Amazon SNS

SNS is a **publish-subscribe messaging service**.

Architecture:

```text
Publisher → SNS Topic → Multiple Subscribers
```

One message can be delivered to **multiple subscribers simultaneously**.

### Key Characteristics

* Pub/Sub messaging
* Event notifications
* Supports multiple protocols

Subscribers can be:

* Email
* SMS
* Lambda
* SQS queues
* HTTP endpoints

### Best Use Cases

* Application notifications
* Event broadcasting
* Alert systems

---

# 3. Apache Kafka

Apache Kafka is an **event streaming platform** designed for high-throughput data pipelines.

Architecture:

```text
Producer → Kafka Topic → Consumer Groups
```

Kafka stores **streams of events for real-time processing**.

### Key Characteristics

* Very high throughput
* Distributed event streaming
* Real-time data pipelines
* Long-term event storage

### Best Use Cases

* Real-time analytics
* Streaming data pipelines
* Log aggregation
* Event streaming systems

---

# 4. RabbitMQ

RabbitMQ is an **open-source message broker** widely used in microservices architectures.

Architecture:

```text
Producer → Exchange → Queue → Consumer
```

RabbitMQ uses **exchanges and routing rules** to deliver messages.

### Key Characteristics

* Flexible routing
* Open-source
* Supports multiple messaging patterns

### Best Use Cases

* Enterprise messaging systems
* Microservice communication
* Task queues

---

# Comparison Table

| Feature          | SQS           | SNS                  | Kafka                  | RabbitMQ             |
| ---------------- | ------------- | -------------------- | ---------------------- | -------------------- |
| Type             | Message Queue | Pub/Sub              | Event Streaming        | Message Broker       |
| Managed Service  | Yes           | Yes                  | Self-managed / Managed | Usually self-managed |
| Message Delivery | One consumer  | Multiple subscribers | Consumer groups        | Flexible routing     |
| Throughput       | High          | High                 | Extremely high         | Medium               |
| Complexity       | Simple        | Simple               | Complex                | Moderate             |

---

# Simple Way to Understand

| Service  | Purpose                             |
| -------- | ----------------------------------- |
| SQS      | Store tasks to process later        |
| SNS      | Send notifications to many services |
| Kafka    | Stream large volumes of data        |
| RabbitMQ | Flexible messaging broker           |

---

# Real Production Architecture

Example modern cloud architecture:

```text
Application
   │
   ▼
SNS Topic
   │
   ├── SQS Queue → Worker Service
   ├── Lambda Function → Processing
   └── Analytics System
```

Services used:

* Amazon SNS
* Amazon SQS
* AWS Lambda

---

# Interview Question

**What is the difference between SQS and SNS?**

Answer:

* **SQS** is a **message queue** where messages are stored and processed by consumers.
* **SNS** is a **publish-subscribe service** that sends messages to multiple subscribers simultaneously.

---
---
## 1.18 Amazon SQS Interview Questions (DevOps Q&A)

![Image](https://d2908q01vomqb2.cloudfront.net/fc074d501302eb2b93e2554793fcaf50b3bf7291/2025/01/29/Serverless-Retry-Mechanism-1-952x630.jpg)

![Image](https://d2908q01vomqb2.cloudfront.net/fc074d501302eb2b93e2554793fcaf50b3bf7291/2021/08/17/Fig1-queue-integration.png)

![Image](https://d2908q01vomqb2.cloudfront.net/fc074d501302eb2b93e2554793fcaf50b3bf7291/2025/02/24/archblog-1041-featurepng-1114x630.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2AFqb_Wi4qdERGFpNKNVjabw.png)

Below are **important DevOps interview questions and answers** related to **Amazon SQS**.

---

# 1. What is Amazon SQS?

**Answer**

Amazon SQS is a **fully managed message queue service** provided by Amazon Web Services that allows applications and microservices to **communicate asynchronously by sending and receiving messages through queues**.

---

# 2. Why is Amazon SQS used?

**Answer**

SQS is used to:

* Decouple applications
* Improve scalability
* Handle large workloads
* Enable asynchronous processing
* Build reliable distributed systems

---

# 3. What are the types of SQS queues?

**Answer**

Two types:

1. **Standard Queue**
2. **FIFO Queue (First-In-First-Out)**

---

# 4. What is the difference between Standard and FIFO queues?

| Feature            | Standard Queue     | FIFO Queue         |
| ------------------ | ------------------ | ------------------ |
| Message order      | Not guaranteed     | Guaranteed         |
| Throughput         | Very high          | Limited            |
| Duplicate messages | Possible           | Prevented          |
| Use case           | High-scale systems | Ordered processing |

---

# 5. What is Visibility Timeout?

**Answer**

Visibility timeout is the **time during which a message becomes invisible to other consumers after it is received by a consumer**.

This prevents multiple consumers from processing the same message simultaneously.

---

# 6. What is Message Retention Period?

**Answer**

Message retention period defines **how long a message stays in the queue before it is automatically deleted**.

Default: **4 days**
Maximum: **14 days**

---

# 7. What is a Dead Letter Queue (DLQ)?

**Answer**

A Dead Letter Queue stores **messages that fail processing multiple times**.

It helps developers **debug failed messages and prevent infinite retries**.

---

# 8. What is Long Polling?

**Answer**

Long polling allows a consumer to **wait for messages for up to 20 seconds** instead of receiving immediate empty responses.

Benefits:

* Fewer API requests
* Lower cost
* Faster message retrieval

---

# 9. What is Short Polling?

**Answer**

Short polling checks only a **subset of SQS servers** and immediately returns the response.

It may result in **empty responses even when messages exist**.

---

# 10. What are the main components of an SQS message?

**Answer**

An SQS message contains:

* Message Body
* Message Attributes
* Message ID
* Receipt Handle

---

# 11. What is the maximum message size in SQS?

**Answer**

Maximum message size:

**256 KB**

---

# 12. What is the maximum visibility timeout?

**Answer**

Maximum visibility timeout:

**12 hours**

---

# 13. How does SQS guarantee message durability?

**Answer**

SQS stores messages **across multiple servers and availability zones**, ensuring **high durability and reliability**.

---

# 14. What is at-least-once delivery?

**Answer**

At-least-once delivery means a message **may be delivered more than once**, so applications must handle **duplicate messages**.

---

# 15. What is idempotency in SQS?

**Answer**

Idempotency means the application can **process the same message multiple times without causing errors or duplicate results**.

---

# 16. How do you delete a message from SQS?

**Answer**

Messages are deleted using the **Receipt Handle** returned when the message is received.

---

# 17. Which AWS services integrate with SQS?

Common integrations:

* AWS Lambda
* Amazon EC2
* Amazon SNS
* Amazon S3
* Amazon CloudWatch

---

# 18. What is the fanout pattern?

**Answer**

The fanout pattern uses **SNS to send a message to multiple SQS queues simultaneously**.

Architecture:

```text
Application → SNS Topic
                    │
         ┌──────────┼──────────┐
         ▼          ▼          ▼
      SQS Q1     SQS Q2     SQS Q3
```

---

# 19. What is message batching?

**Answer**

Message batching allows sending or receiving **up to 10 messages per request**, reducing API calls and cost.

---

# 20. How is SQS pricing calculated?

**Answer**

SQS pricing is **request-based**.

You pay for:

* SendMessage
* ReceiveMessage
* DeleteMessage

AWS provides **1 million free requests per month**.

---

# 21. What happens if a message is not deleted?

**Answer**

If a message is not deleted:

* It becomes visible again after the **visibility timeout**
* Another consumer may process it

---

# 22. How do you monitor SQS?

**Answer**

SQS is monitored using **Amazon CloudWatch**, which tracks queue metrics such as message count and processing delays.

---

# 23. What is the difference between SQS and SNS?

| Feature          | SQS             | SNS                  |
| ---------------- | --------------- | -------------------- |
| Type             | Message Queue   | Pub/Sub              |
| Message delivery | One consumer    | Multiple subscribers |
| Use case         | Task processing | Notifications        |

---

# 24. What is the maximum number of messages in SQS?

**Answer**

SQS supports **unlimited messages** in a queue.

---

# 25. What is the maximum batch size?

**Answer**

Maximum batch size:

**10 messages per batch**

---

# 26. How does SQS help microservices?

**Answer**

SQS decouples services by **allowing them to communicate through queues instead of direct API calls**.

---

# 27. What is SQS FIFO deduplication?

**Answer**

FIFO queues prevent duplicate messages using **message deduplication IDs**.

---

# 28. What happens if a consumer crashes?

**Answer**

If the consumer crashes:

* Message is not deleted
* After visibility timeout expires
* Another consumer can process the message

---

# 29. What is SQS used for in real systems?

**Answer**

Common uses include:

* Order processing
* Background job processing
* Event-driven systems
* Log processing
* Microservices communication

---

# 30. What are SQS best practices?

**Answer**

Best practices include:

* Enable long polling
* Use dead letter queues
* Monitor with CloudWatch
* Delete messages after processing
* Configure proper visibility timeout

---
---
# 2. Amazon SNS (Simple Notification Service)
---

![Image](https://d2908q01vomqb2.cloudfront.net/1b6453892473a467d07372d45eb05abc2031647a/2017/11/20/introducing_sns_message_filtering_image_1.png)

![Image](https://docs.aws.amazon.com/images/sns/latest/dg/images/sns-delivery-protocols.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2A9z3sbaE6yGT1Ukau8iq4ew.png)

![Image](https://d2908q01vomqb2.cloudfront.net/1b6453892473a467d07372d45eb05abc2031647a/2017/07/25/messaging-fanout-for-serverless-with-sns-diagram2.png)

## 2.1 Introduction to Amazon SNS

**Amazon SNS** is a **fully managed publish/subscribe messaging service** provided by Amazon Web Services.

It allows applications to **send messages or notifications to multiple subscribers simultaneously**.

SNS is commonly used for **alerts, notifications, and event-driven architectures**.

---

# Simple Definition

**Amazon SNS is a messaging service used to send notifications to multiple systems or users at the same time.**

---

# Why Amazon SNS is Used

Applications often need to notify **multiple systems or users when an event occurs**.

Example:

When an order is created:

* Email notification
* SMS alert
* Inventory update
* Billing update

SNS can send the **same message to multiple subscribers**.

---

# Real-Life Example

Think of SNS like a **news broadcasting system**.

Example:

TV channel → broadcast news → millions of viewers receive it.

SNS works the same way:

```text
Publisher → SNS Topic → Multiple Subscribers
```

---

# Basic Components of SNS

### 1. Publisher

The service or application that **sends the message**.

Examples:

* Web applications
* Monitoring systems
* Cloud services

---

### 2. Topic

A **topic** is a communication channel where messages are sent.

Subscribers subscribe to this topic to receive notifications.

Example topic name:

```
order-notification-topic
```

---

### 3. Subscriber

Subscribers receive messages published to the topic.

Subscribers can be:

* Email
* SMS
* HTTP endpoint
* Lambda function
* SQS queue
* Mobile push notification

---

# SNS Workflow

Step-by-step:

1. Publisher sends message to SNS topic
2. SNS receives the message
3. SNS sends message to all subscribers
4. Subscribers process the message

---

# Example Architecture

```text
Application
     │
     ▼
  SNS Topic
     │
 ┌───┼────┬─────┐
 ▼   ▼    ▼     ▼
Email SMS Lambda SQS
```

---

# Example Use Case

Monitoring system alert.

If a server fails:

```text
CloudWatch Alert → SNS Topic → Email + SMS + Slack
```

Services used:

* Amazon SNS
* Amazon CloudWatch

---

# Key Characteristics of SNS

* Publish/Subscribe messaging
* Real-time notifications
* Scalable messaging system
* Integration with AWS services
* Supports multiple delivery protocols

---

# Important Point

SNS sends messages to **multiple subscribers simultaneously**, unlike **Amazon SQS**, which sends a message to **one consumer at a time**.

---

# Simple Comparison

| Feature          | SNS                  | SQS             |
| ---------------- | -------------------- | --------------- |
| Messaging type   | Publish/Subscribe    | Message Queue   |
| Message delivery | Multiple subscribers | One consumer    |
| Use case         | Notifications        | Task processing |

---
---
## 2.2 How Amazon SNS Works (Message Flow)

![Image](https://d2908q01vomqb2.cloudfront.net/1b6453892473a467d07372d45eb05abc2031647a/2017/11/20/introducing_sns_message_filtering_image_1.png)

![Image](https://docs.aws.amazon.com/images/sns/latest/dg/images/sns-delivery-protocols.png)

![Image](https://d2908q01vomqb2.cloudfront.net/fc074d501302eb2b93e2554793fcaf50b3bf7291/2023/02/13/adverse_1-1181x630.png)

In **Amazon SNS**, messages are delivered using a **Publish–Subscribe (Pub/Sub) model**.

This model allows **one publisher to send a message to multiple subscribers simultaneously**.

---

# SNS Message Flow Overview

Basic architecture:

```text
Publisher → SNS Topic → Subscribers
```

Subscribers can be:

* Email
* SMS
* HTTP/HTTPS endpoint
* Lambda
* SQS queues
* Mobile notifications

---

# Step-by-Step Working of Amazon SNS

## 1. Publisher Sends Message

A **publisher** sends a message to an SNS topic.

Publishers can be:

* Applications
* Monitoring systems
* AWS services

Example:

```text
Application → Publish Message → SNS Topic
```

---

## 2. SNS Topic Receives Message

The message is sent to an **SNS Topic**, which acts as the **communication channel**.

Example topic:

```text
order-events-topic
```

All subscribers attached to this topic will receive the message.

---

## 3. SNS Identifies Subscribers

SNS checks all **subscriptions linked to the topic**.

Subscribers may include:

* Email users
* SMS numbers
* SQS queues
* Lambda functions
* Webhooks

SNS prepares to send the message to each subscriber.

---

## 4. Message Delivered to Subscribers

SNS delivers the message to all subscribed endpoints.

Example architecture:

```text
Application
     │
     ▼
  SNS Topic
     │
 ┌───┼───────────┬───────────┐
 ▼   ▼           ▼           ▼
Email SMS      SQS Queue   Lambda
```

Each subscriber receives the **same message simultaneously**.

---

# Example Real Workflow

Example: **Server monitoring system**

Services used:

* Amazon CloudWatch
* Amazon SNS

Workflow:

```text
CloudWatch Alarm → SNS Topic → Email + SMS + Lambda
```

Steps:

1. Server CPU usage exceeds limit
2. CloudWatch alarm triggers
3. Alarm sends message to SNS
4. SNS sends notifications to subscribers

---

# Example Message

Example message published to SNS:

```json
{
 "event": "server_alert",
 "instance_id": "i-12345",
 "cpu_usage": "90%"
}
```

This message will be delivered to **all subscribers**.

---

# Important SNS Characteristics

* Messages are **pushed to subscribers automatically**
* Supports multiple delivery protocols
* Highly scalable
* Real-time notification system

---

# SNS vs SQS Message Flow

| Feature              | SNS                  | SQS          |
| -------------------- | -------------------- | ------------ |
| Delivery model       | Push                 | Poll         |
| Message distribution | Multiple subscribers | One consumer |
| Communication type   | Pub/Sub              | Queue-based  |

---

# DevOps Architecture Example

Modern cloud architecture often combines:

* Amazon SNS
* Amazon SQS

Example:

```text
Application → SNS Topic
                │
        ┌───────┼────────┐
        ▼       ▼        ▼
      SQS      SQS      Lambda
```

This pattern is called **Fanout Architecture**.

---

# Interview Question

**How does Amazon SNS deliver messages?**

Answer:

Amazon SNS uses a **publish-subscribe model**, where publishers send messages to a topic, and SNS delivers those messages to all subscribed endpoints.

---
---
## 2.3 Amazon SNS Components

![Image](https://docs.aws.amazon.com/images/sns/latest/dg/images/sns-delivery-protocols.png)

![Image](https://d2908q01vomqb2.cloudfront.net/1b6453892473a467d07372d45eb05abc2031647a/2017/11/20/introducing_sns_message_filtering_image_1.png)

![Image](https://docs.aws.amazon.com/images/prescriptive-guidance/latest/cloud-design-patterns/images/publish-subscribe-1.png)

![Image](https://media.beehiiv.com/cdn-cgi/image/fit%3Dscale-down%2Cquality%3D80%2Cformat%3Dauto%2Conerror%3Dredirect/uploads/asset/file/dae07cda-9ec2-4c44-a138-dc09e13c82ea/image.png)

In **Amazon SNS**, the messaging system is built using several important components.

The **four main components** of SNS are:

1. Publisher
2. Topic
3. Subscriber
4. Endpoint

These components work together to **deliver messages to multiple systems or users**.

---

# 1. Publisher

A **publisher** is the system or application that **sends messages to an SNS topic**.

Publishers generate events or notifications.

### Examples of publishers

* Web applications
* Monitoring services
* Cloud applications
* AWS services

Example architecture:

```text
Application → Publish Message → SNS Topic
```

Example AWS service acting as publisher:

* Amazon CloudWatch

CloudWatch can send alerts to SNS when a system issue occurs.

---

# 2. Topic

A **Topic** is the **communication channel** in SNS.

Publishers send messages to a topic, and SNS distributes those messages to all subscribers.

Example topic name:

```text
order-notification-topic
```

Workflow:

```text
Publisher → SNS Topic → Subscribers
```

A topic can have **multiple subscribers**.

---

# 3. Subscriber

A **subscriber** is a system or user that **receives messages from the SNS topic**.

Subscribers register themselves to receive notifications.

Example architecture:

```text
SNS Topic → Subscribers
```

Subscribers can include:

* Email users
* SMS recipients
* Web services
* Applications
* Message queues

---

# 4. Endpoint

An **endpoint** is the **destination where SNS sends the message**.

Examples of endpoints:

| Endpoint Type | Description                       |
| ------------- | --------------------------------- |
| Email         | Send notification emails          |
| SMS           | Send text messages                |
| HTTP/HTTPS    | Send messages to web services     |
| Lambda        | Trigger serverless functions      |
| SQS           | Send messages to message queues   |
| Mobile push   | Send notifications to mobile apps |

Example architecture:

```text
SNS Topic
   │
   ├── Email Endpoint
   ├── SMS Endpoint
   ├── Lambda Endpoint
   └── SQS Endpoint
```

Services commonly used with SNS:

* AWS Lambda
* Amazon SQS

---

# Complete SNS Workflow

Complete messaging flow:

```text
Publisher
   │
   ▼
SNS Topic
   │
   ├── Subscriber (Email)
   ├── Subscriber (SMS)
   ├── Subscriber (Lambda)
   └── Subscriber (SQS)
```

Each subscriber receives the **same message simultaneously**.

---

# Real Production Example

Example system alert architecture:

```text
CloudWatch Alarm
      │
      ▼
   SNS Topic
      │
 ┌────┼─────┬─────┐
 ▼    ▼     ▼     ▼
Email SMS Lambda SQS
```

Services involved:

* Amazon CloudWatch
* Amazon SNS

---

# Simple Summary

| Component  | Purpose                    |
| ---------- | -------------------------- |
| Publisher  | Sends messages             |
| Topic      | Communication channel      |
| Subscriber | Receives messages          |
| Endpoint   | Destination of the message |

---

# Interview Question

**What are the main components of Amazon SNS?**

Answer:

The main components are:

* Publisher
* Topic
* Subscriber
* Endpoint

---
---
## 2.4 SNS Supported Endpoints

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/0%2Am4g0wju6GxgvbLSp.png)

![Image](https://docs.aws.amazon.com/images/sns/latest/dg/images/sns-delivery-protocols.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2AkADDlMRBoE717nR-mlf6-g.png)

![Image](https://d2908q01vomqb2.cloudfront.net/1b6453892473a467d07372d45eb05abc2031647a/2023/05/10/ComputeBlog-1786-1.png)

In **Amazon SNS**, an **endpoint** is the destination where a notification message is delivered.

SNS supports **multiple endpoint types**, allowing notifications to be sent to **applications, users, or services**.

This flexibility makes SNS ideal for **notification systems and event-driven architectures**.

---

# Common SNS Endpoint Types

## 1. Email

SNS can send **email notifications** to subscribers.

Example:

```text
SNS Topic → Email Notification
```

Use cases:

* System alerts
* Order confirmations
* Application notifications

Subscribers must **confirm the subscription** before receiving messages.

---

# 2. SMS (Text Messages)

SNS can send notifications directly to **mobile phones via SMS**.

Example workflow:

```text
SNS Topic → SMS → Mobile Phone
```

Use cases:

* OTP messages
* Critical alerts
* Security notifications

Example message:

```
Server CPU usage exceeded 90%
```

---

# 3. HTTP / HTTPS Endpoint

SNS can send messages to **web applications using HTTP or HTTPS requests**.

Example architecture:

```text
SNS Topic → HTTPS Endpoint → Web Application
```

Use cases:

* Webhook integrations
* Third-party API notifications
* Real-time event processing

Example:

A payment service receives notifications from SNS via HTTP API.

---

# 4. AWS Lambda

SNS can trigger **serverless functions** using:

AWS Lambda

Example architecture:

```text
SNS Topic → Lambda Function → Process Event
```

Use cases:

* Data processing
* Event automation
* Log analysis

Example event:

```json
{
 "event": "file_upload",
 "file": "image.png"
}
```

Lambda processes the event automatically.

---

# 5. Amazon SQS

SNS can send messages to **message queues** using:

Amazon SQS

Example architecture:

```text
Application → SNS Topic → SQS Queue → Worker
```

This pattern is called the **Fanout Pattern**.

Benefits:

* Reliable message delivery
* Asynchronous processing
* Microservices communication

---

# 6. Mobile Push Notifications

SNS can send push notifications to **mobile applications**.

Supported platforms include:

* Android
* iOS
* Fire OS devices

Example workflow:

```text
SNS Topic → Mobile App → Push Notification
```

Use cases:

* App alerts
* Marketing notifications
* User activity updates

---

# SNS Endpoint Architecture Example

Example production architecture:

```text
Application
   │
   ▼
SNS Topic
   │
 ┌─┼─────────────┬───────────────┬───────────┐
 ▼ ▼             ▼               ▼           ▼
Email SMS      Lambda          SQS        HTTP
```

Each endpoint receives the **same message simultaneously**.

---

# Benefits of Multiple Endpoints

Advantages of SNS endpoint flexibility:

* Send notifications to multiple systems
* Integrate with cloud services
* Support real-time communication
* Build scalable event-driven systems

---

# Interview Question

**What types of endpoints does Amazon SNS support?**

Answer:

Amazon SNS supports several endpoint types including:

* Email
* SMS
* HTTP/HTTPS
* AWS Lambda
* Amazon SQS
* Mobile push notifications

---
---
## 2.5 SNS Message Flow (Publish → Topic → Subscribers)

![Image](https://d2908q01vomqb2.cloudfront.net/1b6453892473a467d07372d45eb05abc2031647a/2017/11/20/introducing_sns_message_filtering_image_1.png)

![Image](https://docs.aws.amazon.com/images/prescriptive-guidance/latest/cloud-design-patterns/images/publish-subscribe-1.png)

![Image](https://docs.aws.amazon.com/images/sns/latest/dg/images/sns-delivery-protocols.png)

![Image](https://docs.aws.amazon.com/images/sns/latest/dg/images/sns-mobile-push-notifications.png)

In **Amazon SNS**, messages are delivered using the **Publish–Subscribe (Pub/Sub) model**.

The message flow follows a simple path:

**Publisher → Topic → Subscribers**

This model allows **one message to be delivered to many subscribers at the same time**.

---

# SNS Message Flow Overview

Basic architecture:

```text
Publisher → SNS Topic → Multiple Subscribers
```

Subscribers can be:

* Email
* SMS
* HTTP endpoint
* Lambda
* SQS queues
* Mobile applications

---

# Step-by-Step SNS Message Flow

## 1. Publisher Sends Message

A **publisher** sends a message to an SNS topic.

Publishers can be:

* Applications
* Monitoring systems
* AWS services

Example:

```text
Application → Publish Message → SNS Topic
```

Example AWS service publisher:

* Amazon CloudWatch

CloudWatch can send alerts to SNS topics.

---

# 2. SNS Topic Receives Message

The message is received by the **SNS topic**.

A topic acts as a **communication channel**.

Example topic:

```text
server-alert-topic
```

All subscribers attached to the topic will receive the message.

---

# 3. SNS Identifies Subscribers

SNS checks all **subscriptions connected to the topic**.

Subscribers may include:

* Email addresses
* SMS numbers
* Lambda functions
* SQS queues
* HTTP endpoints

SNS prepares to send the message to each subscriber.

---

# 4. Message Delivered to Subscribers

SNS delivers the message to **all subscribers simultaneously**.

Example architecture:

```text
SNS Topic
   │
 ┌─┼───────────┬───────────┬──────────┐
 ▼ ▼           ▼           ▼          ▼
Email SMS     Lambda      SQS       HTTP
```

Each subscriber receives the **same message**.

---

# Example Real Workflow

Example: **Server monitoring alert**

Services used:

* Amazon CloudWatch
* Amazon SNS

Workflow:

```text
CloudWatch Alarm → SNS Topic → Email + SMS + Lambda
```

Steps:

1. Server CPU usage crosses threshold
2. CloudWatch alarm triggers
3. Alarm sends message to SNS
4. SNS sends notifications to subscribers

---

# Example Message

Example message published to SNS:

```json
{
 "event": "server_alert",
 "instance_id": "i-123456",
 "cpu_usage": "95%"
}
```

This message will be delivered to **all subscribers of the topic**.

---

# SNS Push-Based Messaging

SNS uses **push delivery**.

This means:

* SNS automatically sends messages to subscribers
* Subscribers do not need to request messages

This is different from **Amazon SQS**, where consumers must **poll the queue**.

---

# DevOps Architecture Example

Many real architectures combine SNS and SQS.

Example:

```text
Application → SNS Topic
                │
        ┌───────┼────────┐
        ▼       ▼        ▼
      SQS      SQS      Lambda
```

This pattern is called **Fanout Architecture**.

---

# Interview Question

**Explain the message flow of Amazon SNS.**

Answer:

Amazon SNS follows the **Publish–Subscribe model**, where publishers send messages to a topic, and SNS distributes those messages to all subscribed endpoints.

---
---
## 2.6 SNS Fanout Pattern (SNS → Multiple SQS Queues)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2A9z3sbaE6yGT1Ukau8iq4ew.png)

![Image](https://d2908q01vomqb2.cloudfront.net/1b6453892473a467d07372d45eb05abc2031647a/2017/07/25/messaging-fanout-for-serverless-with-sns-diagram2.png)

![Image](https://miro.medium.com/1%2A9i7kLcChRnlvmcbjo9MXUA.png)

![Image](https://cms.cloudoptimo.com/uploads/Understanding_AWS_SQS_and_SNS_7880c41627.png)

The **Fanout Pattern** is a common architecture pattern using **Amazon SNS** and **Amazon SQS**.

It allows **one message to be delivered to multiple SQS queues simultaneously**.

This pattern is widely used in **microservices architectures and event-driven systems**.

---

# What is the Fanout Pattern?

The Fanout Pattern distributes a **single message to multiple consumers**.

Architecture:

```text
Publisher → SNS Topic → Multiple SQS Queues
```

Each queue receives a **copy of the same message**.

Each service processes the message independently.

---

# Why Fanout Pattern is Used

Applications often need to trigger **multiple services from one event**.

Example event:

**Order Created**

Systems that must process the event:

* Inventory system
* Payment system
* Shipping system
* Analytics system

Fanout architecture allows all systems to receive the event **simultaneously**.

---

# Fanout Architecture

Example architecture:

```text
Application
   │
   ▼
SNS Topic
   │
 ┌─┼───────────┬───────────┐
 ▼ ▼           ▼           ▼
SQS Queue 1  SQS Queue 2  SQS Queue 3
Inventory   Billing      Shipping
```

Each queue processes the event **independently**.

---

# Example Workflow

Step-by-step process:

1. Application publishes message to SNS topic

2. SNS receives the message

3. SNS sends the message to all subscribed SQS queues

4. Each service processes the message independently

---

# Example Message

Example event message:

```json
{
 "event": "order_created",
 "order_id": "12345",
 "customer": "John"
}
```

SNS sends this message to **all subscribed SQS queues**.

---

# Real Production Example

Example **e-commerce system**.

Architecture:

```text
Order Service
     │
     ▼
   SNS Topic
     │
 ┌───┼────────────┬───────────────┐
 ▼   ▼            ▼               ▼
Inventory Queue  Billing Queue  Shipping Queue
```

Each system processes the order independently.

---

# Benefits of Fanout Pattern

Advantages:

* Decouples microservices
* Scalable architecture
* Reliable event distribution
* Independent service processing
* Easy system expansion

For example, adding a new service:

```text
SNS Topic → New SQS Queue → New Microservice
```

No changes required in the publisher.

---

# Fanout vs Traditional Architecture

Without fanout:

```text
Application → Inventory Service
Application → Billing Service
Application → Shipping Service
```

Many direct integrations.

With fanout:

```text
Application → SNS Topic → Multiple Services
```

Simpler architecture.

---

# Real DevOps Architecture

Modern event-driven architecture:

```text
Application
   │
   ▼
SNS Topic
   │
 ┌─┼─────────────┬──────────────┬──────────────┐
 ▼ ▼             ▼              ▼              ▼
SQS Queue      Lambda        Analytics      Notification
```

Services used:

* Amazon SNS
* Amazon SQS
* AWS Lambda

---

# Interview Question

**What is the SNS Fanout Pattern?**

Answer:

The SNS Fanout Pattern is an architecture where **a message published to an SNS topic is delivered to multiple SQS queues**, allowing multiple services to process the same event independently.

---
---
## 2.7 SNS Message Filtering

![Image](https://d2908q01vomqb2.cloudfront.net/1b6453892473a467d07372d45eb05abc2031647a/2022/11/21/Payload-filtering-example.png)

![Image](https://d2908q01vomqb2.cloudfront.net/1b6453892473a467d07372d45eb05abc2031647a/2022/11/22/Payload-filtering-example3.png)

![Image](https://d2908q01vomqb2.cloudfront.net/1b6453892473a467d07372d45eb05abc2031647a/2018/08/14/Architecture-SNS-with-Cloudformation-1.png)

![Image](https://d2908q01vomqb2.cloudfront.net/1b6453892473a467d07372d45eb05abc2031647a/2017/11/20/introducing_sns_message_filtering_image_3.png)

**Message Filtering** in **Amazon SNS** allows you to **deliver messages only to specific subscribers based on message attributes**.

Instead of sending every message to all subscribers, SNS can **filter messages and send them only to relevant subscribers**.

This improves **efficiency and reduces unnecessary processing**.

---

# Why Message Filtering is Needed

In large systems, different services may only need **specific types of messages**.

Example:

Event types:

* Order Created
* Order Cancelled
* Payment Completed

Without filtering:

```text
SNS Topic → All messages → All queues
```

All queues receive **every message**, even if they don't need it.

With filtering:

```text
SNS Topic → Filter messages → Relevant queues
```

Each queue receives **only relevant messages**.

---

# Example Architecture

```text
Application
   │
   ▼
SNS Topic
   │
 ┌─┼─────────────┬─────────────┐
 ▼ ▼             ▼             ▼
SQS Queue 1    SQS Queue 2   SQS Queue 3
Orders         Payments      Shipping
```

Each queue subscribes with **filter rules**.

---

# Example Message with Attributes

Example message published to SNS:

```json
{
 "event": "order_created",
 "order_id": "12345"
}
```

Message attributes:

```json
{
 "event_type": "order"
}
```

SNS checks these attributes to decide **which subscribers receive the message**.

---

# Example Filter Policy

Example subscription filter policy:

```json
{
 "event_type": ["order"]
}
```

This subscriber will receive **only order-related messages**.

---

# Example Filtering Scenario

System events:

| Event             | Subscriber       |
| ----------------- | ---------------- |
| Order Created     | Order Service    |
| Payment Completed | Payment Service  |
| Shipping Started  | Shipping Service |

Architecture:

```text
Application → SNS Topic
                  │
        ┌─────────┼─────────┐
        ▼         ▼         ▼
   Order Queue  Payment Queue Shipping Queue
```

Each queue receives **only relevant messages**.

---

# Benefits of Message Filtering

Advantages:

* Reduces unnecessary message processing
* Improves system performance
* Simplifies microservice communication
* Reduces infrastructure cost

This is very useful in **large event-driven architectures**.

---

# Real DevOps Example

Example architecture:

```text
Application
   │
   ▼
SNS Topic
   │
 ┌─┼────────────┬────────────┬─────────────┐
 ▼ ▼            ▼            ▼
Order Queue   Payment Queue Shipping Queue
```

Services used:

* Amazon SNS
* Amazon SQS

Each queue processes **only the events it needs**.

---

# Interview Question

**What is SNS Message Filtering?**

Answer:

SNS message filtering allows subscribers to **receive only specific messages based on message attributes**, reducing unnecessary message delivery.

---
---
## 2.8 SNS Security (IAM, Policies, Encryption)

![Image](https://d2908q01vomqb2.cloudfront.net/1b6453892473a467d07372d45eb05abc2031647a/2018/11/15/SNS-AWS-KMS.png)

![Image](https://docs.aws.amazon.com/images/sns/latest/dg/images/AccessPolicyLanguage_Arch_Overview.gif)

![Image](https://d2908q01vomqb2.cloudfront.net/22d200f8670dbdb3e253a90eee5098477c95c23d/2022/05/24/image1-2.png)

![Image](https://d2908q01vomqb2.cloudfront.net/b6692ea5df920cad691c20319a6fffd7a4a766b8/2017/03/31/encrypt_decrypt_1_1_1.gif)

Security is very important when using **Amazon SNS** in production systems.

SNS provides several security mechanisms to ensure that **only authorized users and services can publish or receive messages**.

Main security mechanisms include:

1. IAM Policies
2. SNS Topic Policies
3. Encryption with KMS
4. Network Security

---

# 1. IAM (Identity and Access Management)

Access to SNS resources is controlled using:

AWS Identity and Access Management

IAM allows you to control:

* Who can create SNS topics
* Who can publish messages
* Who can subscribe to topics
* Who can manage subscriptions

### Example IAM Policy

```json
{
 "Effect": "Allow",
 "Action": [
   "sns:Publish",
   "sns:Subscribe",
   "sns:CreateTopic"
 ],
 "Resource": "*"
}
```

This policy allows a user to **publish and subscribe to SNS topics**.

---

# 2. SNS Topic Policies

SNS supports **resource-based policies** called **Topic Policies**.

These policies define **which services or accounts can publish messages to a topic**.

Example use case:

Allow **Amazon S3** to send notifications to an SNS topic.

Architecture:

```text
S3 Bucket → SNS Topic
```

This is commonly used in **event-driven architectures**.

---

# 3. Encryption with KMS

SNS supports **server-side encryption** to protect sensitive data.

Encryption is handled using:

AWS Key Management Service

Encryption protects:

* Message content
* Sensitive business data
* Application events

Example architecture:

```text
Application → SNS Topic
                │
                ▼
           Encryption (KMS)
                │
                ▼
            Subscribers
```

This ensures messages remain **secure during processing**.

---

# 4. Network Security

SNS can be accessed securely within AWS environments.

Security options include:

* VPC endpoints
* Private network communication
* Secure HTTPS connections

Example architecture:

```text
Application (VPC)
      │
      ▼
   VPC Endpoint
      │
      ▼
   SNS Topic
```

This prevents exposure to the **public internet**.

---

# Monitoring SNS Security

SNS activities can be monitored using:

* Amazon CloudWatch
* AWS CloudTrail

These services help track:

* Topic access
* Message publishing
* Subscription changes

---

# SNS Security Best Practices

Recommended practices:

* Use **IAM roles instead of access keys**
* Enable **encryption with KMS**
* Restrict topic access using **least privilege principle**
* Monitor activity with CloudTrail
* Use HTTPS endpoints for secure communication

---

# Real DevOps Security Architecture

Example secure architecture:

```text
Application
     │
     ▼
IAM Role
     │
     ▼
SNS Topic
     │
Encryption (KMS)
     │
     ▼
Subscribers
```

This ensures **authentication, authorization, and encryption**.

---

# Interview Question

**How do you secure Amazon SNS?**

Answer:

SNS security is implemented using:

* IAM policies
* SNS topic policies
* Encryption with AWS KMS
* Network security using VPC endpoints

---
---
## 2.9 Amazon SNS Pricing Model

![Image](https://docs.aws.amazon.com/images/sns/latest/dg/images/sns-delivery-protocols.png)

![Image](https://docs.aws.amazon.com/images/sns/latest/dg/images/sns-sms-end-user-messaging.png)

![Image](https://cdn.prod.website-files.com/655bc1860a87f22da98dd83c/6754a8d7ed2239560fb628ed_6754a882cd877e6511aa3846_publish-subscribe-4%2520%281%29.png)

The pricing of **Amazon SNS** is based mainly on **number of requests and message deliveries**.

SNS is considered **cost-effective** because you only pay for what you use.

---

# 1. Free Tier

AWS provides a **free usage tier** for SNS.

Typical free usage per month includes:

* **1 million SNS publishes**
* **100,000 HTTP/HTTPS deliveries**
* **1,000 email notifications**

This free tier is useful for:

* Learning AWS
* Small applications
* Testing environments

---

# 2. Publish Requests

SNS charges based on **publish requests**.

A publish request happens when a publisher sends a message to an SNS topic.

Example:

```text
Application → SNS Topic
```

Each message published to a topic counts as **one request**.

Example:

```text
1 million messages published → 1 million publish requests
```

---

# 3. Message Delivery Charges

SNS also charges based on **message deliveries to subscribers**.

Example architecture:

```text
Application → SNS Topic → Email + Lambda + SQS
```

If one message is delivered to **three subscribers**, it counts as **three deliveries**.

Example calculation:

| Event              | Count |
| ------------------ | ----- |
| Publish message    | 1     |
| Delivery to Email  | 1     |
| Delivery to SQS    | 1     |
| Delivery to Lambda | 1     |

Total billable actions: **4**

---

# 4. SMS Notification Cost

Sending SMS messages using SNS has **additional charges**.

Example architecture:

```text
SNS Topic → SMS → Mobile Phone
```

SMS pricing depends on:

* Destination country
* Message length
* Telecom provider

SMS notifications are usually used for:

* OTP verification
* Security alerts
* Critical notifications

---

# 5. Email Notifications

SNS can send **email notifications**.

Architecture:

```text
SNS Topic → Email
```

Email notifications are **very low cost** and often used for:

* System alerts
* Monitoring notifications
* Application events

---

# 6. Data Transfer Cost

If SNS communicates with AWS services in the **same region**, data transfer is usually **free**.

Example architecture:

```text
Application → SNS → SQS → Lambda
```

Services involved:

* Amazon SNS
* Amazon SQS
* AWS Lambda

Since they run in the same region, **no extra transfer cost**.

---

# Example Cost Calculation

Example system sending **1 million notifications**.

Architecture:

```text
Application → SNS Topic → Email + SQS
```

Calculation:

| Action            | Count     |
| ----------------- | --------- |
| Publish requests  | 1,000,000 |
| Delivery to Email | 1,000,000 |
| Delivery to SQS   | 1,000,000 |

Total message deliveries: **2,000,000**

Charges apply only after the **free tier limit**.

---

# Why SNS is Cost Efficient

Benefits:

* Pay only for requests and deliveries
* No server management
* Scales automatically
* Suitable for event-driven architectures

---

# DevOps Cost Optimization Tips

Best practices:

* Avoid unnecessary message deliveries
* Use **message filtering**
* Reduce SMS usage if possible
* Use SQS subscribers for processing tasks

These reduce **SNS operational costs**.

---

# Interview Question

**How is Amazon SNS pricing calculated?**

Answer:

Amazon SNS pricing is based on:

* Number of **publish requests**
* Number of **message deliveries**
* **SMS notifications** (if used)

---
---
## 2.10 SNS Integration with AWS Services

![Image](https://miro.medium.com/v2/resize%3Afit%3A1200/1%2AiBucptWLtkkr9QJano41pg.png)

![Image](https://d2908q01vomqb2.cloudfront.net/fc074d501302eb2b93e2554793fcaf50b3bf7291/2021/02/01/Arch-Diagram2.jpg)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2A9z3sbaE6yGT1Ukau8iq4ew.png)

![Image](https://d2908q01vomqb2.cloudfront.net/fc074d501302eb2b93e2554793fcaf50b3bf7291/2024/08/20/fig5-wesfarmers-queue-1024x482.png)

**Amazon SNS** integrates with many services in **Amazon Web Services** to build **event-driven architectures**.

These integrations allow applications to **automatically react to events and trigger workflows**.

Below are the most common SNS integrations used in real cloud systems.

---

# 1. SNS + Amazon SQS

SNS can send messages to **Amazon SQS** queues.

This pattern is called the **Fanout Pattern**.

### Architecture

```text
Application → SNS Topic
                  │
        ┌─────────┼─────────┐
        ▼         ▼         ▼
     SQS Queue 1 SQS Queue 2 SQS Queue 3
```

### Use Cases

* Microservices communication
* Order processing systems
* Event-driven architectures

Each queue processes the message independently.

---

# 2. SNS + AWS Lambda

SNS can trigger **AWS Lambda** functions automatically.

### Architecture

```text
Application → SNS Topic → Lambda Function
```

### Workflow

1. Event occurs
2. SNS publishes message
3. Lambda function is triggered
4. Lambda processes the event

### Use Cases

* Data processing
* Automation workflows
* Event-driven applications

---

# 3. SNS + Amazon CloudWatch

SNS is commonly used with **Amazon CloudWatch** to send alerts.

### Architecture

```text
CloudWatch Alarm → SNS Topic → Email / SMS
```

### Example

If CPU usage exceeds 80%:

* CloudWatch alarm triggers
* SNS sends alert notification

---

# 4. SNS + Amazon S3

Amazon S3 can send notifications to SNS when events occur.

### Architecture

```text
S3 Bucket → SNS Topic → Subscribers
```

Example events:

* File upload
* File deletion
* File modification

### Use Cases

* Image processing pipelines
* Data ingestion workflows

---

# 5. SNS + Amazon EC2

Applications running on **Amazon EC2** can publish messages to SNS topics.

### Architecture

```text
EC2 Application → SNS Topic → Notifications
```

### Example

A server monitoring script running on EC2 sends alerts to SNS when:

* Disk usage exceeds limit
* Server becomes unavailable

---

# 6. SNS + Mobile Applications

SNS can send **push notifications to mobile apps**.

Supported platforms:

* Android
* iOS
* Fire OS

### Architecture

```text
Application → SNS Topic → Mobile Push Notification
```

### Use Cases

* App alerts
* Marketing notifications
* User engagement messages

---

# Example Real DevOps Architecture

Typical event-driven architecture:

```text
Application
   │
   ▼
SNS Topic
   │
 ┌─┼──────────────┬──────────────┬─────────────┐
 ▼ ▼              ▼              ▼             ▼
SQS Queue       Lambda        Email         Mobile App
```

Services used:

* Amazon SNS
* Amazon SQS
* AWS Lambda
* Amazon CloudWatch

---

# Benefits of SNS Integration

Advantages:

* Enables event-driven architectures
* Decouples applications
* Automates workflows
* Supports scalable cloud systems

---

# Interview Question

**Which AWS services integrate with Amazon SNS?**

Answer:

Common SNS integrations include:

* Amazon SQS
* AWS Lambda
* Amazon CloudWatch
* Amazon S3
* Amazon EC2

---
---
## 2.11 Real-World Use Cases of Amazon SNS

![Image](https://media2.dev.to/dynamic/image/width%3D800%2Cheight%3D%2Cfit%3Dscale-down%2Cgravity%3Dauto%2Cformat%3Dauto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2F67clr4vrb55yjdqdyufs.png)

![Image](https://d2908q01vomqb2.cloudfront.net/1b6453892473a467d07372d45eb05abc2031647a/2017/11/16/event_driven_sns_compute_slide01.png)

![Image](https://cdn.prod.website-files.com/655bc1860a87f22da98dd83c/6754a8d7ed2239560fb628ed_6754a882cd877e6511aa3846_publish-subscribe-4%2520%281%29.png)

![Image](https://d2908q01vomqb2.cloudfront.net/972a67c48192728a34979d9a35164c1295401b71/2022/01/21/fig1sf.png)

**Amazon SNS** is widely used in modern cloud architectures to **send notifications, trigger events, and distribute messages to multiple systems**.

Below are some **real-world production use cases**.

---

# 1. System Monitoring Alerts

SNS is commonly used with **Amazon CloudWatch** to send alerts when system metrics exceed thresholds.

### Architecture

```text
CloudWatch Alarm → SNS Topic → Email / SMS
```

### Example

If server CPU usage exceeds **90%**:

1. CloudWatch alarm triggers
2. SNS topic receives alert
3. SNS sends notification to administrators

Use cases:

* Server failure alerts
* High CPU usage alerts
* Application errors

---

# 2. Application Notifications

SNS can send notifications to users about application events.

### Architecture

```text
Application → SNS Topic → Email / SMS
```

### Examples

* Order confirmation emails
* Password reset notifications
* Account activity alerts

This helps applications **notify users in real time**.

---

# 3. Microservices Communication

SNS is widely used in **microservices architectures**.

### Architecture

```text
Application → SNS Topic → Multiple Services
```

Example system:

```text
Order Service
     │
     ▼
   SNS Topic
     │
 ┌───┼────────────┬───────────────┐
 ▼   ▼            ▼               ▼
Inventory       Billing         Shipping
```

Each microservice receives the event independently.

---

# 4. Event-Driven Architectures

SNS is used to trigger workflows automatically when events occur.

Example architecture:

```text
Application → SNS Topic → Lambda Function
```

Services involved:

* AWS Lambda
* Amazon SNS

Example event:

```json
{
 "event": "file_uploaded",
 "file_name": "image.jpg"
}
```

SNS triggers Lambda to process the file.

---

# 5. Fanout Messaging Systems

SNS can distribute a single message to **multiple SQS queues**.

Architecture:

```text
Application → SNS Topic
                │
        ┌───────┼────────┐
        ▼       ▼        ▼
      SQS      SQS      SQS
```

Services used:

* Amazon SQS

Each queue processes the event independently.

---

# 6. Mobile Push Notifications

SNS can send notifications to **mobile applications**.

Architecture:

```text
Application → SNS Topic → Mobile App
```

Use cases:

* App updates
* Promotional notifications
* Security alerts

---

# 7. Data Processing Pipelines

SNS can trigger processing workflows.

Architecture:

```text
Data Producer → SNS Topic → Lambda → Data Processing
```

Example uses:

* Image processing pipelines
* Data ingestion workflows
* Log analysis systems

---

# Example Production Architecture

Typical cloud architecture using SNS:

```text
Application
   │
   ▼
SNS Topic
   │
 ┌─┼──────────────┬──────────────┬─────────────┐
 ▼ ▼              ▼              ▼             ▼
Email           Lambda         SQS          Mobile
```

Services used:

* Amazon SNS
* Amazon SQS
* AWS Lambda
* Amazon CloudWatch

---

# Why Companies Use SNS

Benefits:

* Real-time notifications
* Event-driven architecture
* Scalable messaging system
* Integration with many AWS services
* Reliable message delivery

---

# Interview Question

**Give some real-world use cases of Amazon SNS.**

Answer:

Amazon SNS is used for:

* System monitoring alerts
* Application notifications
* Microservices communication
* Event-driven architectures
* Mobile push notifications
* Fanout messaging systems

---
---
## 2.12 Amazon SNS Hands-on Practical Guide

![Image](https://docs.aws.amazon.com/images/sns/latest/dg/images/sns-delivery-protocols.png)

![Image](https://media.tutorialsdojo.com/public/td-pc-sns-email-json-110724-steps-image-7.png)

![Image](https://editor.analyticsvidhya.com/uploads/92104diagram-how-sns-works-wazuh.png)

![Image](https://d2908q01vomqb2.cloudfront.net/da4b9237bacccdf19c0760cab7aec4a8359010b0/2020/07/07/sns_fifo_two_subscriptions.png)

This section shows a **simple practical example** of using **Amazon SNS**.

We will perform these steps:

1. Create an SNS Topic
2. Create a Subscription
3. Publish a Message
4. Receive the Notification

This is the **basic workflow used in real applications**.

---

# 1. Create an SNS Topic

Steps:

1. Login to **AWS Management Console**
2. Open **SNS Service**
3. Click **Create topic**

Select type:

* **Standard** (most commonly used)
* **FIFO**

Example configuration:

| Setting    | Value                    |
| ---------- | ------------------------ |
| Topic Name | order-notification-topic |
| Type       | Standard                 |

Click **Create topic**.

Now the SNS topic is ready.

---

# 2. Create a Subscription

Subscribers receive messages from the topic.

Steps:

1. Open the created SNS topic
2. Click **Create subscription**

Example configuration:

| Setting  | Value                                       |
| -------- | ------------------------------------------- |
| Protocol | Email                                       |
| Endpoint | [user@example.com](mailto:user@example.com) |

After creating the subscription:

* AWS sends a **confirmation email**
* User must **confirm the subscription**

Only after confirmation will messages be delivered.

---

# 3. Publish a Message

Now publish a message to the SNS topic.

Steps:

1. Open the SNS topic
2. Click **Publish message**

Example message:

```json
{
 "event": "order_created",
 "order_id": "1001",
 "product": "Laptop"
}
```

Click **Publish message**.

SNS immediately sends the message to all subscribers.

---

# 4. Receive the Notification

Subscribers receive the message.

Example email notification:

```
Subject: Order Notification

Message:
Order 1001 has been created successfully.
```

If multiple subscribers exist, all will receive the same message.

---

# SNS Practical Workflow

Example architecture:

```text
Application
   │
   ▼
SNS Topic
   │
 ┌─┼─────────────┬──────────────┐
 ▼ ▼             ▼              ▼
Email          Lambda         SQS
```

Services used:

* Amazon SNS
* AWS Lambda
* Amazon SQS

---

# AWS CLI Example (DevOps Method)

Create topic:

```bash
aws sns create-topic --name order-topic
```

Subscribe to topic:

```bash
aws sns subscribe \
--topic-arn TOPIC_ARN \
--protocol email \
--notification-endpoint user@example.com
```

Publish message:

```bash
aws sns publish \
--topic-arn TOPIC_ARN \
--message "Order Created Successfully"
```

---

# Real DevOps Architecture Example

Production architecture:

```text
Application
   │
   ▼
SNS Topic
   │
 ┌─┼─────────────┬──────────────┬─────────────┐
 ▼ ▼             ▼              ▼             ▼
Email          Lambda         SQS          Mobile App
```

SNS distributes the message to **all subscribers simultaneously**.

---

# Interview Question

**What are the steps to use Amazon SNS?**

Answer:

1. Create an SNS topic
2. Create subscriptions
3. Publish message to topic
4. Subscribers receive notifications

---
---
## 2.13 SNS Monitoring (CloudWatch Metrics & Alerts)

![Image](https://miro.medium.com/1%2A62gLrJ0QKMWa3SknUun4_A.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A2000/1%2AKGgzHhHOA9kCe5_xtQeLCg.png)

![Image](https://cdn.prod.website-files.com/655bc1860a87f22da98dd83c/6754a8d7ed2239560fb628ed_6754a882cd877e6511aa3846_publish-subscribe-4%2520%281%29.png)

![Image](https://d2908q01vomqb2.cloudfront.net/fc074d501302eb2b93e2554793fcaf50b3bf7291/2022/02/22/Figure1-Form-arch-1024x498.png)

Monitoring is important when using **Amazon SNS** in production systems.

Monitoring helps teams **track message delivery, detect failures, and ensure reliable notifications**.

SNS monitoring is mainly done using **Amazon CloudWatch**.

---

# Why SNS Monitoring is Important

Monitoring helps detect issues such as:

* Message delivery failures
* Notification delays
* Subscriber endpoint errors
* System performance issues

This ensures that **notifications reach the intended subscribers**.

---

# Key SNS Metrics in CloudWatch

CloudWatch automatically collects metrics from SNS.

Important metrics include:

| Metric                           | Description                               |
| -------------------------------- | ----------------------------------------- |
| NumberOfMessagesPublished        | Total messages sent to SNS topic          |
| NumberOfNotificationsDelivered   | Successful message deliveries             |
| NumberOfNotificationsFailed      | Failed message deliveries                 |
| NumberOfNotificationsFilteredOut | Messages filtered by subscription filters |

These metrics help analyze **SNS performance and reliability**.

---

# Example Monitoring Architecture

```text
Application
     │
     ▼
 SNS Topic
     │
     ▼
CloudWatch Metrics
     │
     ▼
Alerts / Notifications
```

If delivery failures occur, alerts can notify administrators.

---

# Setting CloudWatch Alarms

CloudWatch alarms can trigger alerts when thresholds are exceeded.

Example alarm configuration:

| Metric                 | Threshold    |
| ---------------------- | ------------ |
| Failed notifications   | > 5 failures |
| Message delivery delay | > 1 minute   |

If these thresholds are reached:

* CloudWatch triggers an alarm
* SNS sends alert notifications

---

# Example Alert Workflow

```text
CloudWatch Alarm
      │
      ▼
   SNS Topic
      │
 ┌────┼─────┬─────┐
 ▼    ▼     ▼     ▼
Email SMS Lambda Slack
```

DevOps teams receive **real-time alerts**.

---

# Monitoring SNS Delivery Status

SNS can track delivery status for endpoints such as:

* HTTP/HTTPS endpoints
* Lambda functions
* SQS queues

Delivery logs can help identify:

* Network errors
* Endpoint failures
* Subscriber issues

---

# Monitoring Logs with CloudTrail

SNS API activity can also be tracked using:

AWS CloudTrail

CloudTrail records:

* Topic creation
* Message publishing
* Subscription changes
* Access attempts

This helps with **security auditing**.

---

# SNS Monitoring Best Practices

Recommended monitoring practices:

* Track message delivery metrics
* Monitor failed notifications
* Configure CloudWatch alarms
* Enable delivery logging
* Monitor API activity with CloudTrail

These practices help maintain **reliable messaging systems**.

---

# Real DevOps Monitoring Architecture

Example production monitoring setup:

```text
Application
     │
     ▼
 SNS Topic
     │
     ▼
CloudWatch Metrics → Alerts → DevOps Team
```

This ensures **quick detection of notification failures**.

---

# Interview Question

**How do you monitor Amazon SNS?**

Answer:

Amazon SNS is monitored using **Amazon CloudWatch**, which tracks metrics such as message publishing, successful deliveries, and delivery failures. Alerts can be configured to notify administrators when issues occur.

---
---
## 2.14 SNS vs Other Messaging Services

![Image](https://media2.dev.to/dynamic/image/width%3D800%2Cheight%3D%2Cfit%3Dscale-down%2Cgravity%3Dauto%2Cformat%3Dauto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fo9w37mipcdnztoc80hpu.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2AYQAVFovDNROQ3xbQsHTu9g.png)

![Image](https://miro.medium.com/1%2AdEX47l5u5YbYbeKes9olXQ.png)

In AWS cloud architectures, several messaging and event services are used for communication between systems.
The most commonly compared services are:

* Amazon SNS
* Amazon SQS
* Amazon EventBridge

Each service is designed for **different messaging patterns and use cases**.

---

# 1. Amazon SNS

SNS is a **publish–subscribe messaging service**.

Architecture:

```text
Publisher → SNS Topic → Multiple Subscribers
```

When a message is published, SNS **pushes the message to all subscribers immediately**.

Subscribers can include:

* Email
* SMS
* Lambda
* SQS queues
* HTTP endpoints

### Best Use Cases

* Notification systems
* Event broadcasting
* Monitoring alerts

---

# 2. Amazon SQS

SQS is a **message queue service** used for **asynchronous processing**.

Architecture:

```text
Producer → SQS Queue → Consumer
```

Messages are stored in the queue until a consumer processes them.

### Best Use Cases

* Task processing systems
* Microservices communication
* Background job processing

---

# 3. Amazon EventBridge

Amazon EventBridge is an **event bus service** used for routing events between AWS services and applications.

Architecture:

```text
Event Source → EventBridge → Target Services
```

EventBridge can route events to:

* Lambda
* SQS
* SNS
* Step Functions
* Other AWS services

### Best Use Cases

* Event-driven architectures
* SaaS integrations
* Application event routing

---

# Comparison Table

| Feature          | SNS                  | SQS             | EventBridge       |
| ---------------- | -------------------- | --------------- | ----------------- |
| Service Type     | Pub/Sub              | Message Queue   | Event Bus         |
| Message Delivery | Push                 | Poll            | Event routing     |
| Consumers        | Multiple subscribers | Single consumer | Multiple targets  |
| Message Storage  | No                   | Yes             | No                |
| Use Case         | Notifications        | Task processing | Event integration |

---

# Simple Way to Understand

| Service     | Purpose                            |
| ----------- | ---------------------------------- |
| SNS         | Send notifications to many systems |
| SQS         | Store tasks for workers            |
| EventBridge | Route events between services      |

---

# Example Architecture

Modern event-driven system:

```text
Application
   │
   ▼
EventBridge
   │
 ┌─┼─────────────┬───────────────┐
 ▼ ▼             ▼               ▼
SNS Topic      SQS Queue       Lambda
```

Services involved:

* Amazon EventBridge
* Amazon SNS
* Amazon SQS
* AWS Lambda

---

# Real Production Example

Example architecture for an **e-commerce platform**.

```text
Order Created Event
        │
        ▼
   EventBridge
        │
  ┌─────┼──────────┐
  ▼     ▼          ▼
SNS   SQS       Lambda
Alerts Workers  Processing
```

* SNS sends alerts
* SQS queues handle background tasks
* Lambda processes events

---

# Interview Question

**What is the difference between SNS, SQS, and EventBridge?**

Answer:

* **SNS** is a publish–subscribe service used for notifications.
* **SQS** is a message queue used for asynchronous task processing.
* **EventBridge** is an event bus used to route events between AWS services.

---
---
## 2.15 Amazon SNS Interview Questions (DevOps Q&A)

![Image](https://miro.medium.com/1%2AKQyq9GSoRVYnFVwMyejRYw.png)

![Image](https://docs.aws.amazon.com/images/prescriptive-guidance/latest/cloud-design-patterns/images/publish-subscribe-4.png)

![Image](https://d2908q01vomqb2.cloudfront.net/1b6453892473a467d07372d45eb05abc2031647a/2017/11/20/introducing_sns_message_filtering_image_1.png)

![Image](https://docs.aws.amazon.com/images/sns/latest/dg/images/sns-delivery-protocols.png)

Below are **important interview questions and answers** about **Amazon SNS**.
These questions are commonly asked in **AWS / DevOps / Cloud interviews**.

---

# 1. What is Amazon SNS?

**Answer**

Amazon SNS is a **fully managed publish–subscribe messaging service** that allows applications to send messages to multiple subscribers simultaneously.

It is mainly used for **notifications and event distribution**.

---

# 2. What is the publish–subscribe model?

**Answer**

The publish–subscribe model is a messaging pattern where:

* Publishers send messages to a **topic**
* Subscribers receive messages from the topic

Architecture:

```text
Publisher → SNS Topic → Multiple Subscribers
```

---

# 3. What are the main components of SNS?

**Answer**

Main components include:

* Publisher
* Topic
* Subscriber
* Endpoint

---

# 4. What is an SNS topic?

**Answer**

An SNS topic is a **communication channel** where messages are published and delivered to subscribed endpoints.

Example:

```text
Application → SNS Topic → Subscribers
```

---

# 5. What types of endpoints does SNS support?

**Answer**

SNS supports several endpoints:

* Email
* SMS
* HTTP/HTTPS
* AWS Lambda
* Amazon SQS
* Mobile push notifications

---

# 6. What is the SNS fanout pattern?

**Answer**

The fanout pattern sends one message from SNS to **multiple SQS queues simultaneously**.

Architecture:

```text
Publisher → SNS Topic → Multiple SQS Queues
```

Each queue processes the message independently.

---

# 7. What is message filtering in SNS?

**Answer**

Message filtering allows subscribers to receive **only specific messages based on message attributes**.

This reduces unnecessary message delivery.

---

# 8. How does SNS deliver messages?

**Answer**

SNS uses a **push delivery model**, meaning messages are automatically sent to subscribers.

Subscribers do not need to request messages.

---

# 9. What is the difference between SNS and SQS?

| Feature          | SNS                  | SQS             |
| ---------------- | -------------------- | --------------- |
| Messaging type   | Publish/Subscribe    | Message Queue   |
| Message delivery | Multiple subscribers | One consumer    |
| Message storage  | No                   | Yes             |
| Use case         | Notifications        | Task processing |

---

# 10. What is the difference between SNS and EventBridge?

| Feature         | SNS             | EventBridge         |
| --------------- | --------------- | ------------------- |
| Messaging model | Pub/Sub         | Event routing       |
| Event filtering | Basic filtering | Advanced filtering  |
| Integration     | AWS services    | AWS + SaaS services |

Example service:

* Amazon EventBridge

---

# 11. What happens when a message is published to SNS?

**Answer**

When a message is published:

1. SNS receives the message
2. SNS checks topic subscriptions
3. SNS delivers the message to all subscribers

---

# 12. What is the maximum message size in SNS?

**Answer**

Maximum message size:

**256 KB**

---

# 13. How is SNS pricing calculated?

**Answer**

SNS pricing is based on:

* Publish requests
* Message deliveries
* SMS notifications

AWS also provides a **free tier for SNS usage**.

---

# 14. How do you secure SNS?

**Answer**

SNS security can be implemented using:

* IAM policies
* SNS topic policies
* Encryption using AWS KMS

Service used:

* AWS Key Management Service

---

# 15. How do you monitor SNS?

**Answer**

SNS can be monitored using:

* Amazon CloudWatch
* AWS CloudTrail

These services track message publishing, deliveries, and failures.

---

# 16. What are some real-world use cases of SNS?

**Answer**

SNS is used for:

* System monitoring alerts
* Application notifications
* Event-driven architectures
* Mobile push notifications
* Microservices communication

---

# 17. Can SNS send messages to multiple services?

**Answer**

Yes. SNS can send messages to multiple subscribers such as:

* Email
* SMS
* Lambda
* SQS
* HTTP endpoints

---

# 18. What is the difference between push and pull messaging?

| Type | Example Service | Description                 |
| ---- | --------------- | --------------------------- |
| Push | SNS             | Messages automatically sent |
| Pull | SQS             | Consumers request messages  |

---

# 19. How does SNS integrate with AWS services?

**Answer**

SNS integrates with services such as:

* Amazon SQS
* AWS Lambda
* Amazon CloudWatch
* Amazon S3

---

# 20. What are the advantages of Amazon SNS?

**Answer**

Advantages include:

* Real-time notifications
* Highly scalable messaging
* Event-driven architecture support
* Integration with many AWS services
* Simple and reliable communication system

---
