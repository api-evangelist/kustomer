# Kustomer GraphQL Schema

## Overview

This document describes the conceptual GraphQL schema for the Kustomer AI-native CRM and customer service platform. Kustomer exposes a REST API at `https://api.kustomerapp.com` but this schema captures the full domain model across customers, conversations, messages, teams, queues, automation, reporting, and AI capabilities.

- **Provider:** Kustomer
- **Kind:** AI-powered Customer Service CRM
- **Developer Docs:** https://developer.kustomer.com/
- **Base URL:** https://api.kustomerapp.com
- **Auth:** Bearer token (API Key)

## Schema File

`kustomer-schema.graphql`

## Type Summary

| Category | Types |
|---|---|
| Customer | Customer, CustomerDetails, CustomerProfile, CustomerTimeline, TimelineEvent, CustomerAttr, CustomAttribute |
| Conversation | Conversation, ConversationDetails, ConversationStatus, ConversationTag, ConversationMeta |
| Message | Message, MessageDetails, MessageType, EmailMessage, ChatMessage, SmsMessage, VoiceMessage, InternalNote |
| Thread | Thread, ThreadDetails |
| Company | Company, CompanyDetails, CompanyAttribute |
| Team & Queue | Team, TeamDetails, Queue, QueueDetails, QueueAssignment |
| Automation | KBot, KBotFlow, KBotDetails, Workflow, WorkflowStep, WorkflowTrigger |
| SLA | SLAPolicy, SLADetails, SLABreach |
| Schedule | BusinessHour, BusinessSchedule |
| Taxonomy | Tag, TagGroup |
| Forms | Form, FormField, FormResponse |
| Snippets | Snippet, SnippetCategory |
| Reporting | Report, ReportFilter, Insight |
| AI | SentimentScore, AISuggestion, AIResponse |
| Auth | APIKey, Token, Webhook |

## Key Relationships

- A **Customer** has a **CustomerProfile**, **CustomerTimeline**, and multiple **Conversation** records.
- A **Conversation** contains **Thread** records, each with **Message** objects (EmailMessage, ChatMessage, SmsMessage, VoiceMessage, or InternalNote via union type).
- A **Conversation** is assigned to a **Team** and optionally a **Queue**.
- **SLAPolicy** is attached to a **Queue** or **Team** and generates **SLABreach** events when violated.
- **KBot** orchestrates automated flows via **KBotFlow** and **KBotDetails**.
- **Workflow** is triggered by **WorkflowTrigger** and executes **WorkflowStep** actions.
- **AISuggestion** and **AIResponse** are surfaced on Conversations and Messages.
- **Report** and **Insight** aggregate conversation and customer data filtered by **ReportFilter**.
- **Webhook** delivers real-time events for all major entity changes.

## Authentication

All queries and mutations require a valid bearer token passed as `Authorization: Bearer <token>`. Tokens are provisioned as **APIKey** objects scoped to specific roles and permissions.

## Pagination

List queries use cursor-based pagination with `first`, `after`, `last`, and `before` arguments returning a standard connection envelope with `edges`, `nodes`, and `pageInfo`.
