# Awesome Generative Visual Reasoning

*This repository contains the paper list for the survey* **Where Does the Reasoning Come From? A Survey of Generative Visual Reasoning**.

<!-- ![overall_structure](./figures/fig_teaser.jpg) -->

[![Awesome](https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg)](https://github.com/ziqihuangg/Awesome-Generative-Visual-Reasoning)
![visitors](https://visitor-badge.laobi.icu/badge?page_id=ziqihuangg.Awesome-Generative-Visual-Reasoning)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat)](https://github.com/ziqihuangg/Awesome-Generative-Visual-Reasoning/pulls)

## Overview

Generative models are increasingly asked to **solve** visual problems rather than depict them, and the results are uneven in a way that is rarely explained. A video model given a first frame and an instruction will segment objects, infer material properties, simulate tool use and solve mazes, none of which it was trained to do — and will then let a ball roll off a table and drift sideways. Explaining that gap requires knowing which mechanism produced which result.

We therefore organise the field by a question that is prior to the usual ones: **where does the reasoning competence actually come from?** Six sources appear in the literature and they are not interchangeable — regularities absorbed during pretraining, language models, multimodal models, simulators and formal systems, search and verifiable reward, and self-supervised predictive objectives. The medium in which a method writes its intermediate state, which we call the **carrier**, runs across these sources as a thread rather than forming a second hierarchy: a simulator has no choice about how to hand over its answer, while a multimodal model has four.

Crossing the six sources with a classification of the reasoning tasks themselves produces the survey's main empirical result. **Formal rule-following is the most verifiable class of task in the field and is well supplied with benchmarks, yet not one of the 153 methods we review targets it, under any source.** The least verifiable class, by contrast, has methods and almost no benchmarks. Our task classification ([Section 1](#1.)) predicts this rather than merely recording it: a rule can be laid down only if it can already be said in discrete terms, so a task whose constraint is a stipulated rule tends to admit a symbolic route to its answer, and generating pixels to solve a problem that symbols already solve has nothing to recommend it. That turns an apparent hole in the literature into a boundary.

It also yields two bounded claims in place of the usual one, and they are not equally strong. Measured over the 129 in-scope tasks we classify, **a single final state fails to carry the answer for 44% of them — for the 28% that ask for no endpoint at all it conveys nothing whatever — while vision itself does the inferential work in 88%**. The case for *visual* reasoning is therefore much firmer than the case for *video* specifically, and we try throughout not to assert the two with equal force.

### Definition

> A system performs **generative visual reasoning** on a task when it emits visual content — a single image, a sequence of images, or a video — and both conditions below hold of that content.

**The inference condition.** There is at least one property of the emitted content that *(i)* is not determined by the conditioning the system was given, and *(ii)* has to take one value rather than another for the output to be correct. Both clauses carry weight. Without *(i)*, image restoration qualifies, because its answer was already in the input. Without *(ii)*, unconstrained generation qualifies, because much is left open but nothing turns on how it is settled. In one sentence: did the system have to commit to something it was not told, and could it have got that wrong?

**The grounding condition.** That property is right or wrong by virtue of visual structure — physical law, geometry, causal dependence among the things depicted, or a condition the task states over the depicted scene. It is not enough that *some* judgement can be made; the judgement must be about the world in the picture, rather than about the picture as an artefact, about linguistic convention, or about what a rater prefers.

Two further properties **describe** admitted work without gating it, and conflating them with the conditions above is the most common mistake in this area:

- **Visual posing** — does answering require attending to an image or a scene, rather than to a description of one? A physics question stated entirely in words is not visually posed even if its answer is rendered.
- **The visual carrier** — is the intermediate state, in systems that have one, written in pixels rather than in text, symbols or latents? This is the axis of [Section 3](#3.), and it is a variable of the method, not a premise of the definition.

Three consequences: **reasoning need not happen in pixels** (a language model deriving a causal chain that a generator renders satisfies both conditions with a non-visual carrier); **depiction is not reasoning** (super-resolution emits pixels and fails clause *(i)*); and **the visual content need not be the deliverable** (drawing an auxiliary line and reading an angle off it is in scope, because the inference committed to the drawing).

Because the conditions are clauses, the boundary can be checked rather than asserted — see [§1.6](#1.6.), where each excluded family fails a nameable clause.

### What You'll Find Here

Within this repository, we collect works that aim to answer some critical questions in this field, such as:

- **Tasks**: What does correctness demand — a unique endpoint, any admissible one, or none at all — and does the constraint come from the world or from a stipulated rule? Which cells has the field left empty?
- **Sources**: Where does a method's reasoning competence come from, and what can it therefore never get right?
- **Carriers**: In what medium is the intermediate state written — language, structured symbols, visual states, continuous latents, or the generation itself — and what does each medium structurally fail to express?
- **Read-out**: A generated image or video does not announce its answer. What extracts it, and how reliable is that extractor?
- **Unification**: Is generative vision to visual problems what instruction-tuned language modelling became to language problems?


### Table of Contents
- [1. Reasoning Tasks, Classified by What Correctness Demands](#1.)
  - [1.1. The Two Cuts, and Why They Come In That Order](#1.1.)
  - [1.2. A: One Right Endpoint](#1.2.)
  - [1.3. B: Many Right Endpoints](#1.3.)
  - [1.4. C: No Endpoint Is Asked For](#1.4.)
  - [1.5. The Overlay: Is the Reasoning Actually Spatial?](#1.5.)
  - [1.6. What Falls Outside, and Why](#1.6.)
  - [1.7. The V1–V6 Rows, and How They Map](#1.7.)
- [2. Sources of Reasoning Competence](#2.)
  - [2.1. S1: Regularities Absorbed from Data](#2.1.)
  - [2.2. S2: Language Models](#2.2.)
  - [2.3. S3: Multimodal Models](#2.3.)
  - [2.4. S4: Simulators and Formal Systems](#2.4.)
  - [2.5. S5: Search, Verification and Reward](#2.5.)
  - [2.6. S6: Self-Supervised Prediction](#2.6.)
- [3. Methods: Carriers and Arrangements](#3.)
  - [3.1. Natural Language](#3.1.)
  - [3.2. Structured Symbols](#3.2.)
  - [3.3. Visual States](#3.3.)
  - [3.4. Continuous Latents](#3.4.)
  - [3.5. No Carrier, and the Generation as Its Own Trace](#3.5.)
- [4. Benchmarks and Evaluation](#4.)
  - [4.1. Benchmarks by Task Class](#4.1.)
  - [4.2. Process-Level and Annotation-Free Protocols](#4.2.)
  - [4.3. Auditing the Verifiers](#4.3.)
- [5. Key Messages](#5.)
- [6. Study and Rethinking](#6.)
  - [6.1. Related Surveys](#6.1.)
  - [6.2. Position, Diagnosis and Analysis](#6.2.)
- [7. Other Useful Resources](#7.)

## Framework at a Glance

### The Task Classes

Two cuts. The **row** is what the task demands of the last frame, which decides how a result can be scored at all. The **column** is where the constraint on the process comes from, which decides whether a checker can exist. Counts are *tasks*, from the 182-task table behind [Section 1](#1.); the third column is the overlay that makes this a taxonomy of *visual* reasoning rather than of reasoning in general.

| | **World constrains the process** — implicit, in the weights | **A stipulated rule constrains it** — explicit, in the input | Needs spatial simulation |
| --- | --- | --- | --- |
| **A** one right endpoint<br>*scored by hitting it* | **A1** · 33 tasks<br>where the ball comes to rest; the other side of an object; the shape behind an occluder | **A2** · 14 tasks<br>the angle by auxiliary line; the tangram; *and* sudoku, mazes, the unique mate | A1: 33/33<br>A2: **6/14** |
| **B** many right endpoints<br>*scored by membership* | **B1** · 29 tasks<br>how cloth drapes; water spilling; *and* throw the ball in, stack a standing tower | **B2** · 17 tasks<br>pour without spilling; drive collision-free; assemble in the manual's order | B1: 29/29<br>B2: **9/17** |
| **C** no endpoint is asked<br>*scored by compliance* | **C1** · 33 tasks<br>the pendulum swinging; a flame burning; a crowd flowing; any fixed-horizon rollout | **C2** · 3 tasks<br>walk the way an old man walks; keep to this beat; demonstrate the procedure | C1: 33/33<br>C2: 3/3 |

Three things fall out of this table and none of them is visible in a subject-matter taxonomy. **A checker exists only in the right column**, so verifiable reward is available there and nowhere else. **A comparable target exists only in row A**, so scoring a row-B or row-C task frame by frame against one recorded clip measures the wrong thing — that clip is a sample of the admissible set, not the answer. And **every task with a symbolic shortcut sits in the right column**, while all 95 tasks in the left column need spatial work, which is the quantitative form of the claim that vision is doing the reasoning rather than decorating it.

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

<a name="1."></a>
## 1. Reasoning Tasks, Classified by What Correctness Demands


This section comes first because everything after it is read against it: which sources are applicable, what a method can be right about, and what an evaluation is entitled to measure. It is deliberately not a list of subject matters. Physics, geometry, rules and planning partition nothing — throwing a ball into a hoop belongs to all four at once — so every criterion here is a **function of the task**: it returns exactly one value per task, which is why the classes cannot overlap, and its range is exhaustive, which is why nothing falls between them. Neither exclusivity nor completeness then has to be argued for.

One premise comes before the cuts. A generative answer is produced as a sequence, so its intermediate states are *always* open to judgement. That holds of every task and therefore cuts nothing; what varies is what the task asks of the **last frame**.

<a name="1.1."></a>
### 1.1. The Two Cuts, and Why They Come In That Order

**The first cut is what the task demands of the last frame.** It leads because it decides how a result can be scored at all — and therefore which families of method are applicable before any of them is tried.

| | What correctness demands of the endpoint | How it can be scored | Supervision available |
| --- | --- | --- | --- |
| **A** | Exactly one final state is right, the way 1+1 has one right value | Hit or miss against that answer | A target |
| **B** | Many final states are right; one of them must be found | Membership: did it land inside the admissible set | The bounds, but no target |
| **C** | No endpoint is asked for; the last frame is merely where one stopped | Step-by-step compliance, since there is nothing to compare against | Per-step legality only |

Row C is not "anything goes". A pendulum accelerating upward is wrong. What is absent is a *target*, not a standard — and tasks with no standard at all, such as *make it look good* or *keep it safe*, are outside the classification entirely ([§1.6](#1.6.)). Conflating the two is easy and costly, because one of them admits a checker and the other has nothing for a checker to check.

**The second cut is where the constraint on the process comes from.** The two sides are different demands on a model rather than two labels:

| | **World** | **Stipulated rule** |
| --- | --- | --- |
| Where the constraint lives | In the weights: absorbed from data, or absent. "Please obey gravity" in a prompt does nothing | In the input: to be read, understood and then executed |
| How failure looks | Gradual and local — slight interpenetration, volume not conserved, the scene still plausible | Discrete and global — one repeated digit voids the grid, one swapped step voids the sequence |
| What judging it takes | Dense step-by-step checking | Often a single check at the end |
| Which sources apply | S1, S6 | S2 and S3 to read the rule, S5 to execute and verify it |
| What generalises | The constraint itself transfers to new scenes | Only the ability to read *a* rule transfers, never the rule |

The fourth row is why **verifiable reward is available for stipulated-rule tasks and nowhere else**: a checker presupposes that somebody has already written the rule down. This is where the task axis meets the source axis, and it is the sharpest thing this classification says about method design.

Where a task has no judgeable process at all — a single static endpoint, such as a furniture layout delivered as one image — the second cut falls back to asking what settles the endpoint.

Crossing the two cuts gives six cells. **Counts below are tasks, not papers.** They come from a 182-task table (129 of them in scope) built partly from benchmarks this survey never cites, so that coverage is tested rather than assumed; the relabelling of the 220 papers onto these cells is in progress, and the method counts quoted elsewhere in this README still refer to the V1–V6 rows of [§1.7](#1.7.).

<a name="1.2."></a>
### 1.2. A: One Right Endpoint

Exactly one final state is right, and it has to be inferred rather than looked up. A directly comparable target exists throughout this row.

| | Constraint on the process | Tasks | Examples |
| --- | --- | --- | --- |
| **A1** | World | 33 | Where a dropped ball comes to rest; what an object looks like from the other side; the shape hidden behind an occluder; what solid a flat net folds into; the table once the gripper has lifted the block; the scene a moment before this frame; which earlier event broke the glass; novel views of a static scene; segmenting *the object that will fall next* |
| **A2** | Stipulated rule | 14 | The filled sudoku; the reassembled jigsaw; the unique mate in two; the tangram silhouette; the unique route through a maze; the angle found by drawing the auxiliary line; compass-and-straightedge construction; the output grid once the transformation has been induced from examples |

Two remarks. A checker exists only in A2, so A1 is the one cell where competence must come from a target and cannot be bought with search. And A2 is where the survey's empirical result lives: it splits 6 spatial against 8 symbolic ([§1.5](#1.5.)), and the methods are missing from precisely the symbolic half.

<a name="1.3."></a>
### 1.3. B: Many Right Endpoints

Several final states are acceptable and one must be produced. No target exists, so a recorded clip is a *sample* of the admissible set rather than the answer — which is why per-pixel comparison against it measures something other than the task.

| | Constraint on the process | Tasks | Examples |
| --- | --- | --- | --- |
| **B1** | World | 29 | How a cloth drapes over a chair; how water fills a glass and spills when tipped; ice melting; a fracture pattern; this street as it would look in winter; the same shot relit at sunset; colourising, and completing what the input does not entail; **and** throw the ball into the hoop, stack a tower that stands, fetch the cup — the goal is stipulated, but the route only has to be possible |
| **B2** | Stipulated rule | 17 | Pour without spilling; drive to the goal without colliding; trace any wall-free route through the maze; assemble in the order the manual gives; demonstrate a surgical or cooking procedure; a long-horizon manipulation plan; break a story into a tellable shot order; turn a script into a storyboard |

The bold clause in B1 is where this classification parts company with an intuition worth naming. Throwing a ball into a hoop *feels* rule-governed, and its goal is indeed stipulated; but nothing human constrains the flight, which only has to be physically possible. The stipulation sits on the endpoint, not on the process, so the task is judged the way a physical prediction is judged.

<a name="1.4."></a>
### 1.4. C: No Endpoint Is Asked For

The task never asks about a final state. Either the process is periodic or steady and has no last frame at all, or the horizon is an arbitrary cut — *the next five seconds* becomes another frame entirely if you ask for six, and the task has not changed. Every judgement therefore falls on the path.

| | Constraint on the process | Tasks | Examples |
| --- | --- | --- | --- |
| **C1** | World | 33 | A pendulum swinging; water boiling; a flame burning; a flag fluttering; gears meshing; a crowd flowing through a doorway; granular media pouring; how a clip continues on its own; what a pedestrian does over the next several seconds; **any fixed-horizon rollout of a world model** — driving, navigation, humanoid, game engine; weather nowcasting; fire spread |
| **C2** | Stipulated rule | 3 | Walk the way an old man walks; keep to this beat; demonstrate the procedure |

This row is the ground on which the claim about dense continuous evolution actually rests: **a single state cannot answer these tasks at all**, not because a sequence is preferable but because handing over an endpoint conveys nothing when no endpoint was asked for. It is also the row that reclassifies most world-model work, which the arbitrary-horizon test places here rather than in B.

C2 is the thinnest cell of the six by a wide margin. A stipulated manner with no endpoint asked for — perform this in a specified way, indefinitely — is barely studied, and we flag it as a structural gap rather than an oversight of ours.

<a name="1.5."></a>
### 1.5. The Overlay: Is the Reasoning Actually Spatial?

The two cuts above describe a **logical structure that is indifferent to modality**: endpoint determinacy and constraint source apply just as well to a text-only task. Left there, the classification would be general reasoning wearing a visual coat. So there is a third criterion, and it is read as an overlay rather than a branch.

Visual necessity has two levels, and only the second discriminates:

- **Is the output visual?** Nearly every task in the table satisfies this, so it separates almost nothing.
- **Does spatial simulation do the inferential work?** This is the question that matters.

```
sim(task) ∈ { spatial, symbolic }
```

**Read it about the inference, never about perception.** Every task needs sight to read the scene — even a photographed maze must be seen before it can be solved — which is exactly why the perceptual level cannot classify anything. The test is: *can the task be written, without loss, as discrete states plus a finite rule set whose size does not grow with the geometry of the scene?* If yes it is `symbolic`, and drawing the answer is rendering rather than reasoning.

Over the 129 in-scope tasks:

| | Needs spatial simulation | Symbolic route exists |
| --- | --- | --- |
| **World column** (A1, B1, C1) | **95 / 95** | 0 |
| **Rule column** (A2, B2, C2) | 18 | **16** |
| Total | **113 (88%)** | 16 (12%) |

**Every symbolic task sits in the stipulated-rule column, and not one of the 95 world-constrained tasks has a symbolic route.** That is not a coincidence. A rule can be laid down only if it can already be said in discrete terms, so stipulability *is* symbolisability; the world carries no comparable rule set at the scale of a scene.

Two consequences. First, this is the measured answer to *which tasks native visual reasoning is for*: the `spatial` ones, meaning the whole world column plus the geometric half of the rule column. Second, the 16 symbolic tasks are where the objection "this is general reasoning with a visual shell" genuinely lands, and we would rather state that than let it pass — script-to-storyboard and short-drama generation are the uncomfortable cases, since ordering discrete narrative units admits a symbolic route and needs an argument we do not yet have.

<a name="1.6."></a>
### 1.6. What Falls Outside, and Why

Exclusions are derived from the cuts rather than listed beside them. Three of the four are degenerate corners of cells that are otherwise in scope, which is why a subject-matter reading of them goes wrong.

Each also fails a nameable clause of the definition, which is what makes the boundary auditable: the first two fail clause *(i)* of the inference condition (the answer was already given, by the input or by the request), the third fails clause *(ii)* (nothing turns on how the output is settled), and the fourth fails the grounding condition (the standard is about the recording, not the depicted world). Four exclusions, three clauses, no residue.

| Excluded | Why | Examples |
| --- | --- | --- |
| The input already carries the answer | A degenerate corner of A1: unique, world-settled, but nothing is left to infer | Super-resolution, denoising, deblurring, artefact removal; depth; optical flow; visible-boundary segmentation; frame interpolation; tracking |
| The request already names the answer | The same corner of A2 | The named class; the exact count; the specified colour; a spatial relation the prompt states outright; the given text string; the prompt's order of actions; layout-conditioned generation once the arrangement is fixed |
| There is no right answer at all | The empty value of the first cut: only a better and a worse, so nothing for a checker to check | Make it look good; make a clip broadly plausible with no particular situation in question; keep the content safe |
| The condition is on the artefact, not the situation | **The only exclusion that needs a gate of its own**, because it takes the same value as B2 on every criterion in the grid | No flicker; smooth motion; appearance stable across frames; no background drift; clean exposure; holding a requested style |

Two boundary rules are worth stating because they are commonly got wrong. **Low-level restoration is not excluded as a batch.** The corner is defined by the input *entailing* the answer, not by a task sounding low-level: denoising is a reversible degradation, but greyscale does not entail colour and a mask leaves no trace of what it covers, so colourisation, non-entailed inpainting and outpainting are ordinary B1 tasks. And **degeneracy is a property of the query, not of the output format**: segmenting a visible boundary is excluded, while segmenting *the object that will fall next* is A1 with a mask for an answer.

<a name="1.7."></a>
### 1.7. The V1–V6 Rows, and How They Map

Earlier drafts graded problems by *what grounds a correct answer* into six rows, V1–V6. The method and instrument counts quoted in this README still come from those labels, so they are kept here until the relabelling is finished. There is no mechanical mapping: every row splits.

| Row | Where it goes |
| --- | --- |
| **V1** Physical law | Landing point pinned → A1; evolution admitting many endings → B1; periodic or open-horizon → C1; counterfactual renderings mostly B1 |
| **V2** Structural persistence | Mostly A1; layout *generation* → B2 if the arrangement is underdetermined, excluded if already fixed |
| **V3** Formal rules | A2 and B2, and this is where the zero-method result sits — [§1.5](#1.5.) predicts it should sit on the symbolic half specifically |
| **V4** Goal attainment | Predicting the rollout → C1 under the arbitrary-horizon test; finding the actions → B2 |
| **V5** Procedure and order | Mostly B2; reordering with a unique true order → A1 |
| **V6** Convention and intent | Predicting what an agent does → A1; shot arrangement → B2, and symbolic there ([§1.5](#1.5.)); conventions the prompt states outright → excluded |
| **V0** | Not a grounding: splits across all four exclusions in [§1.6](#1.6.) |
| **VX** | Targets no single grounding by construction; no cell |

<!-- auto:prob -->
*The 153 methods by the row they target. This is the labelling the counts above are computed from; papers will be re-filed onto the A1–C2 cells as that pass completes. Benchmarks for the same rows are in [§4.1](#4.1.), and the coverage they produce is read in [§5](#5.).*

**V1 · Physical law** · 45

- **S2** — [Event-Centric Causal Thought](https://arxiv.org/abs/2603.09094), [PhyT2V](https://arxiv.org/abs/2412.00596), [WISA](https://arxiv.org/abs/2503.08153), [PhysVid](https://arxiv.org/abs/2603.26285)
- **S3** — [VChain](https://arxiv.org/abs/2510.05094), [Think Before You Diffuse](https://arxiv.org/abs/2505.21653), [VLIPP](https://arxiv.org/abs/2503.23368), [VLM Self-Refinement](https://arxiv.org/abs/2511.20280), [VIPER (2026)](https://arxiv.org/abs/2607.23472), [SiPhy](https://arxiv.org/abs/2607.22355), [Physics Context Builders](https://arxiv.org/abs/2412.08619), [Compositional Physical Reasoning](https://arxiv.org/abs/2408.02687)
- **S4** — [PhyRPR](https://arxiv.org/abs/2601.09255), [CausalMotion](https://arxiv.org/abs/2606.14317), [PhysGen](https://arxiv.org/abs/2409.18964), [PhysChoreo](https://arxiv.org/abs/2511.20562), [NewtonGen](https://arxiv.org/abs/2509.21309), [PhyMAGIC](https://arxiv.org/abs/2505.16456), [Phantom](https://arxiv.org/abs/2604.08503), [PhysRAG](https://arxiv.org/abs/2606.26916), [PhysVideoGenerator](https://arxiv.org/abs/2601.03665), [Simulator-in-the-Loop](https://arxiv.org/abs/2603.06408), [PhysCtrl](https://arxiv.org/abs/2509.20358), [PhyParam](https://arxiv.org/abs/2607.18924), [Equation Discovery + Trajectory](https://arxiv.org/abs/2507.06830), [Physics-Guided Interactions](https://arxiv.org/abs/2510.02284), [Goal Force](https://arxiv.org/abs/2601.05848), [PhiZero](https://arxiv.org/abs/2607.28624), [ODEWorld](https://arxiv.org/abs/2607.27924), [DeforM](https://arxiv.org/abs/2607.18664), [PhysEditWorld](https://arxiv.org/abs/2606.26694), [APT](https://arxiv.org/abs/2606.18586), [PhysGM](https://arxiv.org/abs/2508.13911), [Physics3D](https://arxiv.org/abs/2406.04338)
- **S5** — [PhysRVG](https://arxiv.org/abs/2601.11087), [NEWTON](https://arxiv.org/abs/2605.18396), [PhyGDPO](https://arxiv.org/abs/2512.24551), [VJEPA-2 Reward](https://arxiv.org/abs/2510.21840), [Phys-AR / Timestep Tokens](https://arxiv.org/abs/2504.15932), [Planning with Sketch-Guided Verification](https://arxiv.org/abs/2511.17450)
- **S6** — [VideoREPA](https://arxiv.org/abs/2505.23656), [PhysAlign](https://arxiv.org/abs/2603.13770), [MoE Latent Alignment](https://arxiv.org/abs/2606.04737), [ProPhy](https://arxiv.org/abs/2512.05564), [DiReCT](https://arxiv.org/abs/2603.25931)

**V2 · Structural persistence** · 20

- **S1** — [FreqForcing](https://arxiv.org/abs/2607.27110), [TaoMate](https://arxiv.org/abs/2607.24359), [Diffusion over Diffusion](https://arxiv.org/abs/2303.12346), [Advancing Narrative Long Video](https://arxiv.org/abs/2605.18733), [FreeNoise](https://arxiv.org/abs/2310.15169), [FIFO-Diffusion](https://arxiv.org/abs/2405.11473), [StreamingT2V](https://arxiv.org/abs/2403.14773)
- **S2** — [LLM-grounded Video Diffusion](https://arxiv.org/abs/2309.17444), [VideoDirectorGPT](https://arxiv.org/abs/2309.15091), [CinemaTraj](https://arxiv.org/abs/2607.26910)
- **S3** — [Narrative Weaver](https://arxiv.org/abs/2603.06688)
- **S4** — [OrthoPhys](https://arxiv.org/abs/2603.18639), [ReVision](https://arxiv.org/abs/2504.21855), [3D Scene Prompting](https://arxiv.org/abs/2510.14945), [Diffusion as Shader](https://arxiv.org/abs/2501.03847), [Generative Rendering](https://arxiv.org/abs/2312.01409)
- **S5** — [CoAgent](https://arxiv.org/abs/2512.22536), [VIGOR](https://arxiv.org/abs/2603.16271), [InfLVG](https://arxiv.org/abs/2505.17574)
- **S6** — [Mitigating Compounding Error](https://arxiv.org/abs/2607.27036)

**V3 · Formal rules** — no methods.

**V4 · Goal attainment** · 42

- **S1** — [Orbis 2](https://arxiv.org/abs/2607.15898), [DriftWorld](https://arxiv.org/abs/2607.15065), [GigaWorld-Policy-0.5](https://arxiv.org/abs/2607.13960), [Ego-Dynamics-Augmented World Model](https://arxiv.org/abs/2607.13410), [DreamDojo](https://arxiv.org/abs/2602.06949), [Generative World Modelling for Humanoids](https://arxiv.org/abs/2510.07092), [Navigation World Models](https://arxiv.org/abs/2412.03572), [TeleWorld](https://arxiv.org/abs/2601.00051), [GigaWorld-0](https://arxiv.org/abs/2511.19861), [Adapting Video Diffusion Models](https://arxiv.org/abs/2410.12822), [GAIA-1](https://arxiv.org/abs/2309.17080), [GameNGen](https://arxiv.org/abs/2408.14837), [Genie](https://arxiv.org/abs/2402.15391), [UniSim](https://arxiv.org/abs/2310.06114), [DriveDreamer](https://arxiv.org/abs/2309.09777), [Drive-WM](https://arxiv.org/abs/2311.17918), [WorldDreamer](https://arxiv.org/abs/2402.17144), [Cosmos World Foundation Model](https://arxiv.org/abs/2501.03575)
- **S2** — [EA-WM](https://arxiv.org/abs/2606.13053)
- **S4** — [From Passive Video to Editable Experience](https://arxiv.org/abs/2607.26903), [ContactFlow](https://arxiv.org/abs/2607.26579), [DeVA](https://arxiv.org/abs/2607.24159), [Robot-Factored World Models](https://arxiv.org/abs/2607.22535), [Mind-Studio](https://arxiv.org/abs/2606.16070), [CausalDrive](https://arxiv.org/abs/2606.15341)
- **S5** — [PAVXploreRL](https://arxiv.org/abs/2607.16602), [Action Agent](https://arxiv.org/abs/2605.01477), [Grounding Video Models](https://arxiv.org/abs/2411.07223)
- **S6** — [EgoGenesis](https://arxiv.org/abs/2607.28243), [QQWorld](https://arxiv.org/abs/2607.28415), [Enfold](https://arxiv.org/abs/2607.26657), [Temporally Centered SIGReg Improves Multi-Task](https://arxiv.org/abs/2607.26924), [Temporal-Distance JEPA](https://arxiv.org/abs/2607.25337), [Reinformed Dreamer](https://arxiv.org/abs/2607.26040), [INTACT](https://arxiv.org/abs/2607.26056), [Concept-Guided Spatial Regularization](https://arxiv.org/abs/2607.15142), [Depth-Regularized JEPA World Models](https://arxiv.org/abs/2607.16314), [WAM4D](https://arxiv.org/abs/2606.14048), [V-JEPA 2](https://arxiv.org/abs/2506.09985), [DriveLaW](https://arxiv.org/abs/2512.23421), [Motus](https://arxiv.org/abs/2512.13030), [Video Prediction Policy](https://arxiv.org/abs/2412.14803)

**V5 · Procedure & order** · 7

- **S2** — [Automated Movie Generation](https://arxiv.org/abs/2503.07314), [MAViS](https://arxiv.org/abs/2508.08487), [StoryAgent](https://arxiv.org/abs/2411.04925), [Mora](https://arxiv.org/abs/2403.13248)
- **S5** — [ViMax](https://arxiv.org/abs/2606.07649), [Closed-Loop Triplet Synergistic Generation](https://arxiv.org/abs/2606.16184), [AesopAgent](https://arxiv.org/abs/2403.07952)

**V6 · Convention & intent** · 7

- **S2** — [DirectorLLM](https://arxiv.org/abs/2412.14484), [CineVerse](https://arxiv.org/abs/2504.19894), [Camera Artist](https://arxiv.org/abs/2604.09195), [DramaDirector](https://arxiv.org/abs/2606.24107)
- **S3** — [CANVAS](https://arxiv.org/abs/2604.13452)
- **S5** — [StoryBlender](https://arxiv.org/abs/2604.03315)
- **S6** — [Mental World Modeling](https://arxiv.org/abs/2607.27201)

**VX · General purpose** · 15

- **S3** — [Exploring MLLM-Diffusion Information Transfer](https://arxiv.org/abs/2512.11464), [MetaQueries](https://arxiv.org/abs/2504.06256), [CoCoVa](https://arxiv.org/abs/2511.02360), [Continuous Visual Tokens](https://arxiv.org/abs/2511.19418), [VTI-CoT](https://arxiv.org/abs/2606.05736), [Gen-VCoT](https://arxiv.org/abs/2606.16783), [ProLaViT](https://arxiv.org/abs/2607.02907)
- **S5** — [OpenCoF](https://arxiv.org/abs/2607.08763), [Self-Refining Sampling](https://arxiv.org/abs/2601.18577), [Verifiable Rewards](https://arxiv.org/abs/2605.15458), [UniT](https://arxiv.org/abs/2602.12279), [Video-T1](https://arxiv.org/abs/2503.18942), [Thinking in Frames](https://arxiv.org/abs/2601.21037), [Temporal Backtracking Search](https://arxiv.org/abs/2606.13861), [CollabVR](https://arxiv.org/abs/2605.08735)

**V0 · Outside the paradigm** · 17

- **S1** — [Visko Orbis 1.0](https://arxiv.org/abs/2607.26694), [Inferix](https://arxiv.org/abs/2511.20714), [ConsistI2V](https://arxiv.org/abs/2402.04324), [Video Diffusion Models (2022)](https://arxiv.org/abs/2204.03458), [Imagen Video](https://arxiv.org/abs/2210.02303), [Make-A-Video](https://arxiv.org/abs/2209.14792), [Phenaki](https://arxiv.org/abs/2210.02399), [VideoPoet](https://arxiv.org/abs/2312.14125), [Lumiere](https://arxiv.org/abs/2401.12945), [Stable Video Diffusion](https://arxiv.org/abs/2311.15127), [Text2Video-Zero](https://arxiv.org/abs/2303.13439), [VideoComposer](https://arxiv.org/abs/2306.02018), [AnimateDiff](https://arxiv.org/abs/2307.04725), [DragNUWA](https://arxiv.org/abs/2308.08089), [MotionCtrl](https://arxiv.org/abs/2312.03641), [CameraCtrl](https://arxiv.org/abs/2404.02101)
- **S5** — [Inference-Time Scaling for Joint](https://arxiv.org/abs/2606.03183)
<!-- /auto:prob -->

<a name="2."></a>
## 2. Sources of Reasoning Competence


The spine of the survey. Methods are filed by the source their competence comes from, and cross-indexed by carrier in [Section 3](#3.) and by task class in [Section 1](#1.).

<a name="2.1."></a>
### 2.1. S1: Regularities Absorbed from Data

Pretraining itself. Enough video contains enough falling, colliding and pouring that a generator absorbs a broad prior over dynamics without being told a law — broad coverage with a low ceiling, which is the profile that motivates every other source.

<!-- auto:s1 -->
*41 methods, in 7 families. Tags give the carrier the intermediate state is written in ([§3](#3.)) and the grounding of the problem targeted ([§1.7](#1.7.)); an S1 method has no carrier by definition.*

**Text-to-Video Foundations** · 9

- [ConsistI2V: Enhancing Visual Consistency for Image-to-Video Generation](https://arxiv.org/abs/2402.04324) · arXiv 2024 · `V0`
- [Video Diffusion Models](https://arxiv.org/abs/2204.03458) · arXiv 2022 · `V0`
- [Imagen Video: High Definition Video Generation with Diffusion Models](https://arxiv.org/abs/2210.02303) · arXiv 2022 · `V0`
- [Make-A-Video: Text-to-Video Generation without Text-Video Data](https://arxiv.org/abs/2209.14792) · arXiv 2022 · `V0`
- [VideoPoet: A Large Language Model for Zero-Shot Video Generation](https://arxiv.org/abs/2312.14125) · arXiv 2023 · `V0`
- [Lumiere: A Space-Time Diffusion Model for Video Generation](https://arxiv.org/abs/2401.12945) · arXiv 2024 · `V0`
- [Stable Video Diffusion: Scaling Latent Video Diffusion Models to Large Datasets](https://arxiv.org/abs/2311.15127) · arXiv 2023 · `V0`
- [Text2Video-Zero: Text-to-Image Diffusion Models are Zero-Shot Video Generators](https://arxiv.org/abs/2303.13439) · arXiv 2023 · `V0`
- [AnimateDiff: Animate Your Personalized Text-to-Image Diffusion Models without Specific Tuning](https://arxiv.org/abs/2307.04725) · arXiv 2023 · `V0`

**Long & Streaming Video** · 6

- [Visko Orbis 1.0: A Live Model for Real-Time Interactive Long Video Generation](https://arxiv.org/abs/2607.26694) · arXiv 2026 · `V0`
- [Diffusion over Diffusion for eXtremely Long Video Generation](https://arxiv.org/abs/2303.12346) · arXiv 2023 · `V2`
- [Phenaki: Variable Length Video Generation From Open Domain Textual Description](https://arxiv.org/abs/2210.02399) · arXiv 2022 · `V0`
- [FreeNoise: Tuning-Free Longer Video Diffusion via Noise Rescheduling](https://arxiv.org/abs/2310.15169) · arXiv 2023 · `V2`
- [FIFO-Diffusion: Generating Infinite Videos from Text without Training](https://arxiv.org/abs/2405.11473) · arXiv 2024 · `V2`
- [StreamingT2V: Consistent, Dynamic, and Extendable Long Video Generation from Text](https://arxiv.org/abs/2403.14773) · arXiv 2024 · `V2`

**End-to-End Control Interfaces** · 4

- [VideoComposer: Compositional Video Synthesis with Motion Controllability](https://arxiv.org/abs/2306.02018) · arXiv 2023 · `V0`
- [DragNUWA: Fine-grained Control in Video Generation by Integrating Text, Image, and Trajectory](https://arxiv.org/abs/2308.08089) · arXiv 2023 · `V0`
- [MotionCtrl: A Unified and Flexible Motion Controller for Video Generation](https://arxiv.org/abs/2312.03641) · arXiv 2023 · `V0`
- [CameraCtrl: Enabling Camera Control for Text-to-Video Generation](https://arxiv.org/abs/2404.02101) · arXiv 2024 · `V0`

**General & Interactive Simulators** · 6

- [Adapting Video Diffusion Models to World Models](https://arxiv.org/abs/2410.12822) · arXiv 2024 · `V4`
- [GameNGen: Diffusion Models Are Real-Time Game Engines](https://arxiv.org/abs/2408.14837) · arXiv 2024 · `V4`
- [Genie: Generative Interactive Environments](https://arxiv.org/abs/2402.15391) · arXiv 2024 · `V4`
- [UniSim: Learning Interactive Real-World Simulators](https://arxiv.org/abs/2310.06114) · arXiv 2023 · `V4`
- [WorldDreamer: Towards General World Models for Video Generation via Predicting Masked Tokens](https://arxiv.org/abs/2402.17144) · arXiv 2024 · `V4`
- [Cosmos World Foundation Model Platform for Physical AI](https://arxiv.org/abs/2501.03575) · arXiv 2025 · `V4`

**Driving World Models** · 6

- [Orbis 2: A Hierarchical World Model for Driving](https://arxiv.org/abs/2607.15898) · arXiv 2026 · `V4`
- [DriftWorld: Fast World Modeling through Drifting](https://arxiv.org/abs/2607.15065) · arXiv 2026 · `V4`
- [Ego-Dynamics-Augmented World Model for Autonomous Driving with Zero-Shot Cross-Chassis Adaptation](https://arxiv.org/abs/2607.13410) · arXiv 2026 · `V4`
- [GAIA-1: A Generative World Model for Autonomous Driving](https://arxiv.org/abs/2309.17080) · arXiv 2023 · `V4`
- [DriveDreamer: Towards Real-world-driven World Models for Autonomous Driving](https://arxiv.org/abs/2309.09777) · arXiv 2023 · `V4`
- [Drive-WM: Driving into the Future with Multiview Visual Forecasting and Planning](https://arxiv.org/abs/2311.17918) · arXiv 2023 · `V4`

**Robot & Embodied World Models** · 6

- [GigaWorld-Policy-0.5: A Faster and Stronger WAM Empowered by AutoResearch](https://arxiv.org/abs/2607.13960) · arXiv 2026 · `V4`
- [DreamDojo: A Generalist Robot World Model from Large-Scale Human Videos](https://arxiv.org/abs/2602.06949) · arXiv 2026 · `V4`
- [Generative World Modelling for Humanoids: 1X World Model Challenge Technical Report](https://arxiv.org/abs/2510.07092) · arXiv 2025 · `V4`
- [Navigation World Models](https://arxiv.org/abs/2412.03572) · arXiv 2024 · `V4`
- [TeleWorld: Towards Dynamic Multimodal Synthesis with a 4D World Model](https://arxiv.org/abs/2601.00051) · arXiv 2026 · `V4`
- [GigaWorld-0: World Models as Data Engine to Empower Embodied AI](https://arxiv.org/abs/2511.19861) · arXiv 2025 · `V4`

**Memory & Error Control (training-free)** · 4

- [FreqForcing: Autoregressive Long Video Generation via Spectral Self-Anchoring](https://arxiv.org/abs/2607.27110) · arXiv 2026 · `V2`
- [TaoMate: Anchor-Guided Memory Bridging Evolving and Reference States for Real-Time Audio-Video Digital Human Generation](https://arxiv.org/abs/2607.24359) · arXiv 2026 · `V2`
- [Inferix: A Block-Diffusion based Next-Generation Inference Engine for World Simulation](https://arxiv.org/abs/2511.20714) · arXiv 2025 · `V0`
- [Advancing Narrative Long Video Generation via Training-Free Identity-Aware Memory](https://arxiv.org/abs/2605.18733) · arXiv 2026 · `V2`
<!-- /auto:s1 -->

<a name="2.2."></a>
### 2.2. S2: Language Models

Entering as a rewriter, which enriches an underspecified prompt with the physical effects a scene implies, or as a planner, which decomposes a request into a shot list, scene graph or layout sequence.

<!-- auto:s2 -->
*16 methods, in 5 families. Tags give the carrier the intermediate state is written in ([§3](#3.)) and the grounding of the problem targeted ([§1.7](#1.7.)); an S1 method has no carrier by definition.*

**Prompt-Level Physics Injection** · 3

- [PhyT2V: LLM-Guided Iterative Self-Refinement for Physics-Grounded Text-to-Video Generation](https://arxiv.org/abs/2412.00596) · arXiv 2024 · `natural language` `V1`
- [WISA: World Simulator Assistant for Physics-Aware Text-to-Video Generation](https://arxiv.org/abs/2503.08153) · arXiv 2025 · `natural language` `V1`
- [PhysVid: Physics Aware Local Conditioning for Generative Video Models](https://arxiv.org/abs/2603.26285) · arXiv 2026 · `natural language` `V1`

**LLM Layout & Scene Planning** · 4

- [LLM-grounded Video Diffusion Models](https://arxiv.org/abs/2309.17444) · arXiv 2023 · `structured symbols` `V2`
- [VideoDirectorGPT: Consistent Multi-scene Video Generation via LLM-Guided Planning](https://arxiv.org/abs/2309.15091) · arXiv 2023 · `structured symbols` `V2`
- [DirectorLLM for Human-Centric Video Generation](https://arxiv.org/abs/2412.14484) · arXiv 2024 · `structured symbols` `V6`
- [CinemaTraj: Composing Atomic Camera Trajectories for 3D Scenes with LLM Agents](https://arxiv.org/abs/2607.26910) · arXiv 2026 · `structured symbols` `V2`

**Multi-Agent Narrative Planning** · 5

- [Automated Movie Generation via Multi-Agent CoT Planning](https://arxiv.org/abs/2503.07314) · arXiv 2025 · `structured symbols` `V5`
- [Camera Artist: A Multi-Agent Framework for Cinematic Language Storytelling Video Generation](https://arxiv.org/abs/2604.09195) · arXiv 2026 · `structured symbols` `V6`
- [DramaDirector: Geometry-Guided Short Drama Generation](https://arxiv.org/abs/2606.24107) · arXiv 2026 · `structured symbols` `V6`
- [StoryAgent: Customized Storytelling Video Generation via Multi-Agent Collaboration](https://arxiv.org/abs/2411.04925) · arXiv 2024 · `structured symbols` `V5`
- [Mora: Enabling Generalist Video Generation via A Multi-Agent Framework](https://arxiv.org/abs/2403.13248) · arXiv 2024 · `structured symbols` `V5`

**Event & Task Structure** · 2

- [Chain of Event-Centric Causal Thought for Physically Plausible Video Generation](https://arxiv.org/abs/2603.09094) · arXiv 2026 · `visual states` `V1`
- [EA-WM: Event-Aware World Models with Task-Specification Grounding for Long-Horizon Manipulation](https://arxiv.org/abs/2606.13053) · arXiv 2026 · `structured symbols` `V4`

**Keyframe-Level Story Planning** · 2

- [MAViS: A Multi-Agent Framework for Long-Sequence Video Storytelling](https://arxiv.org/abs/2508.08487) · arXiv 2025 · `visual states` `V5`
- [CineVerse: Consistent Keyframe Synthesis for Cinematic Scene Composition](https://arxiv.org/abs/2504.19894) · arXiv 2025 · `visual states` `V6`
<!-- /auto:s2 -->

<a name="2.3."></a>
### 2.3. S3: Multimodal Models

The only source that genuinely exercises the carrier axis, appearing as a critic that inspects generated keyframes, a planner grounded in observed pixels, and a latent interface that conditions the generator without passing through text.

<!-- auto:s3 -->
*17 methods, in 7 families. Tags give the carrier the intermediate state is written in ([§3](#3.)) and the grounding of the problem targeted ([§1.7](#1.7.)); an S1 method has no carrier by definition.*

**VLM Critique & Self-Refinement** · 1

- [Bootstrapping Physics-Grounded Video Generation through VLM-Guided Iterative Self-Refinement](https://arxiv.org/abs/2511.20280) · arXiv 2025 · `natural language` `V1`

**VLM Physical Reasoning** · 4

- [VLIPP: Towards Physically Plausible Video Generation with Vision and Language Informed Physical Prior](https://arxiv.org/abs/2503.23368) · arXiv 2025 · `structured symbols` `V1`
- [SiPhy: Single-Image Physical Property Reasoning](https://arxiv.org/abs/2607.22355) · arXiv 2026 · `structured symbols` `V1`
- [Physics Context Builders: A Modular Framework for Physical Reasoning in Vision-Language Models](https://arxiv.org/abs/2412.08619) · arXiv 2024 · `structured symbols` `V1`
- [Compositional Physical Reasoning of Objects and Events from Videos](https://arxiv.org/abs/2408.02687) · arXiv 2024 · `structured symbols` `V1`

**Visual Chain-of-Thought Keyframes** · 3

- [VChain: Chain-of-Visual-Thought for Reasoning in Video Generation](https://arxiv.org/abs/2510.05094) · arXiv 2025 · `visual states` `V1`
- [CANVAS: Continuity-Aware Narratives via Visual Agentic Storyboarding](https://arxiv.org/abs/2604.13452) · arXiv 2026 · `visual states` `V6`
- [VIPER: Visual In-Context Physics Reasoning for Physically Plausible Video Generation](https://arxiv.org/abs/2607.23472) · arXiv 2026 · `visual states` `V1`

**Interleaved Visual-Textual CoT** · 2

- [VTI-CoT: Visual-Textual Interleaved Chain of Thought for Video Reasoning](https://arxiv.org/abs/2606.05736) · arXiv 2026 · `visual states` `VX`
- [Gen-VCoT: Generative Visual Chain-of-Thought Reasoning via DiffusionBased RGB Intermediate Representations](https://arxiv.org/abs/2606.16783) · arXiv 2026 · `visual states` `VX`

**MLLM Narrative Conditioning** · 1

- [Narrative Weaver: Towards Controllable Long-Range Visual Consistency with Multi-Modal Conditioning](https://arxiv.org/abs/2603.06688) · arXiv 2026 · `structured symbols` `V2`

**MLLM--Diffusion Latent Interfaces** · 3

- [Exploring MLLM-Diffusion Information Transfer with MetaCanvas](https://arxiv.org/abs/2512.11464) · arXiv 2025 · `continuous latents` `VX`
- [Think Before You Diffuse: Infusing Physical Rules into Video Diffusion2025](https://arxiv.org/abs/2505.21653) · arXiv 2025 · `continuous latents` `V1`
- [Transfer between Modalities with MetaQueries](https://arxiv.org/abs/2504.06256) · arXiv 2025 · `continuous latents` `VX`

**Continuous Visual Thought Tokens** · 3

- [CoCoVa: Chain of Continuous Vision-Language Thought for Latent Space Reasoning](https://arxiv.org/abs/2511.02360) · arXiv 2025 · `continuous latents` `VX`
- [Chain-of-Visual-Thought: Teaching VLMs to See and Think Better with Continuous Visual Tokens](https://arxiv.org/abs/2511.19418) · arXiv 2025 · `continuous latents` `VX`
- [ProLaViT: Learning Progressive Latent Visual Thoughts in Structured Latent Space](https://arxiv.org/abs/2607.02907) · arXiv 2026 · `continuous latents` `VX`
<!-- /auto:s3 -->

<a name="2.4."></a>
### 2.4. S4: Simulators and Formal Systems

Reasoning imported rather than learned: rigid-body engines, particle and Gaussian representations, symbolic equation discovery. Correct by construction for the phenomena they model, and silent outside them.

<!-- auto:s4 -->
*33 methods, in 8 families. Tags give the carrier the intermediate state is written in ([§3](#3.)) and the grounding of the problem targeted ([§1.7](#1.7.)); an S1 method has no carrier by definition.*

**Rigid-Body & Physics Engines** · 5

- [PhysGen: Rigid-Body Physics-Grounded Image-to-Video Generation](https://arxiv.org/abs/2409.18964) · arXiv 2024 · `structured symbols` `V1`
- [PhysChoreo: Physics-Controllable Video Generation with Part-Aware Semantic Grounding](https://arxiv.org/abs/2511.20562) · arXiv 2025 · `structured symbols` `V1`
- [NewtonGen: Physics-Consistent and Controllable Text-to-Video Generation via Neural Newtonian Dynamics](https://arxiv.org/abs/2509.21309) · arXiv 2025 · `structured symbols` `V1`
- [PhysCtrl: Generative Physics for Controllable and Physics-Grounded Video Generation](https://arxiv.org/abs/2509.20358) · arXiv 2025 · `structured symbols` `V1`
- [Learning to Generate Object Interactions with Physics-Guided Video Diffusion](https://arxiv.org/abs/2510.02284) · arXiv 2025 · `structured symbols` `V1`

**Parameters & Equation Discovery** · 5

- [Learning Explicit Physical Parameter Control and Benchmarking for Video Generation](https://arxiv.org/abs/2607.18924) · arXiv 2026 · `structured symbols` `V1`
- [Physics-Grounded Motion Forecasting via Equation Discovery for Trajectory-Guided Image-to-Video Generation](https://arxiv.org/abs/2507.06830) · arXiv 2025 · `structured symbols` `V1`
- [Goal Force: Teaching Video Models To Accomplish Physics-Conditioned Goals](https://arxiv.org/abs/2601.05848) · arXiv 2026 · `structured symbols` `V1`
- [DeforM: Reasoning-Guided Physics-Aware Video Generation via Spatial-Temporal Masking](https://arxiv.org/abs/2607.18664) · arXiv 2026 · `structured symbols` `V1`
- [PhysEditWorld: A Large-Scale Dataset Toward Physics-Editable World Models](https://arxiv.org/abs/2606.26694) · arXiv 2026 · `structured symbols` `V1`

**Physical Language & Continuous Dynamics** · 3

- [PhiZero: A World Model Built Around Physical Language](https://arxiv.org/abs/2607.28624) · arXiv 2026 · `structured symbols` `V1`
- [ODEWorld: A Continuous Predictive Architecture via Physical-Time Flow](https://arxiv.org/abs/2607.27924) · arXiv 2026 · `structured symbols` `V1`
- [APT: Atomic Physical Transitions for Causal Video Generation](https://arxiv.org/abs/2606.18586) · arXiv 2026 · `structured symbols` `V1`

**3D/4D Geometric Conditioning** · 6

- [ReVision: Refining Video Diffusion with Explicit 3D Motion Modeling](https://arxiv.org/abs/2504.21855) · arXiv 2025 · `structured symbols` `V2`
- [PhysGM: Large Physical Gaussian Model for Feed-Forward 4D Synthesis](https://arxiv.org/abs/2508.13911) · arXiv 2025 · `structured symbols` `V1`
- [3D Scene Prompting for Scene-Consistent Camera-Controllable Video Generation](https://arxiv.org/abs/2510.14945) · arXiv 2025 · `structured symbols` `V2`
- [Physics3D: Learning Physical Properties from 3D Assets](https://arxiv.org/abs/2406.04338) · arXiv 2024 · `structured symbols` `V1`
- [Diffusion as Shader: 3D-aware Video Diffusion for Versatile Video Generation Control](https://arxiv.org/abs/2501.03847) · arXiv 2025 · `structured symbols` `V2`
- [Generative Rendering: Controllable 4D-Guided Video Generation with 2D Diffusion Models](https://arxiv.org/abs/2312.01409) · arXiv 2023 · `structured symbols` `V2`

**Geometry-Guided Keyframes** · 3

- [PhyRPR: Training-Free Physics-Constrained Video Generation](https://arxiv.org/abs/2601.09255) · arXiv 2026 · `visual states` `V1`
- [CausalMotion: Structured Physical Reasoning as Keyframe and Trajectory Guidance for Training-Free Video Generation](https://arxiv.org/abs/2606.14317) · arXiv 2026 · `visual states` `V1`
- [OrthoPhys: Physically Plausible Video Generation with Orthogonal-View Geometry Guidance](https://arxiv.org/abs/2603.18639) · arXiv 2026 · `visual states` `V2`

**Latent Physical State** · 4

- [Phantom: Physics-Infused Video Generation via Joint Modeling of Visual and Latent Physical Dynamics](https://arxiv.org/abs/2604.08503) · arXiv 2026 · `continuous latents` `V1`
- [PhysRAG: Enhancing Physics-Awareness in Video Generation via RetrievalAugmented Generation](https://arxiv.org/abs/2606.26916) · arXiv 2026 · `continuous latents` `V1`
- [PhysVideoGenerator: Towards Physically Aware Video Generation via Latent Physics Guidance](https://arxiv.org/abs/2601.03665) · arXiv 2026 · `continuous latents` `V1`
- [DeVA: Decoupled Video-Action Model with physical guidance for robot policy learning](https://arxiv.org/abs/2607.24159) · arXiv 2026 · `continuous latents` `V4`

**Embodied Physical Grounding** · 4

- [From Passive Video to Editable Experience: Physically Grounded Experience Synthesis for Embodied Intelligence](https://arxiv.org/abs/2607.26903) · arXiv 2026 · `structured symbols` `V4`
- [ContactFlow: A video action conditioning that transfers across embodiments](https://arxiv.org/abs/2607.26579) · arXiv 2026 · `structured symbols` `V4`
- [Robot-Factored World Models via Robot Rendering](https://arxiv.org/abs/2607.22535) · arXiv 2026 · `structured symbols` `V4`
- [CausalDrive: Real-time Causal World Models for Autonomous Driving](https://arxiv.org/abs/2606.15341) · arXiv 2026 · `structured symbols` `V4`

**Simulator-in-the-Loop** · 3

- [PhyMAGIC: Physical Motion-Aware Generative Inference with Confidenceguided LLM](https://arxiv.org/abs/2505.16456) · arXiv 2025 · `the generation itself` `V1`
- [Physical Simulator In-the-Loop Video Generation](https://arxiv.org/abs/2603.06408) · arXiv 2026 · `the generation itself` `V1`
- [Mind-Studio: Executable World Models with Lookahead Evaluation for Partially Observable Games](https://arxiv.org/abs/2606.16070) · arXiv 2026 · `the generation itself` `V4`
<!-- /auto:s4 -->

<a name="2.5."></a>
### 2.5. S5: Search, Verification and Reward

Reasoning produced by search rather than construction — test-time scaling, backtracking, verifiable and physics-aware rewards, process-level supervision. Only ever as good as the verifier.

<!-- auto:s5 -->
*25 methods, in 4 families. Tags give the carrier the intermediate state is written in ([§3](#3.)) and the grounding of the problem targeted ([§1.7](#1.7.)); an S1 method has no carrier by definition.*

**Verifiable Rewards & RL** · 7

- [PhysRVG: Physics-Aware Unified Reinforcement Learning for Video Generative Models](https://arxiv.org/abs/2601.11087) · arXiv 2026 · `the generation itself` `V1`
- [Video Models Can Reason with Verifiable Rewards](https://arxiv.org/abs/2605.15458) · arXiv 2026 · `the generation itself` `VX`
- [PhyGDPO: Physics-Aware Groupwise Direct Preference Optimization for Physically Consistent Text-to-Video Generation](https://arxiv.org/abs/2512.24551) · arXiv 2025 · `the generation itself` `V1`
- [Improving the Physics of Video Generation with VJEPA-2 Reward Signal](https://arxiv.org/abs/2510.21840) · arXiv 2025 · `the generation itself` `V1`
- [Reasoning Physical Video Generation with Diffusion Timestep Tokens via Reinforcement Learning](https://arxiv.org/abs/2504.15932) · arXiv 2025 · `the generation itself` `V1`
- [PAVXploreRL: Physical-Action-Visual World Model Reinforcement Learning with Action Exploration](https://arxiv.org/abs/2607.16602) · arXiv 2026 · `the generation itself` `V4`
- [InfLVG: Reinforce Inference-Time Consistent Long Video Generation with GRPO](https://arxiv.org/abs/2505.17574) · arXiv 2025 · `the generation itself` `V2`

**Test-Time Scaling & Search** · 7

- [Self-Refining Video Sampling](https://arxiv.org/abs/2601.18577) · arXiv 2026 · `the generation itself` `VX`
- [UniT: Unified Multimodal Chain-of-Thought Test-time Scaling](https://arxiv.org/abs/2602.12279) · arXiv 2026 · `the generation itself` `VX`
- [Video-T1: Test-Time Scaling for Video Generation](https://arxiv.org/abs/2503.18942) · arXiv 2025 · `the generation itself` `VX`
- [Thinking in Frames: How Visual Context and Test-Time Scaling Empower Video Reasoning](https://arxiv.org/abs/2601.21037) · arXiv 2026 · `the generation itself` `VX`
- [Temporal Backtracking Search for Test-time Generative Video Reasoning](https://arxiv.org/abs/2606.13861) · arXiv 2026 · `the generation itself` `VX`
- [Inference-Time Scaling for Joint Audio-Video Generation](https://arxiv.org/abs/2606.03183) · arXiv 2026 · `the generation itself` `V0`
- [VIGOR: VIdeo Geometry-Oriented Reward for Temporal Generative Alignment](https://arxiv.org/abs/2603.16271) · arXiv 2026 · `the generation itself` `V2`

**Agentic Planning & Closed Loops** · 8

- [NEWTON: Agentic Planning for Physically Grounded Video Generation](https://arxiv.org/abs/2605.18396) · arXiv 2026 · `the generation itself` `V1`
- [ViMax: Agentic Video Generation](https://arxiv.org/abs/2606.07649) · arXiv 2026 · `the generation itself` `V5`
- [Closed-Loop Triplet Synergistic Generation for Long-Form Video](https://arxiv.org/abs/2606.16184) · arXiv 2026 · `the generation itself` `V5`
- [StoryBlender: Inter-Shot Consistent and Editable 3D Storyboard with Spatial-temporal Dynamics](https://arxiv.org/abs/2604.03315) · arXiv 2026 · `the generation itself` `V6`
- [CoAgent: Collaborative Planning and Consistency Agent for Coherent Video Generation](https://arxiv.org/abs/2512.22536) · arXiv 2025 · `the generation itself` `V2`
- [AesopAgent: Agent-driven Evolutionary System on Story-to-Video Production](https://arxiv.org/abs/2403.07952) · arXiv 2024 · `the generation itself` `V5`
- [CollabVR: Collaborative Video Reasoning with Vision-Language and Video Generation Models](https://arxiv.org/abs/2605.08735) · arXiv 2026 · `the generation itself` `VX`
- [Action Agent: Agentic Video Generation Meets Flow-Constrained Diffusion](https://arxiv.org/abs/2605.01477) · arXiv 2026 · `the generation itself` `V4`

**Verification-Guided Generation** · 3

- [OpenCoF: Learning to Reason Through Video Generation](https://arxiv.org/abs/2607.08763) · arXiv 2026 · `the generation itself` `VX`
- [Planning with Sketch-Guided Verification for Physics-Aware Video Generation](https://arxiv.org/abs/2511.17450) · arXiv 2025 · `visual states` `V1`
- [Grounding Video Models to Actions through Goal-Conditioned Exploration](https://arxiv.org/abs/2411.07223) · arXiv 2024 · `structured symbols` `V4`
<!-- /auto:s5 -->

<a name="2.6."></a>
### 2.6. S6: Self-Supervised Prediction

Competence installed during training through an auxiliary predictive objective. The exact complement of S4: it degrades gracefully rather than falling silent, and buys that generality by being impossible to audit.

<!-- auto:s6 -->
*21 methods, in 4 families. Tags give the carrier the intermediate state is written in ([§3](#3.)) and the grounding of the problem targeted ([§1.7](#1.7.)); an S1 method has no carrier by definition.*

**Feature & Relational Alignment** · 5

- [VideoREPA: Learning Physics for Video Generation through Relational Alignment with Foundation Models](https://arxiv.org/abs/2505.23656) · arXiv 2025 · `continuous latents` `V1`
- [PhysAlign: Physics-Coherent Image-to-Video Generation through Feature and 3D Representation Alignment](https://arxiv.org/abs/2603.13770) · arXiv 2026 · `continuous latents` `V1`
- [Physics-Informed Video Generation via Mixture-of-Experts Latent Alignment](https://arxiv.org/abs/2606.04737) · arXiv 2026 · `continuous latents` `V1`
- [ProPhy: Progressive Physical Alignment for Dynamic World Simulation](https://arxiv.org/abs/2512.05564) · arXiv 2025 · `continuous latents` `V1`
- [DiReCT: Disentangled Regularization of Contrastive Trajectories for Physics-Refined Video Generation](https://arxiv.org/abs/2603.25931) · arXiv 2026 · `continuous latents` `V1`

**JEPA & Predictive Representations** · 7

- [QQWorld: Quantile-Quantile Matching for World Model Regularization](https://arxiv.org/abs/2607.28415) · arXiv 2026 · `continuous latents` `V4`
- [Temporally Centered SIGReg Improves Multi-Task World Model Learning: From Analysis to Method](https://arxiv.org/abs/2607.26924) · arXiv 2026 · `continuous latents` `V4`
- [Temporal-Distance JEPA: Plan-Aware Representation Learning for Latent World Model Predictive Control](https://arxiv.org/abs/2607.25337) · arXiv 2026 · `continuous latents` `V4`
- [INTACT: Isomorphic Intent-to-Action Learning for Search-Free World Models](https://arxiv.org/abs/2607.26056) · arXiv 2026 · `continuous latents` `V4`
- [Concept-Guided Spatial Regularization for World Models in Atari Pong](https://arxiv.org/abs/2607.15142) · arXiv 2026 · `continuous latents` `V4`
- [Depth-Regularized JEPA World Models Learn More Transferable Representations from Real Outdoor Robot Data](https://arxiv.org/abs/2607.16314) · arXiv 2026 · `continuous latents` `V4`
- [V-JEPA 2: Self-Supervised Video Models Enable Understanding, Prediction and Planning](https://arxiv.org/abs/2506.09985) · arXiv 2025 · `continuous latents` `V4`

**Latent Action & Video-Action Models** · 5

- [EgoGenesis: Egocentric World-Action Modeling with Online Anchored Projective Memory and Action-3D RoPE](https://arxiv.org/abs/2607.28243) · arXiv 2026 · `continuous latents` `V4`
- [WAM4D: Fast 4D World Action Model via Spatial Register Tokens](https://arxiv.org/abs/2606.14048) · arXiv 2026 · `continuous latents` `V4`
- [DriveLaW: Unifying Planning and Video Generation in a Latent Driving World](https://arxiv.org/abs/2512.23421) · arXiv 2025 · `continuous latents` `V4`
- [Motus: A Unified Latent Action World Model](https://arxiv.org/abs/2512.13030) · arXiv 2025 · `continuous latents` `V4`
- [Video Prediction Policy: A Generalist Robot Policy with Predictive Visual Representations](https://arxiv.org/abs/2412.14803) · arXiv 2024 · `continuous latents` `V4`

**Regularisation for Long Rollout** · 4

- [Enfold: Folding World-Generator Computation into Predictive Representations for Efficient Embodied Control](https://arxiv.org/abs/2607.26657) · arXiv 2026 · `continuous latents` `V4`
- [Mitigating Compounding Error via Video Representation Regularization](https://arxiv.org/abs/2607.27036) · arXiv 2026 · `continuous latents` `V2`
- [Mental World Modeling](https://arxiv.org/abs/2607.27201) · arXiv 2026 · `continuous latents` `V6`
- [Reinformed Dreamer: An Asymmetric World Model Efficiently Trained through Latent Guidance](https://arxiv.org/abs/2607.26040) · arXiv 2026 · `continuous latents` `V4`
<!-- /auto:s6 -->

<a name="3."></a>
## 3. Methods: Carriers and Arrangements


A cross-index into [Section 2](#2.), not a second library: every method is listed in full under its source and appears here only by name. A carrier is the medium an *inferred* intermediate state is written in, so it is a property of methods alone — benchmarks and surveys have none — and the six lists below partition the same 153 methods. Each is grouped by source, which is what makes the correlation between the two axes visible: language and symbols come overwhelmingly from S2 and S4, latents from S3 and S6, and only the multimodal source spreads across all four.

<a name="3.1."></a>
### 3.1. Natural Language

A rewritten prompt, an enumerated list of physical effects, a critique fed back into the next attempt.

<!-- auto:cl -->
*4 methods. Grouped by the source that writes the text.*

- **S2** — [PhyT2V](https://arxiv.org/abs/2412.00596), [WISA](https://arxiv.org/abs/2503.08153), [PhysVid](https://arxiv.org/abs/2603.26285)
- **S3** — [VLM Self-Refinement](https://arxiv.org/abs/2511.20280)
<!-- /auto:cl -->

<a name="3.2."></a>
### 3.2. Structured Symbols

Machine-readable but not linguistic: a scene layout, a set of masses and friction coefficients, a trajectory, a camera path, an executable program.

<!-- auto:cs -->
*39 methods. Grouped by the source that emits the symbols.*

- **S2** — [LLM-grounded Video Diffusion](https://arxiv.org/abs/2309.17444), [VideoDirectorGPT](https://arxiv.org/abs/2309.15091), [DirectorLLM](https://arxiv.org/abs/2412.14484), [Automated Movie Generation](https://arxiv.org/abs/2503.07314), [Camera Artist](https://arxiv.org/abs/2604.09195), [DramaDirector](https://arxiv.org/abs/2606.24107), [StoryAgent](https://arxiv.org/abs/2411.04925), [Mora](https://arxiv.org/abs/2403.13248), [CinemaTraj](https://arxiv.org/abs/2607.26910), [EA-WM](https://arxiv.org/abs/2606.13053)
- **S3** — [Narrative Weaver](https://arxiv.org/abs/2603.06688), [VLIPP](https://arxiv.org/abs/2503.23368), [SiPhy](https://arxiv.org/abs/2607.22355), [Physics Context Builders](https://arxiv.org/abs/2412.08619), [Compositional Physical Reasoning](https://arxiv.org/abs/2408.02687)
- **S4** — [PhysGen](https://arxiv.org/abs/2409.18964), [PhysChoreo](https://arxiv.org/abs/2511.20562), [NewtonGen](https://arxiv.org/abs/2509.21309), [PhysCtrl](https://arxiv.org/abs/2509.20358), [PhyParam](https://arxiv.org/abs/2607.18924), [Equation Discovery + Trajectory](https://arxiv.org/abs/2507.06830), [Physics-Guided Interactions](https://arxiv.org/abs/2510.02284), [Goal Force](https://arxiv.org/abs/2601.05848), [PhiZero](https://arxiv.org/abs/2607.28624), [ODEWorld](https://arxiv.org/abs/2607.27924), [From Passive Video to Editable Experience](https://arxiv.org/abs/2607.26903), [ContactFlow](https://arxiv.org/abs/2607.26579), [Robot-Factored World Models](https://arxiv.org/abs/2607.22535), [DeforM](https://arxiv.org/abs/2607.18664), [PhysEditWorld](https://arxiv.org/abs/2606.26694), [CausalDrive](https://arxiv.org/abs/2606.15341), [APT](https://arxiv.org/abs/2606.18586), [ReVision](https://arxiv.org/abs/2504.21855), [PhysGM](https://arxiv.org/abs/2508.13911), [3D Scene Prompting](https://arxiv.org/abs/2510.14945), [Physics3D](https://arxiv.org/abs/2406.04338), [Diffusion as Shader](https://arxiv.org/abs/2501.03847), [Generative Rendering](https://arxiv.org/abs/2312.01409)
- **S5** — [Grounding Video Models](https://arxiv.org/abs/2411.07223)
<!-- /auto:cs -->

<a name="3.3."></a>
### 3.3. Visual States

The intermediate state is itself an image: keyframes, storyboards, sketches, coarse renderings inspected and revised before the full output is produced.

<!-- auto:cv -->
*12 methods. Grouped by the source that draws the state.*

- **S2** — [Event-Centric Causal Thought](https://arxiv.org/abs/2603.09094), [MAViS](https://arxiv.org/abs/2508.08487), [CineVerse](https://arxiv.org/abs/2504.19894)
- **S3** — [VChain](https://arxiv.org/abs/2510.05094), [CANVAS](https://arxiv.org/abs/2604.13452), [VTI-CoT](https://arxiv.org/abs/2606.05736), [Gen-VCoT](https://arxiv.org/abs/2606.16783), [VIPER (2026)](https://arxiv.org/abs/2607.23472)
- **S4** — [PhyRPR](https://arxiv.org/abs/2601.09255), [CausalMotion](https://arxiv.org/abs/2606.14317), [OrthoPhys](https://arxiv.org/abs/2603.18639)
- **S5** — [Planning with Sketch-Guided Verification](https://arxiv.org/abs/2511.17450)
<!-- /auto:cv -->

<a name="3.4."></a>
### 3.4. Continuous Latents

A feature bank with no human-readable form, transferred from a multimodal model or a predictive encoder into the generator.

<!-- auto:cz -->
*31 methods. Grouped by the source the features come from.*

- **S3** — [Exploring MLLM-Diffusion Information Transfer](https://arxiv.org/abs/2512.11464), [Think Before You Diffuse](https://arxiv.org/abs/2505.21653), [MetaQueries](https://arxiv.org/abs/2504.06256), [CoCoVa](https://arxiv.org/abs/2511.02360), [Continuous Visual Tokens](https://arxiv.org/abs/2511.19418), [ProLaViT](https://arxiv.org/abs/2607.02907)
- **S4** — [Phantom](https://arxiv.org/abs/2604.08503), [PhysRAG](https://arxiv.org/abs/2606.26916), [PhysVideoGenerator](https://arxiv.org/abs/2601.03665), [DeVA](https://arxiv.org/abs/2607.24159)
- **S6** — [VideoREPA](https://arxiv.org/abs/2505.23656), [PhysAlign](https://arxiv.org/abs/2603.13770), [MoE Latent Alignment](https://arxiv.org/abs/2606.04737), [EgoGenesis](https://arxiv.org/abs/2607.28243), [QQWorld](https://arxiv.org/abs/2607.28415), [Enfold](https://arxiv.org/abs/2607.26657), [Mitigating Compounding Error](https://arxiv.org/abs/2607.27036), [Mental World Modeling](https://arxiv.org/abs/2607.27201), [Temporally Centered SIGReg Improves Multi-Task](https://arxiv.org/abs/2607.26924), [Temporal-Distance JEPA](https://arxiv.org/abs/2607.25337), [Reinformed Dreamer](https://arxiv.org/abs/2607.26040), [INTACT](https://arxiv.org/abs/2607.26056), [Concept-Guided Spatial Regularization](https://arxiv.org/abs/2607.15142), [Depth-Regularized JEPA World Models](https://arxiv.org/abs/2607.16314), [WAM4D](https://arxiv.org/abs/2606.14048), [ProPhy](https://arxiv.org/abs/2512.05564), [DiReCT](https://arxiv.org/abs/2603.25931), [V-JEPA 2](https://arxiv.org/abs/2506.09985), [DriveLaW](https://arxiv.org/abs/2512.23421), [Motus](https://arxiv.org/abs/2512.13030), [Video Prediction Policy](https://arxiv.org/abs/2412.14803)
<!-- /auto:cz -->

<a name="3.5."></a>
### 3.5. No Carrier, and the Generation as Its Own Trace

The two regimes that bracket the four carriers: nothing is externalised and competence is whatever pretraining left behind, or the generation *is* the reasoning trace and the external scaffold disappears. The trace can be a video, but it need not be — a sequence of generated images, or an interleaved sequence of images and text, carries the same role without continuous time.

<!-- auto:cn -->
*The two regimes that bracket the four carriers. Nothing is externalised, or the generation is itself the trace.*

**None** · 41 methods

- **S1** — [FreqForcing](https://arxiv.org/abs/2607.27110), [Visko Orbis 1.0](https://arxiv.org/abs/2607.26694), [TaoMate](https://arxiv.org/abs/2607.24359), [Orbis 2](https://arxiv.org/abs/2607.15898), [DriftWorld](https://arxiv.org/abs/2607.15065), [GigaWorld-Policy-0.5](https://arxiv.org/abs/2607.13960), [Ego-Dynamics-Augmented World Model](https://arxiv.org/abs/2607.13410), [Inferix](https://arxiv.org/abs/2511.20714), [DreamDojo](https://arxiv.org/abs/2602.06949), [ConsistI2V](https://arxiv.org/abs/2402.04324), [Diffusion over Diffusion](https://arxiv.org/abs/2303.12346), [Advancing Narrative Long Video](https://arxiv.org/abs/2605.18733), [Generative World Modelling for Humanoids](https://arxiv.org/abs/2510.07092), [Navigation World Models](https://arxiv.org/abs/2412.03572), [TeleWorld](https://arxiv.org/abs/2601.00051), [GigaWorld-0](https://arxiv.org/abs/2511.19861), [Adapting Video Diffusion Models](https://arxiv.org/abs/2410.12822), [GAIA-1](https://arxiv.org/abs/2309.17080), [GameNGen](https://arxiv.org/abs/2408.14837), [Genie](https://arxiv.org/abs/2402.15391), [UniSim](https://arxiv.org/abs/2310.06114), [DriveDreamer](https://arxiv.org/abs/2309.09777), [Drive-WM](https://arxiv.org/abs/2311.17918), [WorldDreamer](https://arxiv.org/abs/2402.17144), [Cosmos World Foundation Model](https://arxiv.org/abs/2501.03575), [Video Diffusion Models (2022)](https://arxiv.org/abs/2204.03458), [Imagen Video](https://arxiv.org/abs/2210.02303), [Make-A-Video](https://arxiv.org/abs/2209.14792), [Phenaki](https://arxiv.org/abs/2210.02399), [VideoPoet](https://arxiv.org/abs/2312.14125), [Lumiere](https://arxiv.org/abs/2401.12945), [Stable Video Diffusion](https://arxiv.org/abs/2311.15127), [Text2Video-Zero](https://arxiv.org/abs/2303.13439), [VideoComposer](https://arxiv.org/abs/2306.02018), [AnimateDiff](https://arxiv.org/abs/2307.04725), [DragNUWA](https://arxiv.org/abs/2308.08089), [MotionCtrl](https://arxiv.org/abs/2312.03641), [CameraCtrl](https://arxiv.org/abs/2404.02101), [FreeNoise](https://arxiv.org/abs/2310.15169), [FIFO-Diffusion](https://arxiv.org/abs/2405.11473), [StreamingT2V](https://arxiv.org/abs/2403.14773)

**The generation itself** · 26 methods

- **S4** — [PhyMAGIC](https://arxiv.org/abs/2505.16456), [Simulator-in-the-Loop](https://arxiv.org/abs/2603.06408), [Mind-Studio](https://arxiv.org/abs/2606.16070)
- **S5** — [OpenCoF](https://arxiv.org/abs/2607.08763), [PhysRVG](https://arxiv.org/abs/2601.11087), [Self-Refining Sampling](https://arxiv.org/abs/2601.18577), [NEWTON](https://arxiv.org/abs/2605.18396), [ViMax](https://arxiv.org/abs/2606.07649), [Closed-Loop Triplet Synergistic Generation](https://arxiv.org/abs/2606.16184), [Verifiable Rewards](https://arxiv.org/abs/2605.15458), [UniT](https://arxiv.org/abs/2602.12279), [PhyGDPO](https://arxiv.org/abs/2512.24551), [VJEPA-2 Reward](https://arxiv.org/abs/2510.21840), [Phys-AR / Timestep Tokens](https://arxiv.org/abs/2504.15932), [Video-T1](https://arxiv.org/abs/2503.18942), [Thinking in Frames](https://arxiv.org/abs/2601.21037), [Temporal Backtracking Search](https://arxiv.org/abs/2606.13861), [StoryBlender](https://arxiv.org/abs/2604.03315), [CoAgent](https://arxiv.org/abs/2512.22536), [AesopAgent](https://arxiv.org/abs/2403.07952), [Inference-Time Scaling for Joint](https://arxiv.org/abs/2606.03183), [CollabVR](https://arxiv.org/abs/2605.08735), [VIGOR](https://arxiv.org/abs/2603.16271), [PAVXploreRL](https://arxiv.org/abs/2607.16602), [Action Agent](https://arxiv.org/abs/2605.01477), [InfLVG](https://arxiv.org/abs/2505.17574)
<!-- /auto:cn -->

<a name="4."></a>
## 4. Benchmarks and Evaluation


Pixels are not a verifiable medium in the sense that a proof or a program is. A generated image or video does not announce its answer: something must extract it before correctness can be assessed, and that extractor is itself a fallible model, so every generative reasoning benchmark inherits the failure modes of its read-out mechanism.

What an instrument may legitimately score is also fixed by the cell its tasks fall in, not by convention. Row A admits comparison against the answer; row B admits only a membership test; row C has no endpoint to compare and has to score the path. Two thirds of the tasks in [Section 1](#1.) therefore cannot be scored against a single reference clip without measuring something other than correctness.

<a name="4.1."></a>
### 4.1. Benchmarks by Task Class

What a benchmark can legitimately do is fixed by the cell its tasks fall in: row A admits comparison against the answer, row B can only test membership in the admissible set, and row C has to score the path. A protocol that compares row-B or row-C output frame by frame against one recorded clip is measuring adherence to a sample rather than correctness ([§1.3](#1.3.)).

<!-- auto:inst -->
*48 benchmarks and datasets, grouped by what they check; the V rows are the labelling of [§1.7](#1.7.). Protocols and metrics are in [§4.2](#4.2.), audits of the judges in [§4.3](#4.3.), and analyses with no task set of their own in [§6.2](#6.2.).*

**Physical Law** · 16

- [What-If World: A Causal Benchmark for General World Models in Embodied Scenarios](https://arxiv.org/abs/2605.27589) · arXiv 2026 · `V1`
- [YoCausal: How Far is Video Generation from World Model? A Causality Perspective](https://arxiv.org/abs/2605.30346) · arXiv 2026 · `V1`
- [Towards World Simulator: Crafting Physical Commonsense-Based Benchmark for Video Generation](https://arxiv.org/abs/2410.05363) · arXiv 2024 · `V1`
- [VideoPhy: Evaluating Physical Commonsense for Video Generation](https://arxiv.org/abs/2406.03520) · arXiv 2024 · `V1`
- [PhyWorldBench: A Comprehensive Evaluation of Physical Realism in Text-to-Video Models](https://arxiv.org/abs/2507.13428) · arXiv 2025 · `V1`
- [VideoPhy-2: A Challenging Action-Centric Physical Commonsense Evaluation in Video Generation](https://arxiv.org/abs/2503.06800) · arXiv 2025 · `V1`
- [Do generative video models understand physical principles?](https://arxiv.org/abs/2501.09038) · arXiv 2025 · `V1`
- [PhyGround: Benchmarking Physical Reasoning in Generative World Models](https://arxiv.org/abs/2605.10806) · arXiv 2026 · `V1`
- [Morpheus: Benchmarking Physical Reasoning of Video Generative Models with Real Physical Experiments](https://arxiv.org/abs/2504.02918) · arXiv 2025 · `V1`
- [WorldBench: Disambiguating Physics for Diagnostic Evaluation of World Models](https://arxiv.org/abs/2601.21282) · arXiv 2026 · `V1`
- [Apple-PI: Benchmarking Thinking with Video Towards Law-Grounded Physical Intelligence](https://arxiv.org/abs/2607.16401) · arXiv 2026 · `V1`
- [Benchmarking Scientific Understanding and Reasoning for Video Generation using VideoScience-Bench](https://arxiv.org/abs/2512.02942) · arXiv 2025 · `V1`
- [T2VWorldBench: A Benchmark for Evaluating World Knowledge in Text-to-Video Generation](https://arxiv.org/abs/2507.18107) · arXiv 2025 · `V1`
- [PhysicsMind: Sim and Real Mechanics Benchmarking for Physical Reasoning and Prediction in Foundational VLMs and World Models](https://arxiv.org/abs/2601.16007) · arXiv 2026 · `V1`
- [World ModelBench: Judging Video Generation Models As World Models](https://arxiv.org/abs/2502.20694) · arXiv 2025 · `V1`
- [T2VPhysBench: A First-Principles Benchmark for Physical Consistency in Text-to-Video Generation](https://arxiv.org/abs/2505.00337) · arXiv 2025 · `V1`

**Structural Persistence** · 4

- [WorldScore: A Unified Evaluation Benchmark for World Generation](https://arxiv.org/abs/2504.00983) · arXiv 2025 · `V2`
- [GeoPhys: The Geometry of Physical Plausibility](https://arxiv.org/abs/2606.20707) · arXiv 2026 · `V2`
- [GeoT2V-Bench: Benchmarking 3D Consistency in Text-to-Video Models via 3D Reconstruction](https://arxiv.org/abs/2606.24829) · arXiv 2026 · `V2`
- [Out of Sight, Out of Mind? Evaluating State Evolution in Video World Models](https://arxiv.org/abs/2603.13215) · arXiv 2026 · `V2`

**Formal Rules** · 4

- [RULER-Bench: Probing Rule-based Reasoning Abilities of Next-level Video Generation Models for Vision Foundation Intelligence](https://arxiv.org/abs/2512.02622) · arXiv 2025 · `V3`
- [Reasoning via Video: The First Evaluation of Video Models'Reasoning Abilities through Maze-Solving Tasks](https://arxiv.org/abs/2511.15065) · arXiv 2025 · `V3`
- [Video Models Start to Solve Chess, Maze, Sudoku, Mental Rotation, and Raven' s Matrices](https://arxiv.org/abs/2512.05969) · arXiv 2025 · `V3`
- [Neuro-Symbolic Evaluation of Text-to-Video Models using Formal Verification](https://arxiv.org/abs/2411.16718) · arXiv 2024 · `V3`

**Goal Attainment** · 2

- [ReactSim-Bench: Benchmarking Reactive Behavior World Model Simulation in Autonomous Driving](https://arxiv.org/abs/2606.14058) · arXiv 2026 · `V4`
- [Omni-WorldBench: Towards a Comprehensive Interaction-Centric Benchmark for World Models](https://arxiv.org/abs/2603.22212) · arXiv 2026 · `V4`

**Procedure & Order** · 2

- [LoCoT2V-Bench: Benchmarking Long-Form and Complex Text-to-Video Generation](https://arxiv.org/abs/2510.26412) · arXiv 2025 · `V5`
- [SLVMEval: Synthetic Meta Evaluation Benchmark for Text-to-Long Video Generation](https://arxiv.org/abs/2603.29186) · arXiv 2026 · `V5`

**Convention & Intent** · 3

- [SVBench: Evaluation of Video Generation Models on Social Reasoning](https://arxiv.org/abs/2512.21507) · arXiv 2025 · `V6`
- [NarrLV: Towards a Comprehensive Narrative-Centric Evaluation for Long Video Generation Models](https://arxiv.org/abs/2507.11245) · arXiv 2025 · `V6`
- [MovieBench: A Hierarchical Movie Level Dataset for Long Video Generation](https://arxiv.org/abs/2411.15262) · arXiv 2024 · `V6`

**General-Purpose Suites** · 6

- [TiViBench: Benchmarking Think-in-Video Reasoning for Video Generative Models](https://arxiv.org/abs/2511.13704) · arXiv 2025 · `VX`
- [V-ReasonBench: Toward Unified Reasoning Benchmark Suite for Video Generation Models](https://arxiv.org/abs/2511.16668) · arXiv 2025 · `VX`
- [MME-CoF-Pro: Evaluating Reasoning Coherence in Video Generative Models with Text and Visual Hints](https://arxiv.org/abs/2603.20194) · arXiv 2026 · `VX`
- [WorldReasonBench: Human-Aligned Stress Testing of Video Generators as Future World-State Predictors](https://arxiv.org/abs/2605.10434) · arXiv 2026 · `VX`
- [Thinking in Video: Can Video Generators Really Reason About the Real World?](https://arxiv.org/abs/2607.17523) · arXiv 2026 · `VX`
- [Can World Simulators Reason? Gen-ViRe: A Generative Visual Reasoning Benchmark](https://arxiv.org/abs/2511.13853) · arXiv 2025 · `VX`

**Quality, Control & Safety** · 11

- [VBench-2.0: Advancing Video Generation Benchmark Suite for Intrinsic Faithfulness](https://arxiv.org/abs/2503.21755) · arXiv 2025 · `V0`
- [Can You Count to Nine? A Human Evaluation Benchmark for Counting Limits in Modern Text-to-Video Models](https://arxiv.org/abs/2504.04051) · arXiv 2025 · `V0`
- [T2VSafetyBench: Evaluating the Safety of Text-to-Video Generative Models](https://arxiv.org/abs/2407.05965) · arXiv 2024 · `V0`
- [VBench++: Comprehensive and Versatile Benchmark Suite for Video Generative Models](https://arxiv.org/abs/2411.13503) · arXiv 2024 · `V0`
- [VBench: Comprehensive Benchmark Suite for Video Generative Models](https://arxiv.org/abs/2311.17982) · arXiv 2023 · `V0`
- [EvalCrafter: Benchmarking and Evaluating Large Video Generation Models](https://arxiv.org/abs/2310.11440) · arXiv 2023 · `V0`
- [T2V-CompBench: A Comprehensive Benchmark for Compositional Text-to-Video Generation](https://arxiv.org/abs/2407.14505) · arXiv 2024 · `V0`
- [T2VTextBench: A Human Evaluation Benchmark for Textual Control in Video Generation Models](https://arxiv.org/abs/2505.04946) · arXiv 2025 · `V0`
- [VANE-Bench: Video Anomaly Evaluation Benchmark for Conversational LMMs](https://arxiv.org/abs/2406.10326) · arXiv 2024 · `V0`
- [Evaluation of Text-to-Video Generation Models: A Dynamics Perspective](https://arxiv.org/abs/2407.01094) · arXiv 2024 · `V0`
- [Human-Activity AGV Quality Assessment: A Benchmark Dataset and an Objective Evaluation Metric](https://arxiv.org/abs/2411.16619) · arXiv 2024 · `V0`
<!-- /auto:inst -->

<a name="4.2."></a>
### 4.2. Process-Level and Annotation-Free Protocols

Protocols that score the intermediate steps rather than only the final frame, and cycle-consistency read-outs that need no labels but score coherence rather than correctness.

<!-- auto:proto -->
*7 entries. What each one scores is the read-out, not the task set.*

- [Reference-Free Assessment of Physical Consistency in World Model-based Video Generation](https://arxiv.org/abs/2606.22363) · arXiv 2026 · `V1`
- [Event-Conditioned Diagnostics of Kinematic, Contact, and Object-Permanence Fields in Passive Object-State World Models](https://arxiv.org/abs/2606.28455) · arXiv 2026 · `V2`
- [Trimming the Long-Tail of Visual World Modeling Evaluation](https://arxiv.org/abs/2606.24256) · arXiv 2026 · `VX`
- [Certified World Models: Predictability Across Configuration, Horizon, and Resolution](https://arxiv.org/abs/2606.13092) · arXiv 2026 · `VX`
- [VIPER: Process-aware Evaluation for Generative Video Reasoning](https://arxiv.org/abs/2512.24952) · arXiv 2025 · `VX`
- [VideoScore2: A Generalized Video Generation Evaluation Metric](https://arxiv.org/abs/2509.22799) · arXiv 2025 · `V0`
- [Scalable Policy Evaluation with Video World Models](https://arxiv.org/abs/2511.11520) · arXiv 2025 · `V4`
<!-- /auto:proto -->

<a name="4.3."></a>
### 4.3. Auditing the Verifiers

The field has begun auditing its own judges, finding that the vision models used to certify physical plausibility collapse on precisely the geometrically demanding cases that distinguish plausible from correct. Gains reported against a weak verifier should be read as gains against that verifier.

<!-- auto:audit -->
*3 entries. Read a reported gain against the verifier that certified it.*

- [Physics-IQ Verified](https://arxiv.org/abs/2606.18943) · arXiv 2026 · `V1`
- [Geometric Collapse: When Vision Models Fail to Verify Physical Causality](https://arxiv.org/abs/2607.06871) · arXiv 2026 · `V1`
- [When a Verified World Model Still Loses: Play-Adequacy vs Prediction-Accuracy in LLM-Synthesized Code World Models](https://arxiv.org/abs/2607.14169) · arXiv 2026 · `V4`
<!-- /auto:audit -->

<a name="5."></a>
## 5. Key Messages

Two claims are usually made on this field's behalf, and usually with equal force: that video is irreplaceable, and that visual reasoning is where things are going. The task classification of [Section 1](#1.) lets us say how much of the corpus each one covers, and they are not the same size.

| Claim | What supports it | Share of the 129 in-scope tasks |
| --- | --- | --- |
| **A sequence cannot be replaced by a single state** | Tasks that ask for no endpoint, plus tasks whose process carries a stated condition | **44%** (57 tasks) |
| **Vision itself does the inferential work** | Tasks with no symbolic route: the whole world column plus the geometric half of the rule column | **88%** (113 tasks) |

Read the gap between the two rows rather than either row alone. The case for reasoning in a visual medium is much firmer than the case for continuous time, and a survey that asserts them together obscures the more useful of the two.

**Where a sequence is genuinely irreplaceable.** In three tiers, not one. *(i)* The 36 tasks that ask for no endpoint at all, where handing over a final state conveys nothing — a pendulum, a flame, a crowd, a gait, any fixed-horizon rollout. This tier needs no argument, because the alternative is unavailable rather than worse. *(ii)* The 21 tasks whose process carries a stated condition of its own — drive without colliding, assemble in the manual's order — where an endpoint is checkable but insufficient. *(iii)* The remaining 56%, where a single state is enough and the sequence is a delivery format. That third tier is the largest, and it is the one that must not be used to support the claim.

**What native visual reasoning is for.** The `spatial` tasks: the whole world-constrained column, where no symbolic route exists at any scale, plus the geometric half of the rule column — the tangram, the jigsaw, the auxiliary line, compass-and-straightedge construction. It is *not* for the 16 tasks that reduce without loss to discrete states and a finite rule set, where a solver or a language model reaches the answer more cheaply and the generated frames add a rendering step and a read-out problem without adding inference. Sudoku, the unique mate and the paper maze are in that group, and so — less comfortably — are script-to-storyboard and short-drama generation.

**How to refute either claim.** A method that *beat* symbolic solvers on the symbolic half of A2, rather than merely reaching non-trivial accuracy, would show that spatial simulation buys something on tasks that do not appear to need it. A method that beat a symbolic pipeline on storyboard ordering would do the same for the narrative case. Both experiments are cheap and neither has been run.

<a name="6."></a>
## 6. Study and Rethinking


<a name="6.1."></a>
### 6.1. Related Surveys

Six bodies of existing literature border this one: generation foundations, long video and storytelling, world models, multimodal reasoning, video understanding, and evaluation. The nearest prior work organises the space by reasoning *task*; we organise it by reasoning *mechanism*. A task-centred account tells you what has been attempted, while a mechanism-centred one tells you why a given approach hits a ceiling.

<!-- auto:surv -->
*60 related surveys, roadmaps and position papers — the context this review sits in. They carry no source or problem label: they are not objects the classification applies to.*

**Video Generation Foundations**

*Diffusion & T2V Foundations*

- [A Survey on Video Diffusion Models](https://arxiv.org/abs/2310.10647) · arXiv 2023
- [A Survey of AI Text-to-Image and AI Text-to-Video Generators](https://arxiv.org/abs/2311.06329) · arXiv 2023
- [Video Diffusion Models: A Survey](https://arxiv.org/abs/2405.03150) · arXiv 2024
- [From Sora What We Can See: A Survey of Text-to-Video Generation](https://arxiv.org/abs/2405.10674) · arXiv 2024
- [Survey of Video Diffusion Models: Foundations, Implementations, and Applications](https://arxiv.org/abs/2504.16081) · arXiv 2025
- [Evolution of Video Generative Foundations](https://arxiv.org/abs/2604.06339) · arXiv 2026

*LLM--Video Bridging*

- [A Survey on Generative AI and LLM for Video Generation, Understanding, and Streaming](https://arxiv.org/abs/2404.16038) · arXiv 2024
- [Bridging Text and Video Generation: A Survey](https://arxiv.org/abs/2510.04999) · arXiv 2025

*Control & Human-Centric Video*

- [A Comprehensive Survey on Human Video Generation: Challenges, Methods, and Insights](https://arxiv.org/abs/2407.08428) · arXiv 2024
- [Controllable Video Generation: A Survey](https://arxiv.org/abs/2507.16869) · arXiv 2025
- [Human Motion Video Generation: A Survey](https://arxiv.org/abs/2509.03883) · arXiv 2025

**Long-Horizon & Storytelling**

*Long Video Generation*

- [A Survey on Long Video Generation: Challenges, Methods, and Prospects](https://arxiv.org/abs/2403.16407) · arXiv 2024
- [Towards Chunk-Wise Generation for Long Videos](https://arxiv.org/abs/2411.18668) · arXiv 2024
- [Exploring the Latest Trends in Long Video Generation](https://arxiv.org/abs/2412.18688) · arXiv 2024
- [A Survey on Long-Video Storytelling Generation: Architectures, Consistency, and Cinematic Quality](https://arxiv.org/abs/2507.07202) · arXiv 2025

**World Models & Physical AI**

*Generation-to-World-Model Roadmaps*

- [Sora as an AGI World Model? A Complete Survey on Text-to-Video Generation](https://arxiv.org/abs/2403.05131) · arXiv 2024
- [Is Sora a World Simulator? A Comprehensive Survey on General World Models and Beyond](https://arxiv.org/abs/2405.03520) · arXiv 2024
- [Simulating the Real World: A Unified Survey of Multimodal Generative Models](https://arxiv.org/abs/2503.04641) · arXiv 2025
- [Simulating the Visual World with Artificial Intelligence: A Roadmap](https://arxiv.org/abs/2511.08585) · arXiv 2025
- [A Mechanistic View on Video Generation as World Models: State and Dynamics](https://arxiv.org/abs/2601.17067) · arXiv 2026
- [Video Generation Models as World Models: Efficient Paradigms, Architectures and Algorithms](https://arxiv.org/abs/2603.28489) · arXiv 2026
- [Visual Generation in the New Era: An Evolution from Atomic Mapping to Agentic World Modeling](https://arxiv.org/abs/2604.28185) · arXiv 2026
- [From Masks to Worlds: A Hitchhiker's Guide to World Models](https://arxiv.org/abs/2510.20668) · arXiv 2025
- [From Seeing to Knowing the World: A Survey of Vision World Models](https://www.preprints.org/manuscript/202604.2072) · arXiv 2026

*World-Model Critique & Agentic Modeling*

- [Critiques of World Models](https://arxiv.org/abs/2507.05169) · arXiv 2025
- [From Generative Engines to Actionable Simulators: The Imperative of Physical Grounding in World Models](https://arxiv.org/abs/2601.15533) · arXiv 2026
- [Agentic World Modeling: Foundations, Capabilities, Laws, and Beyond](https://arxiv.org/abs/2604.22748) · arXiv 2026
- [World Action Models: A Survey](https://arxiv.org/abs/2606.20781) · arXiv 2026
- [World Action Models: The Next Frontier in Embodied AI](https://arxiv.org/abs/2605.12090) · arXiv 2026

*Physical AI & Causal Generation*

- [Generative Physical AI in Vision: A Survey](https://arxiv.org/abs/2501.10928) · arXiv 2025
- [Aligning Perception, Reasoning, Modeling and Interaction: A Survey on Physical AI](https://arxiv.org/abs/2510.04978) · arXiv 2025

*Embodied & Autonomous Systems*

- [Exploring the Interplay Between Video Generation and World Models in Autonomous Driving: A Survey](https://arxiv.org/abs/2411.02914) · arXiv 2024
- [A Survey of World Models for Autonomous Driving](https://arxiv.org/abs/2501.11260) · arXiv 2025
- [The Role of World Models in Shaping Autonomous Driving: A Comprehensive Survey](https://arxiv.org/abs/2502.10498) · arXiv 2025
- [A Survey: Learning Embodied Intelligence from Physical Simulators and World Models](https://arxiv.org/abs/2507.00917) · arXiv 2025
- [A Comprehensive Survey on World Models for Embodied AI](https://arxiv.org/abs/2510.16732) · arXiv 2025
- [A Step Toward World Models: A Survey on Robotic Manipulation](https://arxiv.org/abs/2511.02097) · arXiv 2025
- [Video Generation Models in Robotics: Applications, Research Challenges, Future Directions](https://arxiv.org/abs/2601.07823) · arXiv 2026
- [World Model for Robot Learning: A Comprehensive Survey](https://arxiv.org/abs/2605.00080) · arXiv 2026

**Multimodal & Visual Reasoning**

*Multimodal CoT & Reasoning Models*

- [A Survey on Multimodal Large Language Models](https://arxiv.org/abs/2306.13549) · arXiv 2023
- [A Survey of Chain of Thought Reasoning: Advances, Frontiers and Future](https://arxiv.org/abs/2309.15402) · arXiv 2023
- [Multimodal Chain-of-Thought Reasoning: A Comprehensive Survey](https://arxiv.org/abs/2503.12605) · arXiv 2025
- [Mind with Eyes: from Language Reasoning to Multimodal Reasoning](https://arxiv.org/abs/2503.18071) · arXiv 2025
- [Perception, Reason, Think, and Plan: A Survey on Large Multimodal Reasoning Models](https://arxiv.org/abs/2505.04921) · arXiv 2025
- [Toward Native Multimodal Modeling: A Roadmap](https://arxiv.org/abs/2605.25343) · arXiv 2026

*Thinking with Images & Compositional Reasoning*

- [Thinking with Images for Multimodal Reasoning: Foundations, Methods, and Future Frontiers](https://arxiv.org/abs/2506.23918) · arXiv 2025
- [Reasoning in Computer Vision: Taxonomy, Models, Tasks, and Open Challenges](https://arxiv.org/abs/2508.10523) · arXiv 2025
- [Explain Before You Answer: A Survey on Compositional Visual Reasoning](https://arxiv.org/abs/2508.17298) · arXiv 2025
- [From Perception to Cognition: A Survey of Vision-Language Interactive Reasoning in Multimodal Large Language Models](https://arxiv.org/abs/2509.25373) · arXiv 2025

*Video Understanding & Grounding*

- [Video Understanding with Large Language Models: A Survey](https://arxiv.org/abs/2312.17432) · arXiv 2023
- [A Survey on Video Temporal Grounding with Multimodal Large Language Model](https://arxiv.org/abs/2508.10922) · arXiv 2025
- [Video-LMM Post-Training: A Deep Dive into Video Reasoning with Large Multimodal Models](https://arxiv.org/abs/2510.05034) · arXiv 2025
- [A Survey of Generative Video Models as Visual Reasoners](https://www.techrxiv.org/doi/10.36227/techrxiv.176857888.84304881) · arXiv 2026

*RL, Process Rewards & Test-Time Scaling*

- [Reinforced MLLM: A Survey on RL-Based Reasoning in Multimodal Large Language Models](https://arxiv.org/abs/2504.21277) · arXiv 2025
- [A Survey of Process Reward Models: From Outcome Signals to Process Supervisions for Large Language Models](https://arxiv.org/abs/2510.08049) · arXiv 2025
- [World Models: A Comprehensive Survey of Architectures, Methodologies, Reasoning Paradigms, and Applications](https://arxiv.org/abs/2606.00133) · arXiv 2026
- [Test-Time Scaling in Multimodal Foundation Models: A Comprehensive Survey of Generation and Reasoning](https://arxiv.org/abs/2606.08231) · arXiv 2026

**Evaluation & Reliability**

*Evaluation Surveys*

- [A Survey of AI-Generated Video Evaluation](https://arxiv.org/abs/2410.19884) · arXiv 2024
- [A Survey: Spatiotemporal Consistency in Video Generation](https://arxiv.org/abs/2502.17863) · arXiv 2025
- [The Safety Challenge of World Models for Embodied AI Agents: A Review](https://arxiv.org/abs/2510.05865) · arXiv 2025
<!-- /auto:surv -->

<a name="6.2."></a>
### 6.2. Position, Diagnosis and Analysis

Diagnostic work on whether visual realism and physical understanding are decoupled, whether object state survives occlusion, and whether predictive objectives install anything that deserves the name reasoning.

<!-- auto:diag -->
*9 entries. Studies and positions that fix no task set of their own.*

- [Demystifying Video Reasoning](https://arxiv.org/abs/2603.16870) · arXiv 2026 · `VX`
- [Hallucination in World Models is Predictable and Preventable](https://arxiv.org/abs/2606.27326) · arXiv 2026 · `V4`
- [What Can Latent World Models Know? Physical Parameter Identifiability in Multimodal Predictive Representations](https://arxiv.org/abs/2607.27017) · arXiv 2026 · `V1`
- [How Should World Models Be Evaluated for Embodied Decision-Making? A Decision-Making-Centric Position](https://arxiv.org/abs/2606.15032) · arXiv 2026 · `V4`
- [A Mechanistic View on Video Generation as World Models](https://arxiv.org/abs/2601.17067) · arXiv 2026 · `VX`
- [Video models are zero-shot learners and reasoners](https://arxiv.org/abs/2509.20328) · arXiv 2025 · `VX`
- [Multimodal Chain-of-Thought Reasoning: A Comprehensive Survey](https://arxiv.org/abs/2503.12605) · arXiv 2025 · `VX`
- [Are Video Models Ready as Zero-Shot Reasoners? An Empirical Study with the MME-CoF Benchmark](https://arxiv.org/abs/2510.26802) · arXiv 2025 · `VX`
- [How Far is Video Generation from World Model: A Physical Law Perspective](https://arxiv.org/abs/2411.02385) · arXiv 2024 · `V1`
<!-- /auto:diag -->

<a name="7."></a>
## 7. Other Useful Resources


*Coming soon.*
