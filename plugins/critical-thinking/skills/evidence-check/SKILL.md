---
name: evidence-check
description: Judge how dependable the evidence behind a claim is — intuition, personal experience, examples, testimonials, authority, observation, surveys, research studies, analogies — and check statistics for deception (biased or unknowable numbers, misleading averages, missing baselines, proving one thing while concluding another). Use when a claim cites data, studies, benchmarks, metrics, surveys, case studies, reviews or experts, or when the user asks "is this true", "how solid is this", or "can I trust these numbers".
---

# evidence-check

A factual claim is only as good as what stands behind it. Classify each piece of evidence, then ask the questions that fit its type. Treat "research shows" as "the researchers interpret their findings as showing".

## 1. List the factual claims

Separate claims of fact (could be checked) from opinions (preferences, values). Only the first need evidence; for each, note what evidence is offered — or that none is.

## 2. Evaluate by type

| Evidence type | Main risk | Ask |
|---|---|---|
| **Intuition / gut feeling** | Unexamined, unshareable; confidence reflects a coherent story, not accuracy | Is the domain regular enough to predict, and did this person get long practice with fast feedback in it? If not, treat it as a hypothesis only. |
| **Personal experience** | One case, memory distortions, unusual circumstances | Was it typical? What did the person expect to see? |
| **Case examples / anecdotes** | Vivid, picked to persuade, unrepresentative | How were cases selected? How many counter-cases exist? |
| **Testimonials / reviews** | Selective, may be paid, not experts on causes | Who chose them? What's the full distribution of reviews? Any incentive? |
| **Authority / experts** | Outside their field, conflicts of interest, experts disagree, confident long-range forecasts in unpredictable domains | Expert in *this*? Checked track record, not reputation? Do other experts agree? Who funds them? |
| **Personal observation** | Observers see what they expect | Several independent observers? Conditions controlled? |
| **Surveys / questionnaires** | Leading wording, who responded, honesty | Exact question wording? Sample and response rate? Incentive to answer a certain way? |
| **Research studies** | Quality varies, single studies mislead, findings get oversimplified | See checklist below. |
| **Analogies** | Relevant differences ignored | List similarities *and* differences; do the differences matter to the conclusion? |

### Research checklist
- Quality: design, controls, sample size, pre-registration, peer review — and publication alone guarantees nothing.
- Replication: has anyone else found the same thing? One study against a body of work is weak.
- Interpretation: do the findings support the conclusion, or only a narrower version of it?
- Bias and funding: who paid, who ran it, what did they hope to find?
- Distortion: did the person citing it drop the original qualifications?
- **Generalizing from the sample**: big enough? Broad enough (ages, regions, contexts)? Randomly or conveniently chosen? Does it match the population the claim is about?
- **Generalizing from the measures**: does the measurement actually capture the concept (e.g. "lines of code" for productivity, "time on page" for engagement)? Self-reports vs behavior?
- Source checks for online claims: who publishes it, primary or secondary, when, and what do independent sources say?

## 3. Check the statistics

- **Unknowable or biased numbers**: could anyone actually know this ("80% of attacks go unreported")? How was it counted?
- **Averages**: mean, median or mode? A mean hides skew (a few huge accounts, a few slow requests). Ask for the median, range and distribution — percentiles for latency.
- **Measurement errors**: did the definition or method change over time? Are different things being compared as if they were the same?
- **Concluding one thing, proving another**: the number may be accurate but measure something adjacent to the conclusion (more sign-ups ≠ more retained users; fewer reported bugs ≠ fewer bugs).
- **Omitted numbers**: relative vs absolute change ("doubled" from 1 to 2), missing baseline or control, missing denominator, cherry-picked time window, truncated chart axes, survivorship.
- **Small samples**: small groups produce extreme results by chance — the best and the worst rates both come from the smallest samples. Ask for the sample size before explaining an extreme result.
- **Base rates**: a vivid description of a case ("this looks like a breakout product") should be weighed against how often things in that category actually succeed. Start from the base rate.
- **Regression to the mean**: an unusually good or bad result is usually followed by a more ordinary one, with or without any intervention.
- Always ask for the actual numbers behind *most, many, significantly, faster, leading*.

## Output

```markdown
| Claim | Evidence offered | Type | Problems found | Strength (strong / moderate / weak / none) |
|---|---|---|---|---|
```

Then: what evidence would settle the weakest important claim, and where to look for it. Prefer checking a primary source over trusting a summary, and say when you could not verify something.
