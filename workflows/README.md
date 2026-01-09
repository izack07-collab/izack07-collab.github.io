# 🤖 n8n Workflows Portfolio

This folder contains examples of automation workflows I've developed using **n8n** and **AI agents**.

> ⚠️ **Note:** These are simplified versions for portfolio purposes. Credentials and sensitive data have been removed.

---

## 📁 Workflow Index

| # | File | Description | Stack |
|---|------|-------------|-------|
| 01 | [ugc-video-generator.json](./01-ugc-video-generator.json) | Automated UGC video creation from product images | n8n, GPT-4 Vision, Veo3, fal.ai |
| 02 | [multiagent-support.json](./02-multiagent-support.json) | Multi-agent support system with RAG | n8n, OpenAI, Supabase Vector Store |
| 03 | [ecommerce-sales-agent.json](./03-ecommerce-sales-agent.json) | E-commerce sales agent with payment integration | n8n, OpenAI, Supabase, Asaas |
| 04 | [payment-webhook.json](./04-payment-webhook.json) | Payment confirmation webhook handler | n8n, Asaas, Supabase, Trello |
| 05 | [lead-capture-sdr.json](./05-lead-capture-sdr.json) | Lead capture + SDR qualification agent | n8n, Tally, Notion, OpenAI, WhatsApp |
| 06 | [crm-subworkflow.json](./06-crm-subworkflow.json) | Reusable subworkflow for CRM integration | n8n, Trello, Supabase |

---

## 🎬 01 - UGC Video Generator

**Purpose:** Automatically generate UGC-style commercial videos from product images.

**Flow:**
1. Receive image via webhook
2. Analyze image with GPT-4 Vision
3. Generate styled image with Nano Banana (fal.ai)
4. Create video with Veo3
5. Send results via email

**Use cases:**
- E-commerce product videos
- Social media content
- Ad creatives

---

## 🤖 02 - Multi-Agent Support System

**Purpose:** Technical support center with intelligent routing and RAG.

**Architecture:**
- **Orchestrator Agent:** Routes questions to specialists
- **n8n Specialist:** Answers n8n questions
- **Lovable Specialist:** Answers Lovable questions
- **FlutterFlow Specialist:** Answers FlutterFlow questions

**Features:**
- Each specialist has its own vector store
- Persistent memory with PostgreSQL
- Intelligent question routing

---

## 🛒 03 - E-commerce Sales Agent

**Purpose:** Automated sales agent for online stores.

**Flow:**
1. Receive customer message
2. Present products based on interest
3. Create order
4. Collect customer data
5. Generate payment link (PIX, Boleto, Credit Card)
6. Send payment link

**Integrations:**
- Supabase (database)
- Asaas (payment gateway)
- MCP Tools (order management)

---

## 💳 04 - Payment Confirmation Webhook

**Purpose:** Handle payment confirmations from Asaas.

**Flow:**
1. Receive webhook from Asaas
2. Update order status to "paid"
3. Update lead status
4. Move CRM card to "Paid" list

---

## 📞 05 - Lead Capture + SDR Agent

**Purpose:** Capture leads from forms and automatically qualify via WhatsApp.

**Flow:**
1. Receive lead from Tally form
2. Save to Supabase
3. Create entry in Notion CRM
4. SDR Agent sends first message
5. Qualify lead and present solutions

**Features:**
- Automatic lead qualification
- Persistent conversation memory
- WhatsApp integration (Z-API)

---

## 🔄 06 - CRM Subworkflow

**Purpose:** Reusable subworkflow for CRM operations.

**Features:**
- Create card in Trello (or any CRM)
- Link card ID back to lead in Supabase
- Modular and reusable

---

## 📬 Contact

Interested in implementing similar automations?

- 📧 **Email:** izack07@gmail.com
- 📱 **WhatsApp:** (11) 98558-7684
- 🔗 **LinkedIn:** [Isaac Silveira](https://www.linkedin.com/in/isaac-silveira-49b09821a)
- 🌐 **Portfolio:** [izack07-collab.github.io](https://izack07-collab.github.io)

---

<p align="center">
  <i>Building automations that work while you sleep 🌙</i>
</p>
