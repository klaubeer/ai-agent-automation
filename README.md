<div align="center">

# 🤖 Plataforma de Agente Conversacional com IA

**Agente de IA autônomo construído inteiramente no n8n — integrando LLMs, RAG, processamento multimodal e automação de workflows empresariais via WhatsApp.**

[![n8n](https://img.shields.io/badge/Orquestração-n8n-EA4B71?style=flat-square&logo=n8n&logoColor=white)](https://n8n.io)
[![Supabase](https://img.shields.io/badge/Banco_de_Dados-Supabase-3ECF8E?style=flat-square&logo=supabase&logoColor=white)](https://supabase.com)
[![Redis](https://img.shields.io/badge/Cache-Redis-DC382D?style=flat-square&logo=redis&logoColor=white)](https://redis.io)
[![WhatsApp](https://img.shields.io/badge/Canal-WhatsApp-25D366?style=flat-square&logo=whatsapp&logoColor=white)](https://whatsapp.com)

</div>

---

## Visão Geral

Este projeto é um **agente de IA totalmente autônomo** que roda como um conjunto de workflows no n8n — sem backend customizado. O agente conduz interações completas com clientes via WhatsApp: qualifica leads, responde perguntas a partir de uma base de conhecimento da empresa, agenda compromissos e registra cada interação automaticamente.

A arquitetura combina **raciocínio via LLM**, **RAG com busca vetorial nativa**, **memória de sessão em Redis** e **chamada de ferramentas (tool calling)** — tudo orquestrado visualmente dentro do n8n.

---

## Arquitetura

```
WhatsApp (Usuário)
        │
        ▼
  Gateway de Mensageria
        │
        ▼
  Orquestrador n8n
        │
        ├─── Controle de Sessão (Redis)
        │         └─── Número do usuário → estado da sessão
        │
        ├─── Roteador de Intenção
        │
        ├─── Recuperação Híbrida
        │         ├─── Busca Vetorial (Supabase pgvector)
        │         └─── Memória Conversacional (Redis)
        │
        ├─── Raciocínio LLM + Tool Calling
        │         ├─── Google Calendar API
        │         ├─── Cadastro de Leads (Supabase / PostgreSQL)
        │         └─── APIs Externas
        │
        └─── Geração de Resposta
                  └─── Texto / Áudio / Imagem → WhatsApp
```

---

## O que o Agente Faz

### 🧠 Pipeline de RAG Completo

Documentos são ingeridos automaticamente do **Google Drive** e fontes internas, divididos em chunks, transformados em embeddings e armazenados como vetores no **Supabase (pgvector)**. Quando um usuário faz uma pergunta, o agente:

1. Gera o embedding da pergunta
2. Executa busca por similaridade semântica na base vetorial
3. Recupera os trechos mais relevantes
4. Ancora a resposta do LLM no conhecimento real da empresa

Nenhuma alucinação — cada resposta é fundamentada no contexto recuperado.

### 📋 Qualificação de Leads (AI SDR)

- Coleta e valida dados do cliente através de conversa natural
- Cria registros de usuário no PostgreSQL / Supabase automaticamente
- Registra dados estruturados de interação para integração com CRM
- Conduz o fluxo completo de qualificação sem intervenção humana

### 📅 Agendamento Inteligente

- Verifica disponibilidade em tempo real via **Google Calendar API**
- Agenda, confirma e reagenda compromissos de forma autônoma
- Envia mensagens de confirmação de volta ao usuário

### 💬 Sessão e Memória Conversacional

- Cada número de WhatsApp possui sua própria sessão isolada no **Redis**
- O histórico da conversa é mantido ao longo de múltiplas mensagens
- O agente reconstrói o contexto mesmo quando mensagens chegam fragmentadas (padrão comum no WhatsApp)
- Sessões expiram automaticamente após inatividade

### 🖼️ Processamento Multimodal

O agente compreende e processa:

| Tipo de Entrada | Processamento |
|---|---|
| Texto | Processamento direto pelo LLM |
| Áudio | Transcrição → pipeline de texto |
| Imagens | Análise via modelo de visão |
| Vídeo | Extração de frames + análise |

### 🪵 Log de Usuário e Auditoria

- Toda interação é registrada com timestamp, ID de sessão e conteúdo
- Perfis de usuário são criados no primeiro contato e enriquecidos ao longo do tempo
- Trilha de auditoria completa disponível no Supabase para análise e conformidade

---

## Stack Tecnológica

| Camada | Tecnologia |
|---|---|
| **Orquestração** | n8n (toda a lógica do agente reside aqui) |
| **LLM** | OpenAI / provedores compatíveis via nós de IA do n8n |
| **Base Vetorial** | Supabase pgvector |
| **Embeddings** | Hugging Face / OpenAI Embeddings |
| **Memória de Sessão** | Redis |
| **Banco Principal** | Supabase (PostgreSQL) |
| **Mensageria** | WhatsApp Business API |
| **Síntese de Voz** | ElevenLabs |
| **Calendário** | Google Calendar API |
| **Fonte de Documentos** | Google Drive |

---

## Decisões de Arquitetura

**Tudo no n8n** — toda a lógica do agente, incluindo ingestão de RAG, recuperação, chamadas ao LLM, execução de ferramentas e formatação de resposta, roda como workflows n8n. Isso torna o sistema visual, auditável e fácil de modificar sem necessidade de deploy de código.

**Supabase como backend unificado** — um único projeto Supabase gerencia a base vetorial (pgvector), dados relacionais (perfis de clientes, leads, logs) e serve como fonte única da verdade. Sem banco vetorial separado para administrar.

**Redis para isolamento de sessão** — usuários do WhatsApp são identificados pelo número de telefone. O Redis mapeia cada número para um contexto de sessão ativo, permitindo conversas multi-turno com estado em escala, sem overhead de banco de dados a cada mensagem.

**Tratamento de mensagens fragmentadas** — usuários do WhatsApp frequentemente enviam pensamentos em múltiplas mensagens rápidas. O agente armazena em buffer e reconstrói essas mensagens em um input coerente antes de processar, eliminando respostas fora de contexto.

---

## Fluxo de Ingestão RAG

```
Google Drive / Documentos Internos
            │
            ▼
     Workflow de Ingestão (n8n)
            │
            ├─── Parsing de Documentos
            ├─── Chunking (tamanho e overlap configuráveis)
            ├─── Geração de Embeddings
            └─── Upsert no Supabase pgvector
```

A ingestão roda por agendamento ou pode ser disparada manualmente. Novos documentos são detectados automaticamente.

---

## Resumo de Funcionalidades

| Funcionalidade | Status |
|---|---|
| Integração com WhatsApp | ✅ |
| RAG com pgvector | ✅ |
| Controle de sessão por número de telefone | ✅ |
| Criação de perfil e log de usuário | ✅ |
| Fluxo de qualificação de leads | ✅ |
| Agendamento via Google Calendar | ✅ |
| Multimodal (texto, áudio, imagem, vídeo) | ✅ |
| Memória de sessão com Redis | ✅ |
| Persistência de dados no PostgreSQL | ✅ |
| Orquestração completa no n8n (sem backend customizado) | ✅ |

---

## Como Começar

### Pré-requisitos

- Instância n8n (self-hosted ou cloud)
- Projeto Supabase com extensão pgvector habilitada
- Instância Redis
- Acesso à WhatsApp Business API
- Projeto no Google Cloud (APIs do Calendar e Drive)

### Configuração

1. **Clone** este repositório e importe os arquivos JSON de workflow no n8n
2. **Configure as credenciais** no n8n para Supabase, Redis, WhatsApp e APIs do Google
3. **Execute o workflow de ingestão** para popular a base vetorial com seus documentos
4. **Ative o workflow principal do agente** — o webhook estará ativo

Referência detalhada de variáveis de ambiente e configuração de credenciais em [`docs/setup.md`](docs/setup.md).

---
