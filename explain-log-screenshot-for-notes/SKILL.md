---
name: explain-log-screenshot-for-notes
description: Answers a question about a security log screenshot, SIEM table or lab finding in at most two Ukrainian sentences with English technical terms, ready to paste into Obsidian notes. Use whenever the user shares a screenshot from Kibana/Elastic, Splunk, Sentinel, CloudTrail, M365/o365 audit logs or a lab write-up and asks "чому", "що означає", "чим підозрілий", "поясни це поле", "чому тут X", "why is X suspicious", or wants a short answer for their notes. Prefer this over doc-answer when the answer comes from reading the logs, not from quoting vendor documentation. Do not use for live incidents that need a full investigation, or when the user explicitly asks for a detailed breakdown or doc quotes.
---

# Explain a security log screenshot in two sentences

The user studies SOC/DFIR labs and pastes answers straight into Obsidian. A long answer with intros, bullets, verification steps and source links is useless there. They need one concrete answer they can reread months later and still recognize the pattern.

## Build the answer

1. Read the screenshot and find the exact rows, fields and values that answer the question. If lab text is in the conversation, trust its facts (for example, which IP is the known corporate IP) over your own guesses.
2. Use these parts in this order and skip any that don't apply:
   - **Before**: what the value looked like earlier (time + value).
   - **Change**: what changed (time + field + new value).
   - **Why abnormal**: one plain reason the new value doesn't fit normal user behavior.
   - **What happened next**: the follow-up action in the logs, if visible.
3. Fit it into two sentences at most. Cut hedges and filler before cutting concrete values.

Concrete times, IPs and field values matter most, because they let the user spot the same pattern in a new case. The "what happened next" part turns a guess into a finding.

If the question is about what a field means in general (not what this screenshot shows), give the meaning in plain words in the first sentence and apply it to the screenshot in the second. Don't quote docs or add a URL unless the user asks.

If the screenshot can't answer the question, say so in one sentence and name the field or log that would answer it.

## Style

- Ukrainian prose. Field names, operations, products and common terms stay in English (OWA, user agent, AiTM, New-InboxRule, o365.audit.AppId). Never translate a term literally if analysts say it in English.
- Active voice. Say who did what: "хтось виконав Set-Mailbox", not a passive form.
- No headers, bullets, bold, metaphors, intro phrases or source line.
- Don't join two sentences with a dash or a colon.
- For a follow-up question, keep the same short style unless the user asks for more detail.

## Examples

The values below are made up for illustration (documentation IP ranges).

**Question:** "чому тут owa підозрілий" + screenshot of o365 MailItemsAccessed rows

**Answer:**
До 00:25 jdoe відкривав OWA з корпоративної IP 198.51.100.25, а о 00:28 OWA з повним браузерним user agent прийшов уже з хмарної IP 203.0.113.185. Звичайний користувач не працює з датацентру, а атакуючі часто заходять з хмарних VM або через AiTM-проксі, і через 1–3 хвилини хтось виконав з акаунта jdoe Set-Mailbox і створив New-InboxRule.

**Question:** "чому тільки ipv6 мають o365.audit.AppId" + same screenshot

**Answer:**
AppId з'являється, коли скриньку читає застосунок або сервіс, а не людина через браузер, тому його мають фонові сервіси Microsoft з IPv6-адрес. IPv6 тут лише збіг, бо з хмарної IP 203.0.113.185 хтось заходив через OWA, і там AppId порожній.

**Avoid:** an intro paragraph, five bullets, a "як перевірити" section and a source URL. That was the old long style.
