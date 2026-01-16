# 🎙️ Agente de Voz SDR - Qualificação Automatizada por Telefone

Sistema automatizado de qualificação de leads via ligação telefônica, combinando **IA conversacional** (LLM), **VAPI**, **n8n** e **Supabase** para qualificar leads e agendar reuniões 24/7.

---

## 📊 Métricas do Sistema

| Métrica | Valor |
|---------|-------|
| Latência de Resposta | ~800ms - 1.5s |
| TTS | ElevenLabs Neural (qualidade humana) |
| Operação | 24/7 automatizado |
| Integrações | Google Calendar, CRM, WhatsApp |

---

## 🏗️ Arquitetura Geral

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│   Tally Form    │────▶│   Webhook n8n   │────▶│   VAPI          │
│   (Lead Capture)│     │   (Trigger)     │     │   (Liga p/ Lead)│
└─────────────────┘     └─────────────────┘     └────────┬────────┘
                                                         │
                                                         ▼
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│   Supabase      │◀───▶│   n8n           │◀───▶│   LLM + TTS     │
│   (CRM + RAG)   │     │   (Orquestrador)│     │   (Conversa IA) │
└─────────────────┘     └────────┬────────┘     └─────────────────┘
                                 │
                        ┌────────┴────────┐
                        ▼                 ▼
              ┌─────────────────┐ ┌─────────────────┐
              │   Google        │ │   WhatsApp      │
              │   Calendar      │ │   (Follow-up)   │
              └─────────────────┘ └─────────────────┘
```

---

## 🔄 Fluxo Passo a Passo

### 1️⃣ Captura do Lead (Formulário)

1. Lead preenche formulário Tally com interesse
2. Webhook dispara para n8n
3. n8n salva lead no Supabase com `status = novo`
4. Trigger envia comando para VAPI iniciar ligação

### 2️⃣ Ligação Outbound (VAPI)

```
┌──────────────────────────────────────────────────────────────┐
│ VAPI recebe comando de ligar                                 │
│     │                                                        │
│     ▼                                                        │
│ Inicia chamada para o telefone do lead                       │
│     │                                                        │
│     ▼                                                        │
│ STT (Speech-to-Text) captura voz do lead                     │
│     │                                                        │
│     ▼                                                        │
│ LLM (GPT-4o-mini) processa com contexto:                     │
│     • Dados do lead (nome, interesse, empresa)               │
│     • RAG com base de conhecimento                           │
│     • Prompt de qualificação SDR                             │
│     │                                                        │
│     ▼                                                        │
│ TTS (ElevenLabs) converte resposta em voz natural            │
│     │                                                        │
│     ▼                                                        │
│ Áudio é enviado em tempo real para o lead                    │
│     │                                                        │
│     ▼                                                        │
│ Tratamento de interrupções (barge-in nativo)                 │
└──────────────────────────────────────────────────────────────┘
```

### 3️⃣ Qualificação Inteligente

O agente de voz qualifica o lead através de perguntas SPIN:

**S**ituação: "Qual é o tamanho da sua equipe atual?"
**P**roblema: "Qual o maior desafio que você enfrenta hoje?"
**I**mplicação: "Quanto isso está custando por mês pra empresa?"
**N**eed-payoff: "Se pudéssemos resolver isso, qual seria o impacto?"

### 4️⃣ Ações Automatizadas

Baseado na conversa, o agente pode executar:

| Ação | Trigger |
|------|---------|
| Agendar reunião | Lead qualificado + interesse confirmado |
| Enviar material | Lead pede mais informações |
| Encaminhar para humano | Objeção complexa ou pedido explícito |
| Salvar dados no CRM | Toda ligação |

### 5️⃣ Pós-Ligação

```
┌──────────────────────────────────────────────────────────────┐
│ Ligação encerrada                                            │
│     │                                                        │
│     ▼                                                        │
│ n8n recebe webhook com resumo da conversa                    │
│     │                                                        │
│     ├── Atualiza status no Supabase                         │
│     ├── Se agendou → Cria evento no Google Calendar         │
│     ├── Se qualificado → Notifica equipe comercial          │
│     └── Se desqualificado → Marca para não recontatar       │
└──────────────────────────────────────────────────────────────┘
```

---

## 🛠️ Stack Tecnológica

| Componente | Tecnologia |
|------------|------------|
| Orquestração de Voz | VAPI |
| IA / LLM | OpenAI GPT-4o-mini |
| TTS | ElevenLabs Neural |
| STT | Deepgram (via VAPI) |
| Backend | n8n (self-hosted) |
| Database | Supabase (PostgreSQL) |
| RAG | Supabase pgvector |
| Telefonia | Twilio / Vonage |
| Agendamento | Google Calendar |
| Formulários | Tally |

---

## 🤖 Persona do Agente

O agente foi configurado como **SDR (Sales Development Representative)**:

- **Tom:** Profissional, consultivo, não agressivo
- **Estilo:** Conversa natural, não roteirizada
- **Objetivos:**
  - Qualificar o lead (BANT/SPIN)
  - Identificar dores e necessidades
  - Agendar reunião com consultor
  - Nunca forçar a venda

**Regras de Anti-Alucinação:**
- Só responde sobre o que está no RAG
- Se não souber, admite e oferece enviar informação
- Nunca inventa preços, prazos ou recursos

---

## ⚡ Funcionalidades Avançadas

### Barge-in (Interrupção)
O lead pode interromper o agente a qualquer momento. O agente para de falar e escuta.

### Latência Otimizada
- Streaming de áudio em tempo real
- LLM com função calling otimizada
- TTS com pre-buffer

### Detecção de Silêncio
Se o lead ficar em silêncio por 5s, o agente pergunta: "Você ainda está aí?"

### Transferência para Humano
Se o lead pedir, o agente pode transferir para um atendente humano.

---

## 📁 Estrutura do Projeto

```
projetos/voice-sdr/
├── README.md                    # Este arquivo
├── voice-sdr-workflow.json      # Workflow n8n principal
└── prompts/
    └── system-prompt.md         # Prompt do agente
```

---

## 📞 Contato

**Desenvolvido por:** Isaac Silveira  
**Email:** izack07@gmail.com  
**LinkedIn:** [isaac-silveira](https://www.linkedin.com/in/isaac-silveira-49b09821a)  
**Portfólio:** [izack07-collab.github.io](https://izack07-collab.github.io)

---

*Sistema desenvolvido em Janeiro 2026*
