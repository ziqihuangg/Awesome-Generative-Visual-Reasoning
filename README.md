# Awesome Generative Visual Reasoning

*This repository contains the paper list for the survey* **Where Does the Reasoning Come From? A Survey of Generative Visual Reasoning**.

<!-- ![overall_structure](./figures/fig_teaser.jpg) -->

[![Awesome](https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg)](https://github.com/ziqihuangg/Awesome-Generative-Visual-Reasoning)
![visitors](https://visitor-badge.laobi.icu/badge?page_id=ziqihuangg.Awesome-Generative-Visual-Reasoning)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat)](https://github.com/ziqihuangg/Awesome-Generative-Visual-Reasoning/pulls)

## Overview

Generative models are increasingly asked to **solve** visual problems rather than depict them, and the results are uneven in a way that is rarely explained. A video model given a first frame and an instruction will segment objects, infer material properties, simulate tool use and solve mazes, none of which it was trained to do — and will then let a ball roll off a table and drift sideways. Explaining that gap requires knowing which mechanism produced which result.

We therefore organise the field by a question that is prior to the usual ones: **where does the reasoning competence actually come from?** Six sources appear in the literature and they are not interchangeable — regularities absorbed during pretraining, language models, multimodal models, simulators and formal systems, search and verifiable reward, and self-supervised predictive objectives. The medium in which a method writes its intermediate state, which we call the **carrier**, runs across these sources as a thread rather than forming a second hierarchy: a simulator has no choice about how to hand over its answer, while a multimodal model has four.

Crossing the six sources with visual problems graded by *what grounds a correct answer* produces the survey's main empirical result. **Formal rule-following is the most verifiable problem class in the field and is well supplied with benchmarks, yet not one of the 153 methods we review targets it, under any source.** The least verifiable class, by contrast, has methods and almost no benchmarks. What separates them is not measurability but **depictability**, because a frame cannot hold a symbol that has not yet been bound to a position and an appearance. This yields a bounded claim in place of the usual one: the visual medium is irreplaceable where the intermediate state is dense, continuous and fully determined, and is the wrong instrument where it is sparse, discrete and deliberately partial.

### Definition

> **Generative visual reasoning** is the production of visual output whose content is determined by states the system *infers* rather than states supplied by the conditioning, where correctness is grounded in visual structure.

Three properties are usually conflated, and keeping them apart is what lets one account cover video generation, layout-conditioned image generation, interleaved generation and agentic pipelines at once:

- **P — is the problem posed visually?** Does answering require attending to an image or a scene, rather than to a description of one?
- **C — is the intermediate state visual?** Is the working-out written in pixels, or in text, symbols or latents? This is the *carrier*, and it is a variable rather than a premise.
- **G — is correctness grounded in visual structure?** Is there a physical, geometric, causal or task-defined standard under which the output is right or wrong for reasons that depend on the visual world?

**G** plus the inference condition gates admission; **P** and **C** classify the work. Two consequences: reasoning need not happen in frames, and depiction is not reasoning — super-resolution produces pixels and reasons about nothing.

### What You'll Find Here

Within this repository, we collect works that aim to answer some critical questions in this field, such as:

- **Sources**: Where does a method's reasoning competence come from, and what can it therefore never get right?
- **Carriers**: In what medium is the intermediate state written — language, structured symbols, visual states, or continuous latents — and what does each medium structurally fail to express?
- **Problems**: What grounds a correct answer, and which classes of visual problem has the field left unaddressed?
- **Read-out**: A generated video does not announce its answer. What extracts it, and how reliable is that extractor?
- **Unification**: Is video generation to visual problems what instruction-tuned language modelling became to language problems?


### Table of Contents
- [1. Sources of Reasoning Competence](#1.)
  - [1.1. S1: Regularities Absorbed from Data](#1.1.)
  - [1.2. S2: Language Models](#1.2.)
  - [1.3. S3: Multimodal Models](#1.3.)
  - [1.4. S4: Simulators and Formal Systems](#1.4.)
  - [1.5. S5: Search, Verification and Reward](#1.5.)
  - [1.6. S6: Self-Supervised Prediction](#1.6.)
- [2. Carriers of the Intermediate State](#2.)
  - [2.1. Natural Language](#2.1.)
  - [2.2. Structured Symbols](#2.2.)
  - [2.3. Visual States](#2.3.)
  - [2.4. Continuous Latents](#2.4.)
  - [2.5. No Carrier, and the Video as Its Own Trace](#2.5.)
- [3. Visual Problems, Graded by What Grounds an Answer](#3.)
  - [3.1. V1: Physical Law](#3.1.)
  - [3.2. V2: Structural Persistence](#3.2.)
  - [3.3. V3: Formal Rules](#3.3.)
  - [3.4. V4: Goal Attainment](#3.4.)
  - [3.5. V5: Procedure and Order](#3.5.)
  - [3.6. V6: Convention and Intent](#3.6.)
  - [3.7. V0 and VX: The Two Bands That Are Not Groundings](#3.7.)
- [4. Benchmarks and Evaluation](#4.)
  - [4.1. Benchmarks by Grounding](#4.1.)
  - [4.2. Process-Level and Annotation-Free Protocols](#4.2.)
  - [4.3. Auditing the Verifiers](#4.3.)
- [5. Study and Rethinking](#5.)
  - [5.1. Related Surveys](#5.1.)
  - [5.2. Position, Diagnosis and Analysis](#5.2.)
- [6. Other Useful Resources](#6.)

## Framework at a Glance

### The Six Sources

Each source states what it contributes that the others cannot, and what it structurally cannot supply. Counts are methods in the current draft, out of 153.

| Source | Where the competence comes from | What it cannot supply | Methods |
| --- | --- | --- | --- |
| **S1** | Regularities absorbed during pretraining | Law-like generalisation; it interpolates between memorised cases | 41 |
| **S2** | Language models: compositional and commonsense structure | Geometry and quantity — it cannot say *where*, *how much*, or exactly *when* | 16 |
| **S3** | Multimodal models: they can both see an intermediate state and judge it | Verified transfer from static relations to dynamics | 17 |
| **S4** | Simulators and formal systems: exact within their domain | Anything outside its equations — cloth, fluids, fracture, articulated contact | 33 |
| **S5** | Search and verifiable reward: score candidates and keep the best | More than its verifier can detect | 25 |
| **S6** | Self-supervised predictive objectives, installed during training | Auditability; no intermediate state exists to inspect | 21 |

### The Four Carriers Are Not a Ladder

The literature tends to number the carriers L0–L5, which invites a reading in which each stage supersedes the last. That reading is false three times over: the chronology runs the wrong way (structured symbols are the oldest explicit carrier, visual states the newest), the populations are not monotonic (natural language is the smallest family, at 4 methods), and capability does not order them. Two independent properties place them in a 2×2 whose cells predict their characteristic failures.

| | **No spatial commitment** | **Spatially committed** |
| --- | --- | --- |
| **Symbolic** | **Natural language** — cannot say where, how much, or exactly when | **Structured symbols** — cannot leave a fixed vocabulary |
| **Distributed** | **Continuous latents** — cannot be read, edited or checked | **Visual states** — cannot express uncertainty, or anything in between |

Language, symbols and visual states place the reasoning *outside* the generator, which is why so many such methods are training-free and why they chain readily. Continuous latents do the opposite: they modify the generator during training, so they are not a stage in a pipeline but an alternative to having one.

### The Problem Classes

Rows are ordered by how much of the correctness judgement a machine can make without a human. Method-building tracks *depictability*; instrument-building tracks *verifiability*; the two come apart at V3 and V6 in opposite directions.

| Class | What grounds a correct answer | Coverage |
| --- | --- | --- |
| **V1** | Physical law | 66 papers, 45 of them methods — the best-instrumented row |
| **V2** | Structural persistence: 3D geometry, identity and layout surviving occlusion and time | 25 papers |
| **V3** | Formal rules: mazes, board games, symbolic puzzles | 4 instruments, **zero methods** |
| **V4** | Goal attainment: is the rollout good enough to act on? | 48 papers, the clearest practical payoff |
| **V5** | Procedure and order: do sub-goals occur in a valid order? | 9 papers |
| **V6** | Convention and intent: narrative, cinematic language, other agents' mental states | 10 papers, and almost no instruments |
| **V0 / VX** | Not groundings: general quality (outside the paradigm) and work targeting no single grounding | Kept explicit as the control condition |

<a name="1."></a>
## 1. Sources of Reasoning Competence

The spine of the survey. Methods are filed by the source their competence comes from, and cross-indexed by carrier in [Section 2](#2.) and by problem class in [Section 3](#3.).

<a name="1.1."></a>
### 1.1. S1: Regularities Absorbed from Data

Pretraining itself. Enough video contains enough falling, colliding and pouring that a generator absorbs a broad prior over dynamics without being told a law — broad coverage with a low ceiling, which is the profile that motivates every other source.

*Paper list coming soon.*

<a name="1.2."></a>
### 1.2. S2: Language Models

Entering as a rewriter, which enriches an underspecified prompt with the physical effects a scene implies, or as a planner, which decomposes a request into a shot list, scene graph or layout sequence.

*Paper list coming soon.*

<a name="1.3."></a>
### 1.3. S3: Multimodal Models

The only source that genuinely exercises the carrier axis, appearing as a critic that inspects generated keyframes, a planner grounded in observed pixels, and a latent interface that conditions the generator without passing through text.

*Paper list coming soon.*

<a name="1.4."></a>
### 1.4. S4: Simulators and Formal Systems

Reasoning imported rather than learned: rigid-body engines, particle and Gaussian representations, symbolic equation discovery. Correct by construction for the phenomena they model, and silent outside them.

*Paper list coming soon.*

<a name="1.5."></a>
### 1.5. S5: Search, Verification and Reward

Reasoning produced by search rather than construction — test-time scaling, backtracking, verifiable and physics-aware rewards, process-level supervision. Only ever as good as the verifier.

*Paper list coming soon.*

<a name="1.6."></a>
### 1.6. S6: Self-Supervised Prediction

Competence installed during training through an auxiliary predictive objective. The exact complement of S4: it degrades gracefully rather than falling silent, and buys that generality by being impossible to audit.

*Paper list coming soon.*

<a name="2."></a>
## 2. Carriers of the Intermediate State

<a name="2.1."></a>
### 2.1. Natural Language

A rewritten prompt, an enumerated list of physical effects, a critique fed back into the next attempt.

*Paper list coming soon.*

<a name="2.2."></a>
### 2.2. Structured Symbols

Machine-readable but not linguistic: a scene layout, a set of masses and friction coefficients, a trajectory, a camera path, an executable program.

*Paper list coming soon.*

<a name="2.3."></a>
### 2.3. Visual States

The intermediate state is itself an image: keyframes, storyboards, sketches, coarse renderings inspected and revised before the full output is produced.

*Paper list coming soon.*

<a name="2.4."></a>
### 2.4. Continuous Latents

A feature bank with no human-readable form, transferred from a multimodal model or a predictive encoder into the generator.

*Paper list coming soon.*

<a name="2.5."></a>
### 2.5. No Carrier, and the Video as Its Own Trace

The two regimes that bracket the four carriers: nothing is externalised and competence is whatever pretraining left behind, or the generated frames *are* the reasoning trace and the external scaffold disappears.

*Paper list coming soon.*

<a name="3."></a>
## 3. Visual Problems, Graded by What Grounds an Answer

Only problems whose answer is underdetermined by the input are in scope. Tier 0 — super-resolution, denoising, interpolation — recovers its target by a fixed local map and needs no reasoning; Tier 1 — segmentation, depth, flow — sits on the line, and which side it falls on depends on the query rather than the task.

<a name="3.1."></a>
### 3.1. V1: Physical Law

*Paper list coming soon.*

<a name="3.2."></a>
### 3.2. V2: Structural Persistence

*Paper list coming soon.*

<a name="3.3."></a>
### 3.3. V3: Formal Rules

The row the survey is built around, and the one with no methods in it. The gap is not measurability — a maze is either solved or not — and not difficulty, since native generation already gets non-trivial accuracy. It is an interface failure: solving a rule problem requires holding a partial assignment, and a frame cannot show a symbol without also showing where it is and what it looks like.

*Paper list coming soon.*

<a name="3.4."></a>
### 3.4. V4: Goal Attainment

*Paper list coming soon.*

<a name="3.5."></a>
### 3.5. V5: Procedure and Order

*Paper list coming soon.*

<a name="3.6."></a>
### 3.6. V6: Convention and Intent

*Paper list coming soon.*

<a name="3.7."></a>
### 3.7. V0 and VX: The Two Bands That Are Not Groundings

*Paper list coming soon.*

<a name="4."></a>
## 4. Benchmarks and Evaluation

Video is not a verifiable medium in the sense that a proof or a program is. A generated video does not announce its answer: something must extract it from pixels before correctness can be assessed, and that extractor is itself a fallible model, so every generative reasoning benchmark inherits the failure modes of its read-out mechanism.

<a name="4.1."></a>
### 4.1. Benchmarks by Grounding

*Paper list coming soon.*

<a name="4.2."></a>
### 4.2. Process-Level and Annotation-Free Protocols

Protocols that score the intermediate steps rather than only the final frame, and cycle-consistency read-outs that need no labels but score coherence rather than correctness.

*Paper list coming soon.*

<a name="4.3."></a>
### 4.3. Auditing the Verifiers

The field has begun auditing its own judges, finding that the vision models used to certify physical plausibility collapse on precisely the geometrically demanding cases that distinguish plausible from correct. Gains reported against a weak verifier should be read as gains against that verifier.

*Paper list coming soon.*

<a name="5."></a>
## 5. Study and Rethinking

<a name="5.1."></a>
### 5.1. Related Surveys

Six bodies of existing literature border this one: generation foundations, long video and storytelling, world models, multimodal reasoning, video understanding, and evaluation. The nearest prior work organises the space by reasoning *task*; we organise it by reasoning *mechanism*. A task-centred account tells you what has been attempted, while a mechanism-centred one tells you why a given approach hits a ceiling.

*Paper list coming soon.*

<a name="5.2."></a>
### 5.2. Position, Diagnosis and Analysis

Diagnostic work on whether visual realism and physical understanding are decoupled, whether object state survives occlusion, and whether predictive objectives install anything that deserves the name reasoning.

*Paper list coming soon.*

<a name="6."></a>
## 6. Other Useful Resources

*Coming soon.*
