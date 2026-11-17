---
name: argument-analysis
description: Evaluate an argument end to end by asking a fixed sequence of critical questions — issue and conclusion, reasons, ambiguous words, value and descriptive assumptions, fallacies, evidence, rival causes, statistics, omitted information, and reasonable alternative conclusions. Use when asked to critique, assess or "think critically about" an article, proposal, RFC, design doc, pitch, vendor claim, research summary, AI-generated answer, or any text that tries to persuade.
---

# argument-analysis

Read like a gold panner, not a sponge. A sponge absorbs everything it reads; a panner keeps asking questions and keeps only what survives them. The aim is not to win against the author, but to decide what is worth believing and acting on.

Apply the same standard to arguments you like as to arguments you dislike. Critical thinking used only against the other side is the weak kind.

## The questions, in order

Work through them in sequence; each one builds on the last. Write short answers, citing the text.

### 1. What are the issue and the conclusion?
- **Issue**: the question the text is answering. Is it descriptive ("what is / was / will be true?") or prescriptive ("what should we do?").
- **Conclusion**: the claim the author wants you to accept. Look for it in the title, opening and closing, and after words like *therefore, so, thus, this shows, we should*.
- If you can't find a conclusion, there is nothing to evaluate yet — say so.

### 2. What are the reasons?
- List each reason offered for the conclusion: beliefs, evidence, analogies, principles. Look after *because, since, given that, studies show*.
- Lay the structure out explicitly: `Reason 1 → Reason 2 → Conclusion`. Reasons come first: a conclusion without reasons is an opinion, not an argument.

### 3. What words or phrases are ambiguous?
- Find the key terms in the issue, reasons and conclusion — especially abstract ones (*secure, scalable, fair, simple, productive, best practice*).
- For each, ask: could it reasonably mean two different things, and would the argument's strength change depending on which? If yes, the argument can't be judged until it's pinned down.

### 4–5. What are the assumptions? (use `assumption-finder` for depth)
- **Value assumptions**: which value does the author rank above another (e.g. speed over safety, autonomy over consistency)?
- **Descriptive assumptions**: what unstated beliefs about how the world *is* must be true for the reasons to support the conclusion?

### 6. Are there fallacies in the reasoning? (see `fallacy-check`)
Check whether any reason depends on a flawed assumption, a diversion, or a trick such as begging the question.

### 7. How good is the evidence? (see `evidence-check`)
Classify each factual claim by its source (intuition, personal experience, examples, testimonials, authority, observation, research, analogy) and judge how dependable it is.

### 8. Are there rival causes? (see `rival-causes`)
Whenever the argument claims X caused Y, list other plausible explanations.

### 9. Are any statistics deceptive? (see `evidence-check`)
Check what the numbers actually measure, which average is used, missing baselines, and whether the numbers prove the conclusion or something nearby.

### 10. What significant information is omitted?
Every argument is incomplete, and a coherent story feels convincing however little information it rests on. Ask what would change your judgment if you knew it:
- the strongest counterarguments and contrary evidence,
- other definitions of key terms,
- other values or perspectives,
- where the "facts" came from,
- the actual numbers behind words like *most, many, significant, faster*,
- costs, side effects, long-term or second-order effects,
- who benefits from the conclusion being accepted.

### 11. What reasonable conclusions are possible?
- Avoid either/or framing. List several conclusions the same reasons could support.
- Use **if-clauses**: "If the priority is cost, then A; if it is reliability, then B."
- State which conclusion is best supported, and how strongly.

## Output

```markdown
**Issue:** …
**Conclusion:** …
**Reasons:** 1) … 2) …
**Ambiguities:** term — readings — does it matter?
**Assumptions:** value: … / descriptive: …
**Fallacies:** …
**Evidence quality:** claim — source type — strength
**Rival causes / statistics:** …
**Omitted:** …
**Reasonable conclusions:** if …, then …
**Verdict:** what to accept, reject, or hold until more is known — and what would change your mind.
```

Keep the tone fair. Name strengths as well as weaknesses; acknowledge good reasoning wherever it appears.
