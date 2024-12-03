---
layout: post
subtitle: Ensuring Transactional Continuity with the Outbox Pattern in distributed applications
title: EDA with the Outbox Pattern
author: Shawn Wallace
tags: [Event-Driven Architecture, Patterns & Practices, Architecture]
thumbnail-img: /assets/img/outbox-pattern.webp
---

Distributed systems are powerful and help us address many problems but they often introduce others. Ensuring 
transactional continuity in multi-step processes are particularly difficult challenges. One that comes up a lot for me (for instance) is updating a database 
and publishing an event to a event stream simultaneously. This can lead to data inconsistencies and critical failures 
due to the *dual-write problem*.

The *dual-write problem* occurs when an application updates multiple systems independently. This can lead to potentially 
causing inconsistencies due to network errors or other exceptions. Distributed systems lack transactional 
boundaries, making it hard to ensure both operations succeed or fail. This can lead leads to data inconsistencies, 
duplicate data, or logical errors requiring manual reconciliation.

Thankfully there are design patterns that can help us address this problem. The transactional *outbox pattern* 
is a reliable solution to this challenge. Let's explore its definition, problems solved, and implementation to ensure transactional consistency in applications that are part of distributed systems.


(watch this [video](https://www.youtube.com/watch?v=XALvnX7MPeo) from Milan Jovanovic)

-----------

### The Problem: Transactional Continuity in Distributed Systems

Transactional continuity seeks to ensure that all operations in a system occur together as a single unit of work. For example, when a user places an order, the system should:
1.	Update the database with the order details.
2.	Publish an event to notify other services, such as inventory or shipping.

However, without proper safeguards, distributed systems can experience:

* **Partial Updates**: One system completes its work (e.g., database update), but posting to the event stream fails.
* **Data Inconsistency**: Other services may miss critical updates or receive incomplete information.
* **Complex Error Handling**: Recovering from such failures can be very involved/complicated and error-prone.

The root of the problem lies in attempting to perform two distinct operations—updating the database and 
sending a message—atomically, across different systems.

#### What is the Outbox Pattern?

The outbox pattern provides a robust way to maintain transactional continuity. Instead of directly publishing events to a event stream, the pattern introduces an intermediate step: an outbox table within the database.

How it works:
1.	When a transaction occurs, all changes, including messages to be published, are written to the database in a single atomic transaction. This includes writing a record to the outbox table.
2.	A separate process (often a background job) reads messages from the outbox table and publishes them to the event stream.
3.	Once a message is successfully published to the event stream, it’s marked as processed in the outbox table.

This approach decouples the database write and message publishing, ensuring that no partial updates occur.

#### How the Outbox Pattern Solves the Problem

The outbox pattern resolves transactional continuity issues by:
* **Ensuring Atomicity**: Writing both the database changes and the event to the outbox table happens within the same transaction. If the transaction fails, nothing is committed.
* **Decoupling Message Delivery**: A background process handles the responsibility of delivering messages, allowing the main transactionto focus on database updates.
* **Providing Reliability**: In case of a failure during message publishing, the message remains in the outbox table for retry.

For example, in an e-commerce system, an order creation process would:
1. Write the order to the database.
2. Write an `OrderCreated` message to the outbox table.
3. A background process would pick up the `OrderCreated` message and publish it to the event stream for processing by downstream services.

### Implementation Overview

To implement the outbox pattern, you will minimally need the following components:
1.	**Outbox Table**: A dedicated table in your application/transactional database to store messages to be published.
	* Example schema: `id`, `payload`, `status`, `created_at`, `processed_at`, `trace_id`.
2.	**Message Relay**: A service or background process to read messages from the outbox table and send them to the event stream.
	* Technologies: Microservices, Cron jobs, message brokers, or cloud-based eventing systems.
3.	**Idempotent Processing**: Ensure message consumers can handle duplicate messages gracefully.

You Create the Order and create an entry in the Outbox in one database transaction.

```sql
-- Example SQL for creating an order and writing to the outbox table in one transaction
BEGIN TRANSACTION;
INSERT INTO orders (id, details) VALUES (1, 'Order Details');
INSERT INTO outbox (id, payload, status) VALUES (1, '{"event": "OrderCreated"}', 'PENDING');
COMMIT;
```
A seperate worker process can handle retrieving unsent Outbox messages, publish the events to the event stream, and update the Outbox entries with status.

```csharp
// Message relay process
const messages = db.query("SELECT * FROM outbox WHERE status = 'PENDING'");
messages.forEach(message => {
  sendMessageToQueue(message.payload);
  db.query("UPDATE outbox SET status = 'PROCESSED' WHERE id = ?", message.id);
});
```
The worker process can be refined for batching, retries, and possibly implementing dead-letter functionality per your specific requirements.


#### Benefits of the Outbox Pattern

Adopting the outbox pattern provides several advantages:
* **Consistency**: Database updates and event publishing happen reliably.
* **Simplified Error Handling**: Messages remain in the outbox until successfully delivered.
* **Scalability**: The pattern works well with distributed systems and large-scale applications.
  
#### Challenges and Considerations

While the outbox pattern offers a robust solution, it’s not without challenges:
* **Increased Complexity**: Setting up and maintaining the outbox table and message relay adds overhead.
* **Performance Impacts**: Polling the outbox table for pending messages can introduce latency.
* **Monitoring**: Requires robust monitoring to ensure messages are processed in a timely manner.

#### Alternatives

The outbox pattern is often compared to:
* **Two-Phase Commit**: A more complex approach that ensures atomicity across systems but at the cost of 
performance and scalability.
* **Idempotent Consumers**: While useful, this alone does not address the dual-write problem.

By combining the outbox pattern with idempotent consumers, you can achieve a highly reliable and scalable architecture.

### Finally
In modern distributed systems, maintaining transactional continuity is critical. Implementing the outbox 
pattern will help ensure consistency between multiple step processes like database updates and event streams publishing. The will make systems 
resilient, reliable, and scalable.

Share your experiences and lessons learned in the comments.