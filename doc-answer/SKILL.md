---
name: doc-answer
description: Answer user questions by searching official documentation and providing verified answers with exact quotes and source URLs. Use this skill whenever the user asks a factual question about a product, service, technology, framework, or standard and expects an answer grounded in official docs — not from memory. Trigger phrases include "what does the docs say about", "find in the documentation", "answer from the docs", "quote from the article", "what does [product] documentation say", or any question where the user pastes a URL or article title and asks for specific information from it. Also trigger when the user asks a series of study/exam questions and wants doc-backed answers, or when the user says "answer like last time" referring to a previous doc-grounded answer. Works for any vendor or technology — Microsoft, AWS, Google Cloud, Elastic, CrowdStrike, Kubernetes, etc.
---

# Doc Answer Skill

Answer user questions using official documentation as the single source of truth. Every claim must be backed by an exact quote from a real document with a working source URL.

## Core Workflow

1. **Understand the question.** Identify the product/technology, the specific concept, and what exactly the user wants to know.

2. **Find the right documentation page.**
   - If the user provided a URL → fetch that page directly.
   - If no URL → search for the official documentation page using targeted queries like `site:learn.microsoft.com "suppression rules"` or `site:docs.aws.amazon.com "S3 lifecycle"`.
   - Always prefer primary vendor documentation over blogs, forums, or third-party sites.
   - If the first search doesn't find the right page, refine the query and try again (up to 3 attempts).

3. **Extract the answer with exact quotes.**
   - Read the documentation page content.
   - Find the specific paragraph(s) that answer the question.
   - Quote the relevant text **exactly as written** — do not paraphrase the quote itself.
   - Keep quotes concise: prefer 1-3 sentences that directly answer the question. Do not quote entire sections.

4. **Format the response.**

## Response Format

Every answer MUST follow this structure:

```
From the documentation:

> "[exact quote from the page]"

[Brief explanation in the user's language if needed — what this means in practical terms, exam context, or comparison with other concepts.]

Source: [full URL of the page]
```

## Rules

### Quoting
- Quotes must be **character-for-character identical** to the source text. Do not rephrase, reorder, or merge sentences from different paragraphs into one quote.
- If the answer requires information from multiple places on the same page, use separate quotes with a brief connector between them.
- If the answer requires information from multiple pages, provide separate quote blocks with separate source URLs.
- Bold key phrases inside quotes using **bold** to highlight the most important part for the user.

### Source URLs
- Every quote must have a source URL.
- URLs must be real and link to the actual page where the quote appears.
- Prefer canonical English-language URLs (e.g., `learn.microsoft.com/en-us/...` not `learn.microsoft.com/ro-ro/...`).
- Do not construct URLs from memory — only use URLs found via search or fetch.

### When information is NOT found
- If the documentation does not contain an answer to the question, say so explicitly: "I searched [URL] and this specific information is not covered on this page."
- Suggest alternative search terms or related pages if available.
- Never fabricate quotes or URLs.

### Multi-question sessions
- When the user asks multiple questions about the same topic (e.g., exam study session), maintain the same format for each answer.
- If all answers come from the same page, state the source once at the end with a note: "All quotes above are from: [URL]"
- Track which questions have been answered and which remain.

### Language
- Quotes are always in the **original language of the documentation** (usually English).
- Explanations and connectors can be in the **user's preferred language**.
- Technical terms stay in English regardless of explanation language.

## Examples

### Example 1: Single question, single source

User: "What is a suppression rule in MDE?"

Response:
From the documentation:

> "You can create suppression rules for specific alerts that are **known to be innocuous** such as known tools or processes in your organization."

This means suppression rules hide or auto-resolve alerts you know are safe — like a legitimate admin tool that triggers a detection.

Source: https://learn.microsoft.com/en-us/defender-endpoint/manage-suppression-rules

### Example 2: Question with two relevant quotes from same page

User: "What happens when you hide vs resolve an alert with a suppression rule?"

Response:
From the documentation:

**Hide:**
> "Alerts that are marked as hidden will be **suppressed from the entire system**, both on the device's associated alerts and from the dashboard and **won't be streamed across Defender for Endpoint APIs**."

**Resolve:**
> "Alerts that are automatically resolved will appear in the **resolved section** of the alerts queue, alert page, and device timeline and will appear as **resolved across Defender for Endpoint APIs**."

The difference: resolve keeps the alert visible but closed; hide removes it completely — even from API streams.

Source: https://learn.microsoft.com/en-us/defender-endpoint/manage-alerts

### Example 3: Information not found

User: "Does the suppression rule page mention machine learning exclusions?"

Response:
I searched https://learn.microsoft.com/en-us/defender-endpoint/manage-suppression-rules and this specific information is not covered on this page. The page only covers manual suppression rules based on IoC conditions.

You might find ML-related exclusions in the Automated Investigation documentation instead.
