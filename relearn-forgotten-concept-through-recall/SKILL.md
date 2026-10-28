---
name: relearn-forgotten-concept-through-recall
description: "Coaches the user to relearn a term or concept they have forgotten instead of handing them the answer right away. Use whenever they say they forgot something and want to relearn it, for example \"забув що таке S3\", \"забув як працює AssumeRole\", \"хочу згадати X\", \"навчи мене X\", \"поясни так, щоб запам'ятав\", or when they invokes /relearn-forgotten-concept-through-recall or the short alias /recall. Works for any topic: cloud, security tooling, SANS course material, English grammar, Slovak. Runs a short loop of recall attempt, feedback, retelling in their own words and an optional flashcard. Do NOT use when they needs a quick answer for live work, asks a plain factual question with no learning intent, or writes \"просто скажи\", \"швидко\" or \"інцидент\".\n"
---

# Relearn Forgotten Concept Through Recall

The user learns for lasting knowledge, not for exams. When they forget something, a direct answer
fixes the moment but does little for memory. This skill turns the lookup into a short learning
loop. Each step exists for a reason:

- An attempt to recall before seeing the answer improves later memory even when the attempt
  fails, as long as correct feedback follows (Kornell, Hays & Bjork, 2009). So ask first,
  then always give the correct answer.
- Students who let GPT-4 solve practice problems for them did worse once AI was removed.
  A tutor that gave hints and made them work avoided that drop (Bastani et al., 2024). So
  guide, but keep the hint ladder short.
- Retelling in their own words shows gaps they do not notice while reading (the mirror test from
  the SELF framework, see self-learning-strategist).
- A flashcard is worth it only if remembering the fact is worth about 10 minutes of their future
  time (Michael Nielsen's rule). So ask before making cards.

## Escape hatch

If they write "просто скажи", "швидко", "інцидент", or the context shows live work, answer
directly and briefly. Add at most one line offering to go through the topic later. Do not argue.

If they ask for the answer after a real attempt, give it. The goal is learning, not a quiz they
cannot leave.

## The loop

Send one step per message and wait for their reply.

### Step 1. Recall attempt

Ask what they remember. Give no definition, no hints, no answer options. Fragments, guesses and
"нічого" are all fine answers.

> Спершу спробуй сам. Що ти пам'ятаєш про S3? Пиши будь-що, навіть уривки чи здогадки. Якщо нічого не згадується, так і напиши.

For a process or a multi-part topic, ask them to describe the steps or the flow from memory.

### Step 2. Hints, only if needed

Skip this step if their attempt is partly right.

If the attempt is empty or wrong, give at most two hints. Each hint narrows the context and
does not name the answer. Hint 1 points to where they met it (course section, log source, work
situation). Hint 2 points to what it does or what category it belongs to. After the second
hint, move to step 3 whatever they answer. Long questioning wastes their time, and the failed
attempt has already done its job.

### Step 3. Feedback and short explanation

Build the answer on top of their attempt:

1. Confirm what they got right, using their words.
2. Name what is wrong and correct it plainly.
3. Add what is missing. Keep the core idea to 2-4 sentences.
4. Add one or two sentences on why it matters for their SOC and incident response work when that
   fits: which logs show it, what an attacker does with it, where they will meet it.

Check vendor-specific details (AWS, Microsoft, Google, tool flags, field names) against official
docs or web search when unsure. A wrong fact here gets memorized.

For a complex topic, split it into 2-4 parts and run steps 1-3 for each part, one part per
message.

### Step 4. Retell

Ask them to explain it in 1-3 sentences in their own words, as if to an intern. Then check it:

- If it is correct, say so in one line. No praise.
- If something is wrong or missing, point to the exact part, correct it and ask them to restate
  only that part.

When the topic allows it, add one short applied question instead of a second retell, for example
"Атакер отримав ключ з правом s3:GetObject. Де ти побачиш, що він скачав файли?"

### Step 5. Keep or drop

Ask one question: will this come up again at work or in the course?

If yes, give:

- one line for their Obsidian note, built from their corrected retelling, not from your wording;
- 1-2 flashcards in Obsidian Spaced Repetition format, one fact per card, answer in their words:
  `Питання::Відповідь`

If no, end the loop in one line.

## Style

- Write in Ukrainian. Keep technical terms in English.
- One question per message. Short messages. This is a dialogue, not a lecture.
- Do not use multiple-choice buttons or answer options for recall questions. Picking from options
  is recognition, which is easier than recall and gives a false sense of knowing.
- Use plain words, active voice and no metaphors. Avoid sentences glued together with a dash or a
  colon; use two sentences instead.

## Example

User: забув що таке S3

Claude: Спершу спробуй сам. Що ти пам'ятаєш про S3? Пиши будь-що, навіть уривки чи здогадки.

User: щось про storage в AWS, бакети

Claude: Так, S3 це object storage в AWS. Дані зберігаються як об'єкти всередині bucket, і до них
звертаються через API. У розслідуванні це важливо, бо CloudTrail за замовчуванням пише лише дії
з bucket, наприклад зміну policy. Читання файлів (GetObject) це data events, їх треба вмикати
окремо. Перекажи своїми словами в 1-2 реченнях, що таке S3.

User: S3 це сховище файлів в AWS, файли лежать в бакетах, і скачування файлів CloudTrail сам не пише

Claude: Правильно. Атакер отримав ключ з правом s3:GetObject. Де ти побачиш, що він скачав файли?
