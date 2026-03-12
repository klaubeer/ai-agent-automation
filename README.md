# 🇧🇷 PT-BR

# AI Conversational Agent Platform

Plataforma de **Agentes Conversacionais baseados em Inteligência Artificial** para automação de atendimento, qualificação de leads, suporte ao cliente e execução de processos comerciais.

O projeto demonstra uma **arquitetura completa de IA aplicada**, combinando **LLMs, RAG avançado, automação de workflows e integração com sistemas externos**.

O agente atua como um **Agente Atendente**, capaz de conversar com usuários, acessar bases de conhecimento da empresa, consultar sistemas internos e executar ações automaticamente.

---

# Arquitetura do Sistema

Fluxo de alto nível da arquitetura:

```
Usuário (WhatsApp)
↓
Gateway de Mensageria
↓
Workflow Orchestrator (n8n)
↓
Processamento de intenção
↓
Hybrid Retrieval (Vector Search + Context Memory)
↓
Seleção de contexto
↓
LLM Reasoning
↓
Execução de Tools / APIs
↓
Geração da resposta
↓
Resposta + Fontes
```

A arquitetura combina:

* LLM reasoning
* recuperação semântica (RAG)
* execução de ferramentas
* automação de processos

Permitindo que o agente funcione como uma **interface inteligente para sistemas empresariais**.

---

# Pipeline de RAG

O sistema implementa um pipeline completo de **Retrieval Augmented Generation**.

### Ingestão automática de conhecimento

Documentos são carregados automaticamente de:

* Google Drive
* bases internas
* arquivos empresariais

O pipeline realiza:

```
Documentos
↓
Parsing
↓
Chunking
↓
Embeddings
↓
Vector Storage
```

---

### Banco vetorial

Os embeddings são armazenados no **Supabase Vector Database**, permitindo:

* busca semântica
* recuperação contextual
* grounding das respostas

---

### Processo de recuperação

Quando o usuário faz uma pergunta:

```
Pergunta do usuário
↓
Embedding da pergunta
↓
Busca semântica no vetor database
↓
Recuperação dos documentos mais relevantes
↓
Seleção de contexto
↓
Envio para o LLM
↓
Resposta baseada em conhecimento real
```

---

# Funcionalidades do Agente

## AI SDR (Qualificação de Leads)

* qualificação automática de leads
* coleta de dados do cliente
* criação de cadastro
* integração com CRM

---

## Atendimento ao Cliente

* respostas automáticas via RAG
* acesso à base de conhecimento da empresa
* suporte pós-venda
* resolução de dúvidas frequentes

---

## Agendamento Inteligente

Integração com **Google Calendar** para:

* verificação de disponibilidade
* criação automática de compromissos
* confirmação de agendamentos

---

## Memória Conversacional

Utiliza **Redis** para manter memória de sessão:

* contexto da conversa
* histórico de interações
* continuidade do atendimento

---

## Processamento Multimodal

O agente suporta:

* texto
* áudio
* imagens
* vídeos

Com processamento automático de mídia.

---

## Inteligência de Conversa

O sistema trata particularidades do WhatsApp:

* mensagens fragmentadas
* envio múltiplo de mensagens
* reconstrução de contexto da conversa

---

# Banco de Dados

O sistema utiliza **Supabase** como backend principal.

Armazena:

* cadastro de clientes
* histórico de conversa
* leads
* logs de interação

---

# Orquestração de Workflows

Toda a lógica do sistema é orquestrada por **n8n**.

O n8n gerencia:

* automações
* integrações com APIs
* pipelines de IA
* execução de ferramentas

---

# Stack Tecnológica

### Inteligência Artificial

* Large Language Models
* AI Agents
* Prompt Engineering
* Tool Calling

---

### Retrieval

* RAG (Retrieval Augmented Generation)
* Embeddings
* Vector Search

---

### Backend

* Python
* Redis
* Supabase

---

### Automação

* n8n
* Webhooks
* REST APIs

---

### Integrações

* WhatsApp APIs
* Google Drive
* Google Calendar
* Hugging Face
* ElevenLabs

---

# Características da Arquitetura

✔ Agente conversacional baseado em LLM
✔ Pipeline RAG completo
✔ Integração com WhatsApp
✔ Memória de conversação
✔ Processamento multimodal
✔ Automação de processos empresariais
✔ Integração com sistemas externos
✔ Arquitetura escalável

---

# 🇺🇸 English Version

# AI Conversational Agent Platform

AI-powered conversational agent platform designed to automate **customer support, lead qualification, scheduling, and operational workflows**.

This project demonstrates a **production-grade conversational AI architecture**, combining **LLMs, advanced RAG pipelines, workflow automation, and messaging platform integrations**.

The agent functions as an **AI SDR and operational assistant**, capable of interacting with users, accessing company knowledge bases, and executing actions in internal systems.

---

# System Architecture

High-level architecture flow:

```
User (WhatsApp)
↓
Messaging Gateway
↓
Workflow Orchestrator (n8n)
↓
Intent Processing
↓
Hybrid Retrieval (Vector Search + Context Memory)
↓
Context Selection
↓
LLM Reasoning
↓
Tool / API Execution
↓
Response Generation
↓
Answer + Sources
```

The architecture combines:

* LLM reasoning
* semantic retrieval
* tool execution
* workflow automation

This allows the system to act as an **AI-powered interface for enterprise systems**.

---

# RAG Pipeline

The system implements a full **Retrieval Augmented Generation pipeline**.

### Knowledge ingestion

Documents are automatically loaded from:

* Google Drive
* internal knowledge bases
* company documentation

Processing pipeline:

```
Documents
↓
Parsing
↓
Chunking
↓
Embeddings
↓
Vector Storage
```

---

### Vector database

Embeddings are stored in **Supabase Vector Database**, enabling:

* semantic search
* contextual retrieval
* grounded responses

---

### Retrieval flow

When a user asks a question:

```
User Query
↓
Query Embedding
↓
Semantic Vector Search
↓
Relevant Document Retrieval
↓
Context Selection
↓
LLM Generation
↓
Answer grounded in retrieved knowledge
```

---

# Agent Capabilities

## AI SDR

* automated lead qualification
* customer data collection
* contact registration
* CRM integration

---

## Customer Support

* FAQ automation using RAG
* company knowledge retrieval
* post-sale support
* information queries

---

## Intelligent Scheduling

Integration with **Google Calendar** for:

* availability checking
* automated appointment booking
* scheduling confirmation

---

## Conversation Memory

The system uses **Redis session memory** to maintain context:

* conversation history
* follow-up questions
* persistent session state

---

## Multimodal Processing

The agent can process:

* text messages
* audio
* images
* videos

---

## Messaging Intelligence

The system handles messaging platform quirks such as:

* fragmented messages
* multi-message input
* conversation reconstruction

---

# Database Layer

The system uses **Supabase** as its primary database.

Stored data includes:

* customer profiles
* conversation logs
* leads
* interaction history

---

# Workflow Orchestration

The system is orchestrated using **n8n workflows**.

n8n manages:

* agent orchestration
* automation pipelines
* external integrations
* tool execution

---

# Tech Stack

### AI

* Large Language Models
* AI Agents
* Prompt Engineering
* Tool Calling

---

### Retrieval

* Retrieval Augmented Generation
* Embeddings
* Vector Search

---

### Backend

* Python
* Redis
* Supabase

---

### Automation

* n8n
* Webhooks
* REST APIs

---

### Integrations

* WhatsApp APIs
* Google Drive
* Google Calendar
* Hugging Face
* ElevenLabs

---

# Architecture Characteristics

✔ Conversational AI agent
✔ Full RAG pipeline
✔ WhatsApp automation
✔ Multimodal processing
✔ Conversation memory
✔ Enterprise workflow automation
✔ Tool execution
✔ Scalable architecture

Se quiser, eu também posso te gerar **um diagrama de arquitetura profissional (tipo big tech)** para colocar no README. Isso aumenta MUITO o impacto do GitHub.
