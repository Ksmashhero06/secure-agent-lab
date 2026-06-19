# Secure Agent Lab: Shopping Assistant

This repository contains the **Shopping Assistant** agent developed under Unit 4 of the Google AI Agents Intensive course. The agent is built with the Agent Development Kit (ADK) and includes rigorous security guardrails, vulnerability scanning, and testing.

## 🚀 Overview

The **Shopping Assistant** is designed to assist users with shopping tasks, such as redeeming discount codes, cart checkouts, and loyalty points administration.

To transition this from a simple prototype to an enterprise-grade agent, the codebase is hardened against malicious tool usage, guest privilege escalation, and credential leaks.

## 🔒 Security Architectures & Guardrails

We performed a formal **STRIDE Threat Modeling** analysis (documented in `shopping-assistant/threat_model.md`) and implemented the following mitigations:

1.  **Authorization Controls:**
    *   **Guest Access Prevention:** Guests (prefixed with `guest_`) are restricted from administrative actions (e.g. updating discount status) and earning loyalty points.
    *   **Admin Verification:** Sensitive tools require verified administrator credentials (`admin-001`).
2.  **Single-Use Discount Enforcement:**
    *   The `redeem_discount` tool validates if a code has already been redeemed by a specific user to prevent replay attacks and double-discount exploitation.
3.  **Local Static Scanning (Pre-commit hooks):**
    *   Configured local `pre-commit` hooks containing static checks (via `Semgrep`) that scan the codebase for hardcoded secrets or credentials (e.g., Gemini API keys starting with `AIzaSy`) and intercept commits containing leaks.

## 🧪 Security & Unit Testing

The agent's tool boundaries are fully validated with `pytest`. Unit tests under `shopping-assistant/tests/test_agent.py` cover:
*   Guest user exclusion from loyalty points.
*   Single-use gating of discount code redemption.
*   Access controls on administrative tools.

To run the test suite:
```powershell
cd shopping-assistant
uv run pytest
```

## 💻 Running the Agent

Start the local ADK Dev UI to interact with the agent:
```powershell
cd shopping-assistant
uv run adk web app --host 127.0.0.1 --port 8084
```
Access the interface in your browser:
*   **Dev UI:** `http://127.0.0.1:8084/dev-ui/?app=app`

---

## 👤 Author & Featured Projects

### Sathiyamoorthi K (Ksmashhero)
*B.Tech Information Technology Student (2027 Batch) | Aspiring Software Engineer & AI Developer*

*   🌐 **LinkedIn:** [Sathiyamoorthi K](https://www.linkedin.com/in/sathiyamoorthi-k-336a79307/)
*   💻 **GitHub:** [@Ksmashhero06](https://github.com/Ksmashhero06/)
*   📸 **Instagram:** [@kkssathiyamoorthi06](https://www.instagram.com/kkssathiyamoorthi06/)

---

### 🇮🇳 Featured Project: India's Voice of Justice
*   **Repository Link:** [Ksmashhero06/India-s-Voice-of-Justice](https://github.com/Ksmashhero06/India-s-Voice-of-Justice)
*   🏆 **Tamil Nadu State-Level Selection (Niralthiruvizha 3.0 / Villupuram Cohort)**: Selected and enrolled in the Wadhwani Foundation Learning & Entrepreneurship program.
*   **Overview:** An AI-powered multilingual legal assistance platform designed to simplify access to legal information for Indian citizens. Uses Retrieval-Augmented Generation (RAG), FastAPI, React, FAISS vector search, HuggingFace multilingual embeddings, and Google Gemini AI to provide structured legal guidance, complaint drafting, and legal awareness in multiple Indian languages.

