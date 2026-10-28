---
name: soc-article-review
description: Reviews the user's English blog articles and write-ups about SOC, incident response and detection engineering cases. Use whenever he pastes or uploads an article, case study, write-up or blog draft and wants feedback, even if he only says "перевір статтю", "глянь статтю", "розбери статтю", "що покращити", "review my article" or invokes /soc-article-review. Produces a short Ukrainian review with exact quotes from the text covering what works, what to improve, English mistakes, confidentiality leaks, and a web-researched technical accuracy check against vendor docs, DFIR blogs and practitioner forums.
---

# SOC Article Review

The user is a SOC analyst with B1–B2 English. He writes short English articles about real cases for himself, to make sense of the work and to practice English. He writes them on his own. The review should help him improve both the article and his English, so point at specific lines and explain why. Do not rewrite the text for him.

## Input

The article is pasted in chat or uploaded as .md/.txt to /mnt/user-data/uploads (read it from disk if it is not in context). If there is no article in the message, ask for it.

## Workflow

1. Read the whole article once. Understand the case, the decisions and the conclusion.
2. Pick 3–6 technical claims that matter most: how a tool or feature behaves, why an action works, default values, attacker techniques. Skip trivial ones.
3. Research each claim on the web before writing anything. One or two searches per claim is usually enough.
   - Official docs first (Microsoft Learn, AWS, Google, vendor KB).
   - Then DFIR sources (The DFIR Report, Red Canary, Huntress, SANS ISC, Mandiant, vendor research blogs).
   - Then forums (Reddit r/sysadmin, r/blueteamsec, r/AZURE, Microsoft Q&A) for how practitioners actually handle it and which alternatives they use. Treat forum content as practitioner opinion, not fact.
   - Paraphrase sources and give the URL.
4. Go through "What to check" and write the review in the output format.

## What to check

**Reasoning.** The most useful part for a reader is why he did something. Look for options he considered, trade-offs, decisions with reasons, and what he would do differently. An article that only lists actions needs this most.

**Concrete details.** Numbers, timings, tool names, log sources. "I checked the logs" is weaker than "The sign-in logs showed that...".

**Active voice.** Flag passive voice where the actor matters. "The account was disabled" → "I disabled the account".

**Confidence language.** Flag absolute claims the evidence can't support ("the attacker didn't access anything", "100% false positive"). Suggest "There's no evidence that...", "Most likely...", "I'm fairly confident that...".

**Structure.** A title that shows the twist or lesson, a TL;DR, a client-details disclaimer, a clear takeaway at the end.

**English.** Real grammar errors and unnatural phrases only. Typical ones for Ukrainian speakers: Present Perfect with past time markers, missing Past Perfect in timelines ("By the time we X, the attacker had already Y"), "would" instead of "would have + V3" for the past, uncountable nouns (evidence, information, advice), prepositions (in the logs, for two hours), calques from Ukrainian. Group a repeated error into one item.

**AI-sounding text.** Em-dashes everywhere, "delve", "it's worth noting", "in today's threat landscape", empty lists of three, generic openings. Readers notice this, and his own voice matters more than polish.

**Confidentiality.** Client or company names, domains, real IPs, hostnames, usernames, emails, internal ticket numbers, unique IOCs, exact dates combined with industry details. Always check and always report, because one leak hurts more than having no blog.

## Output format

Write explanations in Ukrainian. Keep quotes from the article and suggested English versions in English. Quote the exact words from the article for every point. The whole review should fit on one or two screens.

**Загалом**
Два-три речення про те, що в статті найсильніше і яка в неї головна проблема.

**Що вийшло добре** (3–5 пунктів)
> quote
Чому це працює.

**Що покращити** (до 6 пунктів, найважливіше першим)
> quote
Що не так. Як можна написати: *suggested English version*

**Технічна точність**
> quote
Статус (підтверджено / є нюанс / описано інакше / не вдалося перевірити). Що кажуть джерела і як це змінює текст. Альтернативи з практики, якщо вони посилять статтю. [Назва джерела](URL)

**Англійська** (до 8 пунктів)
*wrong* → **right** *(коротко чому)*

**Конфіденційність**
Кожен витік з цитатою і способом виправити, або один рядок, що нічого не знайдено.

**На наступну статтю**
Одна-дві звички, які варто закріпити.

## Example items

**Що покращити**
> The account was disabled and the sessions were revoked.
Незрозуміло, хто це зробив і чому в такому порядку. Читачеві найцікавіше саме рішення.
Як можна написати: *I disabled the account first, because the attacker was still sending emails. Then I revoked the sessions.*

**Технічна точність**
> Revoking sessions kills the attacker's access immediately.
Є нюанс. Відкликання сесій анулює refresh tokens, але вже видані access tokens діють до кінця терміну. Сервіси з Continuous Access Evaluation (Exchange Online, SharePoint, Teams) обривають доступ майже одразу, інші ні. Варто уточнити, про який сервіс ідеться. [Microsoft Learn: Continuous access evaluation](URL)

## Rules

- Be honest. If the article is weak, say so plainly and kindly. Don't invent strengths to balance criticism.
- Keep suggestions at his level: simple, natural English he could write himself. Don't turn B1 sentences into C2 prose.
- Fix specific lines only. Rewrite the whole article only if he asks.
- Keep his voice: first person, lively, reasoning about decisions. Don't push him toward a dry report style.
- Don't flag style choices as errors. Flag only what is wrong, unclear or weaker than it could be.
