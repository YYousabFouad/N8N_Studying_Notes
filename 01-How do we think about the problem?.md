# How Do We Think About the Problem?

Before building an n8n workflow, we should first understand **the problem we want to solve**.

## 1. Why Should We Automate?

We should not automate something just because n8n can do it.

First, ask:

### A. Is there repetition?

Look for a task that happens repeatedly because of a specific **trigger**.

Examples:

- A new row is added to a Google Sheet.
    
- A customer submits a form.
    
- A new email arrives.
    
- A new order is created.
    

If the same process happens again and again, it may be a good candidate for automation.

### B. Does automation create business value?

Compare:

**Manual process**  
→ Time + Human effort + Money

**Automated process**  
→ Less manual effort + Less time + Lower cost

The important question is:

> **Is the value gained from automation greater than the effort and cost of building it?**

So automation should solve a real business problem, not just be technically interesting.

---

# 2. Think in Terms of Trigger → Action

A simple way to understand an automation is:

**Something happens → We react to it**

### Trigger

The **trigger** is the event that starts the workflow.

Examples:

- New row added to Google Sheets
    
- New email received
    
- New form submission
    
- New order created
    

### Action / Output

The **action** is what we want n8n to do after the trigger happens.

Examples:

- Send an email
    
- Add data to a spreadsheet
    
- Send a notification
    
- Update a database
    

---

# 3. Example: Google Sheets → Gmail

The video uses the idea of connecting **Google Sheets with Gmail** as an example of an automation workflow.

Think about it as:

```text
┌─────────────────────┐
│   Something happens │
│   in Google Sheets  │
└──────────┬──────────┘
           │
           ▼
       TRIGGER
           │
           ▼
┌─────────────────────┐
│     n8n Workflow    │
└──────────┬──────────┘
           │
           ▼
        ACTION
           │
           ▼
┌─────────────────────┐
│    Send an Email    │
│       with Gmail    │
└─────────────────────┘
```

The important thing is **not the specific Google Sheets → Gmail workflow**.

The important idea is learning to recognize:

> **What event starts the process?**
> 
> **What action should happen afterward?**

---

# 4. The Problem-Solving Checklist

Before creating an n8n workflow, ask:

1. **What is the repetitive task?**
    
2. **What event triggers the task?**
    
3. **What action normally happens after that event?**
    
4. **How often does this happen?**
    
5. **How much time/effort/money does the manual process consume?**
    
6. **Will automation provide enough value to justify building it?**
    

---

# Key Takeaway

- **Don't start with n8n nodes. Start with the problem.**
    
- A basic automation can be understood as **Trigger → Action**, and its purpose is to reduce repetitive manual work when doing so creates real value.