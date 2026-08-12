# 1. What is a Node in n8n?

A **Node** is a single building block in an n8n automation.

Think of a node as **one step that performs one job**.

For example:

- Get data from Google Sheets
- Send an email with Gmail
- Make an HTTP request
- Check a condition
- Transform data
- Save data to a database
- Send a Slack message

So if your automation has 5 different tasks, you will probably have several nodes connected together.

### Simple example

Imagine you want:

> "When I receive a new customer from Google Sheets, send them a Gmail message."

You might have:

```
[Google Sheets]
       ↓
     [IF]
       ↓
    [Gmail]
```

Each box is a **node**.

---

# 2. What does a Node actually contain?

A node usually has three important things:

### 1. Input

The node can receive data from another node.

### 2. Operation

The node performs some action on that data.

### 3. Output

The node produces data that can be passed to the next node.

Think:

```
Input → Process → Output
```

For example:

```
Customer Data
      ↓
   Gmail Node
      ↓
Email Sent
```

The Gmail node receives information such as:

```
name: John
email: john@gmail.com
```

and uses that information to send an email.

---

# 3. Types of Nodes

In n8n, you will encounter different kinds of nodes.

The most important distinction for a beginner is:

### Trigger Nodes

They **start** the workflow.

Examples:

- Schedule Trigger
- Webhook
- Gmail Trigger
- Google Sheets Trigger
- Form Trigger

### Action / Regular Nodes

They **do something** after the workflow starts.

Examples:

- Gmail
- Google Sheets
- HTTP Request
- Slack
- Telegram

### Logic / Processing Nodes

They help you make decisions or manipulate data.

Examples:

- IF
- Switch
- Filter
- Set/Edit Fields
- Code

So you can think of nodes like this:

```
              NODES
                │
       ┌────────┼─────────┐
       ↓        ↓         ↓
    Trigger   Action    Logic
       │        │         │
     Start    Do work   Make decisions
```

---

# 4. What is a Trigger?

A **Trigger** is the thing that tells n8n:

> **"Start this workflow now."**

This is extremely important.

A normal node doesn't usually decide when the workflow should start.

The **trigger** does.

---

## Example 1: Schedule Trigger

Suppose you want n8n to run every morning at 9 AM.

You could use:

```
Schedule Trigger
       ↓
   Get Data
       ↓
   Process Data
       ↓
    Send Email
```

The Schedule Trigger waits.

At 9 AM:

```
9:00 AM
   ↓
Trigger fires
   ↓
Workflow starts
```

---

# 5. Example: Gmail Trigger

Suppose you want:

> "Whenever I receive a new email, process it."

You could have:

```
Gmail Trigger
      ↓
     IF
      ↓
    Gmail
```

The Gmail Trigger waits for the event.

When the event happens:

```
New email arrives
       ↓
Gmail Trigger
       ↓
Workflow starts
```

---

# 6. Example: Webhook Trigger

A webhook is another very important trigger.

Imagine another application sends a request to n8n.

```
Other Application
       ↓
    HTTP Request
       ↓
     Webhook
       ↓
   n8n Workflow
```

The webhook receives the request and starts the workflow.

This is commonly used when you want another application to communicate with n8n.

---

# 7. Important: A Trigger is also a Node

This is an important detail.

You shouldn't think:

> Trigger and Node are completely different things.

Instead:

> **A trigger is a special type of node.**

So:

```
Node
├── Trigger Node
├── Action Node
├── Logic Node
└── Data/Processing Node
```

For example:

**Schedule Trigger** is a node.

But its special job is to **start the workflow**.

---

# 8. What is a Workflow?

A **workflow** is the complete automation you build in n8n.

It contains:

- Trigger(s)
- Nodes
- Connections
- Data flow
- Logic

For example:

```
Schedule Trigger
       ↓
Google Sheets
       ↓
     IF
    ↙  ↘
  YES   NO
   ↓     ↓
 Gmail   End
```

All of this together is one **workflow**.

---

# 9. Think about it like a real-world process

Suppose your job is:

> Every day, check a spreadsheet and email customers who haven't paid.

The human process might be:

```
Every morning
     ↓
Open spreadsheet
     ↓
Check customers
     ↓
Find unpaid customers
     ↓
Send emails
```

In n8n:

```
Schedule Trigger
       ↓
Google Sheets
       ↓
Filter / IF
       ↓
Gmail
```

Now you've converted a **manual process into an automated workflow**.

---

# 10. The most important concept: Data flows between Nodes

This is where n8n becomes really interesting.

Nodes don't just execute independently.

They can **pass data to each other**.

Example:

```
Google Sheets
      ↓
{
  "name": "John",
  "email": "john@gmail.com"
}
      ↓
     Gmail
```

The Gmail node can use:

```
name
email
```

from the previous node.

So n8n is essentially moving and transforming data through a series of connected steps.

```
Trigger
   ↓
Data
   ↓
Node
   ↓
Modified Data
   ↓
Node
   ↓
Final Result
```

---

# 11. Connections

The lines between nodes represent the **connection/data flow**.

Example:

```
[Trigger] ─────→ [Google Sheets] ─────→ [Gmail]
```

The direction matters.

The workflow normally processes nodes according to their connections.

Think of the arrows as saying:

> "After this step, send the result to the next step."

---

# 12. A complete example

Let's say you want to automate:

> When a new customer is added to Google Sheets, send them a welcome email.

You could build:

```
Google Sheets Trigger
         ↓
      Get Data
         ↓
       Gmail
```

### Step 1 — Trigger

Google Sheets detects a new row.

```
New row added
      ↓
Trigger fires
```

### Step 2 — Get/process data

n8n receives something like:

```
Name: Ahmed
Email: ahmed@gmail.com
```

### Step 3 — Gmail

The Gmail node takes the email address and sends:

```
To: ahmed@gmail.com

Subject: Welcome!

Hello Ahmed...
```

The whole thing is one workflow.

---

# 13. Trigger vs Node vs Workflow

This distinction is worth memorizing:

|Concept|Meaning|
|---|---|
|**Node**|One building block / one step|
|**Trigger**|A special node that starts the workflow|
|**Workflow**|The complete automation made from connected nodes|

Or even simpler:

```
Trigger
   ↓
Starts
   ↓
Nodes
   ↓
Perform work
   ↓
Workflow
   ↓
Achieves the goal
```

A better mental model is:

> **Trigger = When?**  
> **Nodes = What happens?**  
> **Workflow = The whole process**

---

# 14. One important correction

You may see explanations saying:

> "Every workflow must have exactly one trigger."

That's **not a good rule to memorize for n8n**.

A workflow can contain multiple trigger nodes. For example, you could have different ways of starting a workflow.

The important idea is:

> **A workflow needs a way to be triggered when you want it to run automatically.**

For a beginner, however, it's usually easier to start with **one trigger and then build the rest of the workflow**.

---

# 15. Manual execution vs automatic execution

When you're learning n8n, you will often execute a workflow manually.

For example:

```
You click "Execute"
        ↓
Trigger / workflow executes
        ↓
Nodes run
```

Later, when you activate the workflow, n8n can run it automatically according to its trigger.

For example:

```
Workflow Active
      ↓
Schedule Trigger
      ↓
9:00 AM
      ↓
Workflow executes automatically
```

This distinction is important when you're testing your automations.

---

# 16. The mental model you should use

When looking at an n8n workflow, ask yourself three questions:

### Question 1: What starts it?

Look for the **Trigger**.

> "What event causes this automation to run?"

### Question 2: What happens after it starts?

Look at the **nodes**.

> "What does each node do?"

### Question 3: What is the final goal?

Look at the entire **workflow**.

> "What problem is this automation solving?"

---

# Key Takeaway

- **Node:** One building block that performs a task.
- **Trigger:** A special node that starts the workflow when an event occurs.
- **Workflow:** The complete automation made by connecting nodes together.
- **Data flows between nodes**, allowing one node's output to become another node's input.

### The easiest way to remember it:

```
TRIGGER
"When should I start?"
       ↓
NODES
"What should I do?"
       ↓
WORKFLOW
"How do all these steps work together
to achieve the goal?"
```

![[02-N8N_Basics.png]]