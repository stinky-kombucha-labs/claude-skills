---
name: obsidian-note-writer
description: >
  Convert screenshots of learning materials (textbook pages, slides, whiteboard photos,
  handwritten notes, app screenshots) into clean Obsidian-ready markdown files. Use this
  skill whenever the user uploads an image of educational content and asks to "зробити md",
  "занести в обсидіан", "зроби нотатку", "конспект", "write a note", or any variation of
  wanting a markdown note from visual material. Also trigger when the user uploads a
  screenshot and mentions Obsidian, vault, or note-taking in any language. Covers any
  subject — English grammar, Slovak, certifications, cybersecurity, programming, etc.
  Always use this skill even if the user just drops a screenshot without explicit
  instructions but the context implies they want an Obsidian note.
---

# Obsidian Note Writer

Converts screenshots of learning materials into compact, Obsidian-ready `.md` files
matching the user's personal note-taking style.

## Core Principles

1. **One screenshot = one topic = one file.** If the user uploads multiple images, ask
   whether they are separate topics or one lesson before combining. Never assume they
   belong together.

2. **Compact over comprehensive.** The user's notes are short — formula, markers, a few
   examples, key rule bolded. No filler text, no lengthy explanations, no tables unless
   the source material is itself a table.

3. **Only what's on the screen.** Do not add information that isn't in the screenshot.
   Do not invent extra examples, extra vocabulary, or extra rules. If the screenshot
   shows 3 examples, the note has 3 examples.

4. **Ukrainian meta-language.** Section headers, short explanations, and annotations
   are in Ukrainian. The learning content stays in its original language (English terms
   stay English, Slovak stays Slovak, etc.).

## Formatting Rules

### Structure

```
# Topic Name

##Section (if needed)

Rule or formula in **bold**.

Examples as plain lines, key parts in **bold**.
```

### What to use

- `**bold**` for key grammar points, formulas, important terms, rules
- `*italic*` for short clarifying notes in parentheses: *(однакові)*, *(заперечення)*
- Plain text lines for examples — no bullet lists for examples unless the source uses them
- Bullet lists (`-`) only when listing items of the same type (markers, keywords)
- Wikilinks `[[Other Note]]` only if the user explicitly asks or mentions related notes

### What NOT to use

- No `---` horizontal rules — never use them as section separators, they are distracting
- No space after `##` — write `##Section`, not `## Section`
- No emoji, no stickers, no callouts (`> [!tip]`)
- No tables unless the source material is literally a table
- No YAML frontmatter (unless user asks)
- No tags (unless user asks)
- No verbose explanations — one line per rule max
- No headers deeper than `##` — keep it flat
- No blockquotes for emphasis (only for short clarifying side-notes if needed)

## Workflow

### Step 1 — Read the screenshot

Look at the uploaded image. Identify:
- The topic (e.g. "Comparatives", "Past Simple", "Slovak Cases")
- What type of content it contains: rules, formulas, examples, vocabulary, tables
- How much content there is — this determines note length

### Step 2 — Extract content faithfully

Pull out exactly what's on the screen:
- Rules/formulas as they appear
- Examples as they appear
- Vocabulary/word lists as they appear
- Tables as they appear

Do NOT rephrase examples. Do NOT add your own examples. Do NOT expand abbreviations
into full explanations.

### Step 3 — Format as compact markdown

Apply the formatting rules above. The note should be roughly proportional to the
source material — a small screenshot = a short note, a dense screenshot = a longer note
but still compact.

### Step 4 — Name the file

Use the topic name in English, PascalCase or hyphenated:
- `Comparatives.md`
- `Present-Continuous.md`
- `Slovak-Cases-Nominativ.md`
- `Nmap-Scan-Types.md`

### Step 5 — Save and present

Save to `/mnt/user-data/outputs/<filename>.md` and present to the user.

## Examples

**Example 1 — English grammar screenshot with rules + examples:**

Input: Screenshot showing Present Perfect formula, markers, examples

Output:
```markdown
# Present Perfect

**have / has + V3 (past participle)**

Маркери: ever, never, just, already, yet, recently, so far, since, for

I **have visited** London. *(досвід)*
She **has just finished** her homework. *(щойно)*
We **haven't seen** this film yet. *(ще ні)*
**Have** you ever **been** to Japan? *(питання про досвід)*

**since** — з конкретного моменту: since 2020, since Monday
**for** — протягом періоду: for 3 years, for a long time
```

**Example 2 — Slovak vocabulary screenshot:**

Input: Screenshot with a list of Slovak words and translations

Output:
```markdown
# Slovak — Jedlo (їжа)

chlieb — хліб
maslo — масло
mlieko — молоко
syrok — сирок
vajce — яйце
mäso — м'ясо
ryba — риба
zelenina — овочі
ovocie — фрукти
```

**Example 3 — Certification study material screenshot:**

Input: Screenshot of network scan types from a security course

Output:
```markdown
# Nmap Scan Types

**-sS** — SYN scan (half-open), найшвидший, потрібен root
**-sT** — TCP connect, повне з'єднання, не потребує root
**-sU** — UDP scan, повільний
**-sV** — визначення версій сервісів
**-O** — визначення ОС

Комбінація: `nmap -sS -sV -O target`
```
