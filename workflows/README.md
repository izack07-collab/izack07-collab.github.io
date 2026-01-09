# 📦 Workflow Examples

Coleção de templates de workflows n8n para automação e IA. Cada template demonstra um caso de uso comum que pode ser adaptado para diferentes projetos.

---

## 📋 Templates Disponíveis

### 1. UGC Video Generator
**Arquivo:** `01-ugc-video-generator.json`

Gera vídeos estilo UGC (User Generated Content) automaticamente usando IA.

**Fluxo:**
1. Recebe imagem de referência via Webhook
2. Analisa imagem com GPT-4 Vision
3. Gera prompt otimizado para imagem UGC
4. Cria imagem via fal.ai (Nano Banana)
5. Gera vídeo via Veo3 (image-to-video)
6. Envia resultado por email

**Stack:** Webhook → OpenAI Vision → fal.ai → Veo3 → Gmail

---

### 2. Multi-Agent Support
**Arquivo:** `02-multiagent-support.json`

Sistema de atendimento com múltiplos agentes especializados que se revezam conforme o contexto.

**Características:**
- Agente de triagem inicial
- Roteamento para especialistas (vendas, suporte técnico, financeiro)
- Memória compartilhada entre agentes
- Escalação para humano quando necessário

**Stack:** Chat Trigger → Router Agent → Specialist Agents → Supabase

---

### 3. E-commerce Sales Agent
**Arquivo:** `03-ecommerce-sales-agent.json`

Agente de vendas completo para loja virtual com gestão de pedidos e pagamentos.

**Fluxo:**
1. Cliente inicia conversa
2. Verifica/cria cadastro no Supabase
3. Agente apresenta produtos
4. Coleta dados do cliente (nome, CPF, email, telefone, endereço)
5. Gera link de pagamento (PIX, Boleto, Cartão)
6. Acompanha status do pedido

**Stack:** Chat Trigger → Supabase → Sales Agent (GPT-4) → MCP Tools → Asaas

---

### 4. Payment Webhook
**Arquivo:** `04-payment-webhook.json`

Processa webhooks de plataformas de pagamento e atualiza status de pedidos.

**Eventos tratados:**
- Pagamento confirmado
- Pagamento recusado
- Reembolso processado
- Assinatura renovada/cancelada

**Stack:** Webhook → Parser → Supabase → Notificações (Email/WhatsApp)

---

### 5. Lead Capture SDR
**Arquivo:** `05-lead-capture-sdr.json`

Captura e qualifica leads automaticamente, encaminhando apenas os prontos para o time comercial.

**Fluxo:**
1. Recebe lead de formulário/landing page
2. Enriquece dados (empresa, cargo, tamanho)
3. Pontua lead (scoring baseado em critérios)
4. Se qualificado: agenda reunião ou envia para CRM
5. Se não qualificado: entra em nurturing

**Stack:** Webhook → Enrichment API → AI Scoring → CRM/Calendar

---

### 6. CRM Subworkflow
**Arquivo:** `06-crm-subworkflow.json`

Subworkflow reutilizável para operações comuns de CRM.

**Operações:**
- Criar/atualizar contato
- Registrar interação
- Atualizar pipeline/stage
- Criar tarefa de follow-up

**Stack:** Supabase → Merge → Update Operations

---

## 🚀 Projetos em Produção

Para documentação completa de projetos reais em produção, veja:

- **[MVM - Sistema de Recuperação de Vendas](../projetos/mvm/README.md)**  
  Sistema completo com IA conversacional, CRM customizado e recuperação de 15-25% dos carrinhos abandonados.

---

## 💡 Como Usar

1. Baixe o arquivo JSON do template desejado
2. Importe no seu n8n (Settings → Import Workflow)
3. Configure as credenciais (OpenAI, Supabase, etc.)
4. Ajuste os prompts e parâmetros para seu caso de uso
5. Teste com dados de exemplo antes de colocar em produção

---

**Desenvolvido por:** Isaac Silveira  
**Contato:** izack07@gmail.com
