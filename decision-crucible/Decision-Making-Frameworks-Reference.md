---
title: "Decision-Making Frameworks Quick Reference"
created: 2026-03-29
type: reference
tags: [decision-making, mental-models, frameworks, reference]
status: active
---

# Decision-Making Frameworks Quick Reference

Structured index of decision-making techniques organized by use case and domain. Each entry includes when to use it, the core steps, and limitations. For deep research on each framework, see [[Decision-Making-Frameworks-Research]].

---

## Framework Selection Guide

Use this table to quickly identify which framework fits your situation:

| Situation | Primary Framework | Supporting Frameworks |
|---|---|---|
| Something is accepted without question | First Principles | Inversion, Socratic Method |
| New evidence arrives | Bayesian Reasoning | Base rate check, Calibration |
| Choosing between defined options | Decision Matrix + WWHTBT | Expected Value, Opportunity Cost |
| Planning a major initiative | Pre-Mortem + WWHTBT | Second-Order Thinking, FMEA |
| Fast-moving competition | OODA Loop | Clausewitz friction, Game Theory |
| Unsure what kind of problem it is | Cynefin Framework | Differential Diagnosis |
| Quantifying risk vs. reward | Expected Value + NNT/NNH | Marginal Analysis, Dose-Response |
| Stuck and cannot solve forward | Inversion | Proof by Contradiction, Dialectical Reasoning |
| Worried about unintended consequences | Second-Order Thinking | Sowell stage-two, Fault Tree |
| Personal/emotional decision | IFS Parts Check + CBT Audit | Affect Heuristic awareness |
| Evaluating whether a claim is true | Falsification (Popper) | Deutsch hard-to-vary, Feynman self-deception |
| Post-failure analysis | Root Cause Analysis | FTA + FMEA retrospective |

---

## Always-On Frameworks

These two run on every non-trivial decision:

### First Principles Thinking
**Core question:** What do I know to be fundamentally true, independent of convention?

1. List all assumptions embedded in the problem framing
2. Tag each: convention, competitor-inherited, historical, fear-based, authority, untested
3. Strip to irreducible truths (verifiable regardless of context)
4. Reconstruct approaches using only verified truths
5. Compare conventional vs. first-principles paths

**Techniques:** Socratic Questioning (6 types), Five Whys
**Limitations:** High mental energy. Not every problem needs it. Risk of reinventing wheels.

### "What Would Have to Be True" (WWHTBT) -- Roger Martin
**Core question:** What conditions must hold for each option to be the best choice?

1. List all viable options
2. For each: what must be true about industry, customers, capabilities, competitors?
3. Identify the most uncertain conditions (barriers to choice)
4. Design tests for the uncertain conditions
5. Monitor conditions as a "canary" -- if they stop holding, revisit the decision

**Limitations:** Requires honesty about uncertainty. Can be gamed.

---

## General Frameworks

### Bayesian Reasoning
**When:** New evidence should change your belief. Probability-heavy decisions.
**Steps:** Establish prior -> Assess likelihood -> Calculate posterior -> Iterate
**Key concept:** Likelihood ratios. LR > 10 = strong evidence. LR = 1 = no evidence.
**Watch for:** Base rate neglect (the most common Bayesian error).

### Decision Matrix (Weighted Scoring)
**When:** Multiple defined options, multiple criteria, need alignment.
**Steps:** List options -> Define criteria -> Assign weights BEFORE evaluating -> Score -> Calculate -> Compare
**Critical rule:** Set criteria and weights before anyone sees options.
**Limitations:** False precision. Only as good as chosen criteria.

### Pre-Mortem (Gary Klein)
**When:** Before committing to anything major. Overconfident teams.
**Steps:** Brief team -> "Imagine it failed spectacularly" -> Silent brainstorm -> Share -> Prioritize -> Mitigate
**Key insight:** Prospective hindsight increases accuracy of identifying failure reasons by 30%.

### OODA Loop (Boyd)
**When:** Competitive speed matters. Ambiguous, rapidly changing situations.
**Steps:** Observe -> Orient (the critical step) -> Decide -> Act -> Loop
**Key insight:** Victory goes to whoever cycles faster. Orientation is where biases live.

### Expected Value Calculation
**When:** Quantifiable probabilities and payoffs exist. Repeatable bets.
**Formula:** EV = Sum(probability_i x value_i)
**Kahneman caveat:** Humans are not EV maximizers. Loss aversion, probability weighting.

### Inversion (Munger)
**When:** Stuck. When avoiding stupidity beats seeking brilliance.
**Steps:** Define goal -> "What would guarantee failure?" -> List failure causes -> Ensure you're doing the opposite
**Munger's five notions:** Simplify, Quantify, Invert, Think multidisciplinary, Watch for lollapalooza effects.

### Second-Order Thinking (Sowell)
**When:** Policy, strategy, incentives. Anything with ripple effects.
**Steps:** First-order consequence -> "And then what?" -> Continue chain -> Map interactions -> Identify feedback loops
**Sowell's rule:** "There are no solutions, only trade-offs." Who bears costs? When do they arrive?

### Opportunity Cost Analysis
**When:** Every resource allocation decision.
**Core insight:** "Should I do X?" is always "Should I do X instead of Y?"
**Steps:** List all alternatives (not just the obvious one) -> Value each -> Identify what you give up

### Cynefin Framework (Snowden)
**When:** Need to determine what type of problem you face before choosing an approach.
**Domains:** Clear (best practices) -> Complicated (expert analysis) -> Complex (safe-to-fail probes) -> Chaotic (act first) -> Disorder (break apart)
**Diagnostic:** Do I understand causation? Is it stable? Is expertise sufficient?

### Dialectical Reasoning
**When:** Two valid positions seem to conflict. Seeking synthesis.
**Steps:** Articulate thesis -> Seek strongest antithesis -> Examine assumptions in both -> Synthesize

---

## Domain-Specific Techniques

### Engineering
- **Root Cause Analysis:** 5 Whys, Fishbone/Ishikawa diagrams, Pareto analysis
- **Fault Tree Analysis (FTA):** Top-down. Undesired event -> causes via AND/OR gates -> basic events
- **FMEA:** Bottom-up. For each component: what could fail? What happens? Risk Priority Number = Severity x Occurrence x Detection

### Science
- **Scientific Method:** Observe -> Hypothesize -> Experiment -> Analyze -> Conclude -> Replicate
- **Falsification (Popper):** A theory is scientific only if it can be proven false. "What evidence would disprove this?"
- **Conjecture and Refutation:** Problem -> Bold theory -> Rigorous testing -> New problems

### Philosophy -- Deutsch's Epistemology
- **Good explanations are hard to vary.** If you can swap the details without changing the conclusion, the explanation is weak.
- **Fallibilism.** All knowledge is provisional and improvable.
- **Problems are soluble.** Physical limitations stem from natural laws only; knowledge gaps create apparent barriers.
- **Bad philosophy:** Philosophy that actively prevents knowledge growth (instrumentalism, explanationless science).

### Mathematics
- **Proof by Contradiction:** Assume the opposite. Show it leads to impossibility. Therefore the original must be true.
- **Game Theory:** Nash Equilibrium, Prisoner's Dilemma, zero-sum vs. positive-sum. "What game am I playing?"
- **Optimization:** Local vs. global optima. Constraints. Multi-objective = inevitable trade-offs (Pareto frontier).

### Psychology (Personal Decisions)
- **IFS Parts Check:** Which parts are active? Managers (control), Firefighters (impulse), Exiles (pain)? Access Self (8 Cs: Calm, Curious, Clear, Compassionate, Confident, Creative, Courageous, Connected).
- **CBT Distortion Audit:** All-or-nothing, catastrophizing, emotional reasoning, mind reading, fortune telling, should statements, overgeneralization, mental filtering.
- **Cognitive Restructuring:** Identify automatic thought -> Evidence for/against -> Name distortion -> Generate balanced alternative.

### Medicine
- **Evidence Hierarchy:** Meta-analyses > RCTs > Cohort > Case-control > Case reports > Expert opinion
- **NNT/NNH:** Number Needed to Treat (lower = better). Number Needed to Harm (higher = better). Favor intervention when NNT < NNH.
- **Differential Diagnosis:** Gather data -> List possible causes -> Test to narrow -> Simplest explanation covering most findings (Occam).

### Economics (Sowell)
- **Incentive Analysis:** People respond to incentives. Change the cost, change the behavior.
- **Marginal Analysis:** Decide based on additional benefit vs. additional cost of one more unit. Sunk costs irrelevant.
- **Constrained vs. Unconstrained Vision:** Is human nature fixed (work with incentives) or malleable (design ideal systems)?

### Military/Strategy
- **Clausewitz Friction:** The gap between plan and reality. Build slack, redundancy, adaptability.
- **Center of Gravity:** The one thing that holds everything together. Focus there.
- **Boyd's OODA:** Cycle faster. Create confusion. Act with irregularity.

### Exercise/Health Science
- **Progressive Overload:** Growth requires systematically increasing challenge. Plateau = comfort zone.
- **Dose-Response:** First units of effort produce the most benefit (diminishing returns). Am I on the steep or flat part?
- **Benefit-Harm Ratio:** Maximize the ratio of benefit over harm, not absolute benefit.

---

## Cognitive Biases Quick Reference

### Information Overload Biases
- **Confirmation Bias:** Seeking/remembering what confirms beliefs
- **Availability Heuristic:** Overweighting vivid/recent info
- **Anchoring:** First number dominates
- **Negativity Bias:** Negatives hit harder than positives
- **Bias Blind Spot:** Seeing biases in others, not yourself

### Meaning-Making Biases
- **Narrative Fallacy:** Weaving facts into false cause-effect stories
- **Survivorship Bias:** Studying winners, ignoring losers
- **Base Rate Neglect:** Ignoring background frequencies
- **Dunning-Kruger:** Low skill -> overestimate. High skill -> underestimate.
- **Hindsight Bias:** "I knew it all along"
- **Clustering Illusion:** Seeing patterns in random data

### Action Biases
- **Sunk Cost Fallacy:** Continuing because of past investment
- **Status Quo Bias:** Preferring current state over change
- **Loss Aversion:** Losses feel 2x worse than equivalent gains
- **Affect Heuristic:** Deciding based on current emotion
- **Overconfidence:** 90% confident = right about 70% of the time
- **Optimism Bias:** Overestimating positive outcomes (planning fallacy)

### Memory Biases
- **Peak-End Rule:** Judging by peak and ending, not average
- **Framing Effect:** Presentation changes decisions ("90% survival" vs. "10% mortality")
- **WYSIATI:** Treating available info as the whole story

---

## The Master Checklist

Before any significant decision, run these 12 questions:

1. **What type of problem is this?** (Cynefin: clear, complicated, complex, chaotic?)
2. **What are my assumptions?** (First Principles: facts vs. conventions?)
3. **What would I need to believe for this to be the best choice?** (WWHTBT)
4. **What would guarantee failure?** (Inversion, Pre-Mortem)
5. **What happens after that? And after that?** (Second-Order Thinking)
6. **What am I giving up?** (Opportunity Cost)
7. **What is the expected value?** (EV calculation)
8. **What biases might be distorting my thinking?** (Cognitive bias audit)
9. **What evidence would change my mind?** (Falsification)
10. **Am I fooling myself?** (Feynman's first principle)
11. **Which parts of me are making this decision?** (IFS: Self or reactive part?)
12. **Is my explanation hard to vary?** (Deutsch: would changing any detail break it?)

---

## Key Thinkers

| Thinker | Core Principle | Decision Application |
|---|---|---|
| David Deutsch | Good explanations are hard to vary | Test if your reasoning survives detail-swapping |
| Thomas Sowell | No solutions, only trade-offs | Map full consequence chains. Who pays? When? |
| Charlie Munger | Invert, always invert | Ask what guarantees failure, then avoid it |
| Daniel Kahneman | System 1 shortcuts fool System 2 | Check for anchoring, loss aversion, overconfidence |
| Karl Popper | Falsification is the engine of knowledge | "What would make me abandon this belief?" |
| Richard Feynman | You are the easiest person to fool | Report what might invalidate your reasoning |

---

## Decision Records

All decisions processed through the Decision Crucible skill are saved to:
`04-LIFE/decision-making/Decision-Records/`

Each record includes: context, frameworks applied, key challenges and resolutions, the decision, load-bearing assumptions, trade-offs, falsification criteria, and monitoring triggers.
