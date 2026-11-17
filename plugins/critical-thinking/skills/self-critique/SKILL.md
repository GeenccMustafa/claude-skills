---
name: self-critique
description: Apply strong-sense critical thinking to your own conclusion, recommendation, plan or draft — steelman the opposing view, check for thinking speed bumps (rushing, stereotypes, halo effect, belief perseverance, availability, answering the wrong question, egocentrism, wishful thinking), consider alternative conclusions, and rewrite so a critical reader can follow it. Use before committing to a decision or recommendation, before sending an important document, when the user asks "am I missing something", "poke holes in this", "play devil's advocate", or when Claude is about to give a confident recommendation on a contested question.
---

# self-critique

Weak-sense critical thinking defends what you already believe and attacks everything else. Strong-sense critical thinking turns the same questions on your own beliefs. Reasoning chosen to reach a conclusion you already wanted is managed reasoning, not thinking.

Hold conclusions firmly enough to act on them, and loosely enough to still ask: *might I be wrong?*

## 1. State your position plainly

Issue, conclusion, and your reasons — one line each. If you can't state them, you don't have an argument yet.

## 2. Run the critical questions on yourself

Use `argument-analysis` on your own position, paying special attention to:
- your **value assumptions** — what you are ranking higher, and who would rank it differently,
- your weakest **evidence** — would you accept it from someone you disagree with?,
- **rival causes** you haven't ruled out,
- **omitted information** — what you didn't look for.

## 3. Steelman the other side

Write the strongest case *against* your conclusion, as its best advocate would, not a straw version. Ask: what do they know or value that I am underweighting? If you can't make a convincing case, you probably don't understand the issue well enough yet.

## 4. Check the speed bumps

| Speed bump | Self-check question |
|---|---|
| **Thinking too quickly** | Did I decide before gathering the reasons? |
| **Stereotypes** | Am I judging a person, team, tool or idea by its group rather than its merits? |
| **Halo effect** | Am I trusting this because of something else I like about the source? |
| **Belief perseverance** | What evidence would change my mind — and have I looked for it? |
| **Availability** | Am I over-weighting a vivid or recent example (the last outage, one loud customer)? |
| **Answering the wrong question** | Did I swap the hard question for an easier one I could answer? |
| **Egocentrism** | Am I assuming others see, want or know what I do? |
| **Wishful thinking** | Would I reach the same conclusion if I didn't want it to be true? |
| **Discomfort with questioning** | Am I avoiding a question because the answer might be inconvenient? |

## 5. Consider alternative conclusions

Avoid either/or. List other reasonable conclusions and the conditions under which each would be right ("If the deadline is fixed, A; if quality matters most, B"). Decide whether your original conclusion still wins, should be narrowed, or should be dropped.

## 6. Rewrite for a critical reader

If the output is a document or recommendation:
- State the issue and conclusion up front.
- Give reasons with evidence, and name their sources.
- Define ambiguous key terms.
- Make your value priorities explicit.
- Acknowledge the strongest counterargument and rival explanations, and say why you still hold your view.
- State your confidence and what would change your mind.

## Output

```markdown
**Position:** …
**Strongest counter-case:** …
**Speed bumps found:** …
**Weakest links:** …
**Alternative conclusions:** if …, then …
**Revised position:** keep / narrow / change — confidence: high / medium / low
**What would change my mind:** …
```

Be honest in the output: if the critique changed the conclusion, say so plainly.
