# 🚀 Amazon SQS (Simple Queue Service)
Amazon SQS is a fully-managed distributed **message queuing service** that enables decoupling and scaling of microservices, distributed systems, & serverless applications.  
It allows asynchronous communication between components by sending messages through a secure, durable, highly scalable queue.

---

## 🎯 Why SQS is Used?
| Problem | SQS Solution |
|--------|--------------|
| Services depend on each other directly | Decouples microservices |
| API traffic spikes overload apps | Smooths workload using buffering |
| Processes fail due to system downtime | Durable message storage |
| Tasks must be processed asynchronously | Background processing |
| Message loss or duplication risk | Ensures reliability + retries |

---

## 🧱 Types of SQS Queues
| Type | Description | Use Case |
|------|------------|-----------|
| **Standard Queue** | Unlimited throughput, best-effort ordering | Email sending, notifications, background processing |
| **FIFO Queue (First-In-First-Out)** | Exact ordering & no duplicate messages | Banking, transactions, billing |
| **DLQ (Dead Letter Queue)** | Stores failed processing messages | Debugging, error handling |

---

## 🔐 Key Features
- High availability & durability
- Automatic scaling
- At-least-once delivery
- Message retention up to 14 days
- Message visibility timeout
- Dead-letter queues
- Secure (IAM & SSE Encryption)

---

## 🔧 Step-By-Step: Create SQS Queue
### 🪜 Create Standard Queue in AWS Console
1. Login to **AWS Console**
2. Open **SQS service**
3. Click **Create Queue**
4. Select **Standard Queue**
5. Enter queue name → Example: `order-queue`
6. Configure:
   - Visibility Timeout: **30 sec**
   - Message Retention: **4 days**
   - Encryption: **Enabled**
7. Keep defaults & click **Create**

---

## 🚚 Sending Message to SQS (Console)
1. Open the queue
2. Click **Send & Receive Messages**
3. Enter message body (JSON optional)
4. Click **Send Message**

---

## 🧾 Receive & Process Messages
1. Go to **Poll for Messages**
2. View received messages
3. Select message → **Delete**
4. Message removed from queue permanently

---

## 🔁 Reliability Controls
| Feature | Purpose |
|---------|---------|
| **Visibility Timeout** | Prevent duplicate processing |
| **DLQ** | Store failed messages |
| **Retry Mechanism** | Ensures message success |
| **Long Polling** | Reduces empty response charges |

---

# 🏗 Architecture Diagram — Basic SQS Workflow

```mermaid
flowchart LR
    A[Producer / Application] -->|Send Message| B[SQS Queue]
    B -->|Poll Message| C[Consumer / Lambda / Worker]
    C -->|Process| D[(Database / Service)]
    C -->|Delete| B

sequenceDiagram
    participant U as User
    participant AP as Application Server
    participant Q as SQS Queue
    participant L as Lambda Worker
    participant DB as Database

    U->>AP: Submit Request
    AP->>Q: Add to Queue
    L->>Q: Poll Messages
    L->>DB: Save / Process
    DB-->>L: Success
    L->>Q: Delete Message

