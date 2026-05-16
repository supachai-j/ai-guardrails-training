---
source_type: doc
source_url: https://github.com/supachai-j/guard-demo-client/blob/main/designdocs/DESIGN_OVERVIEW.md
ingested_at: 2026-05-16
title: Agentic Demo - Design Overview (guard-demo-client design docs)
---

# Agentic Demo – Design Overview
_Last updated: 2025-08-27_

This document summarizes the product vision and feature set for the **Agentic Demo** used by Sales for local demos.

## Objectives
- Skinnable B2B landing page + chatbot.
- Admin console to configure branding, LLM, **Lakera**, **RAG (upload + AI-generated seed packs)**, and tools via **ToolHive (MCP)**.
- Export/Import JSON skins for easy sharing across laptops.

## Key Features
- **Lakera Guard** toggle + overlay (overall status, per-guardrail results, raw JSON view)
- **RAG Upload** (PDF/MD/TXT/CSV ≤10MB) and **AI-Generated Seed Packs** (industry + prompt → synthetic markdown → preview → ingest to Chroma)
- Tooling via **ToolHive** and starter mock tools: Calculator, HTTP Fetch, Calendar Lookup, GitHub Repo Info
- Model selection dropdown with editable list of OpenAI models

## Stack
- Frontend: Vite + React + TypeScript + Tailwind
- Backend: FastAPI + SQLite + Chroma
- LLM: OpenAI (chat + tools); simple ReAct agent; optional LangGraph scaffold
