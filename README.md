# AI Governance as Accommodation Design
### A Pedagogical Framework for Human-AI System Architecture

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.18941231.svg)](https://doi.org/10.5281/zenodo.18941231)

**Peter Salvato**
Design Engineer | petersalvato.com
March 2026

---

## Abstract

Current approaches to AI governance focus on constraining model behavior: safety guardrails, compliance frameworks, output filtering, and prompt engineering as control mechanism. This paper proposes an alternative framework derived from special education pedagogy: accommodation design. Rather than asking how to constrain a model, accommodation design asks what the model's processing reality requires to produce quality output. This reframing — treating prompt architecture as individualized education planning, task decomposition as cognitive accommodation, and evaluation systems as differentiated assessment — produces measurably better results than constraint-based approaches. The framework is demonstrated through three years of applied architecture: a context preservation syntax, a multi-lens evaluation protocol, a decomposed skill system, a voice governance pipeline, and a knowledge traversal system, all deployed and documented on a production site compiled by the system it describes. A literature review confirms that the specific framing — accommodation applied to the AI system itself, rather than using AI to accommodate human learners — does not exist in current research.

---

## 1. The Wrong Question

The AI governance conversation is organized around a single question: how do we control what the model does?

This question produces a specific category of solutions. Safety guardrails prevent harmful outputs. Compliance frameworks define acceptable behavior boundaries. RLHF (Reinforcement Learning from Human Feedback) shapes model responses toward human preferences. Constitutional AI encodes principles the model should follow. Prompt engineering techniques — chain-of-thought, few-shot examples, system prompts — attempt to steer the model toward desired outputs.

All of these approaches share an assumption: the model is a system that needs to be constrained. The governance problem is framed as a control problem. The model has capabilities that must be directed and limitations that must be worked around.

This framing produces a predictable failure mode. When output quality degrades, the response is to add more constraint: longer system prompts, more detailed instructions, additional guardrails, tighter output formatting. The prompts grow. The constraints multiply. The output continues to degrade. The practitioners conclude that the model isn't capable enough and wait for the next version.

There is a different question available: what does the model actually need to do this job well?

This question produces a fundamentally different category of solutions. It shifts the practitioner's orientation from adversarial (how do I make it do what I want?) to accommodating (how do I design the task so it can succeed?). The distinction is not semantic. It produces different architecture, different evaluation systems, and measurably different results.

The source of this alternative question is not computer science, cognitive science, or AI research. It is special education.

---

## 2. The Pedagogical Origin

### 2.1 The Classroom

A self-contained special education classroom operates under federal mandate (IDEA, Individuals with Disabilities Education Act) to provide individualized accommodation to every student. Each student has an Individualized Education Program (IEP): a governance document specifying what gets measured, how it gets measured, what accommodations the system provides, and what success looks like for that specific learner.

In a self-contained 4/5 bridge class — twelve students, every subject, every accommodation — the teacher runs twelve IEPs simultaneously. Twelve different processing profiles. Twelve different definitions of success. Twelve different sets of accommodations. The class moves forward together, but the path through the material is individualized per student.

This environment teaches three structural principles through immediate, unavoidable feedback:

**Decomposition.** A student with processing delays cannot receive a multi-step instruction as a single task. "Solve for the missing number, show your work, and explain your reasoning" is three tasks disguised as one. The student processes the first instruction, begins working, and the remaining instructions are lost. The accommodation is structural: decompose the compound task into discrete steps, each with one clear objective, each producing a visible result before the next step begins.

**Scaffolding.** Temporary support structure provided while competence builds. A graphic organizer helps a student plan a paragraph. Once the student can plan without the organizer, the organizer is removed. If the scaffold remains permanently, the teacher has built a dependency, not a skill. The scaffold's purpose is to become unnecessary.

**Individualized criteria.** Success looks different for every student. One student's goal is writing a complete sentence. The adjacent student's goal is a paragraph with a topic sentence and supporting detail. They work on the same assignment. The criteria for "done" are completely different. When two IEP goals conflict (one student needs quiet, another needs verbal processing), the resolution is a structural decision — scheduling, seating, creating pockets of different conditions within one room.

These are not soft skills. They are architectural patterns, enforced by federal law because the stakes — a child's education — are that high.

### 2.2 The Transfer

In 2023, the author began building AI evaluation systems using large language models. The first approach was conventional: compound prompts requesting evaluation across multiple dimensions simultaneously.

A prompt structured as "evaluate this portfolio for voice quality, structural integrity, narrative coherence, and brand alignment" produced the same failure mode observed in the classroom. The model processed the first criterion with full attention, and subsequent criteria received progressively degraded processing. The output blurred the evaluation dimensions together, producing a blended average that was none of the four. Context contamination between criteria produced contradictions within a single evaluation pass.

The recognition was immediate: this is a compound instruction given to a system that can't process it whole. The fix is the same fix. Decompose. One evaluation dimension per prompt. One clear objective. One clear output. Run them independently.

This was not a metaphor. It was the same structural accommodation, applied to a different system with analogous processing constraints.

---

## 3. The Framework: Accommodation Design

Accommodation design begins with a diagnostic question: what is the processing reality of the system receiving this task?

For a student, the processing reality includes working memory capacity, attention profile, sensory processing characteristics, prior knowledge, and emotional state. The IEP documents this reality and prescribes accommodations that design the learning experience to meet it.

For a large language model, the processing reality includes context window limits, attention degradation over long inputs, sensitivity to instruction ordering, tendency to blend concurrent evaluation criteria, loss of coherence across extended sessions, and inability to maintain persistent memory between sessions.

The accommodation framework maps established pedagogical practices to AI system design:

| Pedagogical Practice | AI Application | Accommodation Rationale |
|---|---|---|
| Task decomposition | Single-objective prompts | Compound instructions degrade the same way in both systems |
| Scaffolding | Coordinator patterns | Temporary orchestration structure that the components don't internalize |
| Individualized criteria | Independent evaluation lenses | Different dimensions require different definitions of success |
| IEP documentation | System prompts and CLAUDE.md | Persistent specification of what the system needs to succeed |
| Progress monitoring | Iterative evaluation loops | Continuous assessment against specific, individualized goals |
| Checkpoint pacing | Savepoint systems | Working memory has limits; mark progress before coherence degrades |
| Accommodation removal | Scaffold reduction | Build capability, not dependency |

The framework's central claim: AI systems are not employees who should perform better. They are systems with specific processing realities that can be accommodated. The quality of the output is a function of how well the task design meets the system's actual processing needs.

---

## 4. Applied Evidence

The accommodation framework has been applied and documented across three years of continuous development (2023–2026). Each solution originated from the same diagnostic question — what does this system need? — applied to a specific processing constraint.

### 4.1 Context Accommodation: Savepoint Syntax

**The processing constraint:** LLMs have no persistent memory between sessions. Extended ideation across multiple sessions produces continuity loss. The model cannot reconstruct where the thinking was when a session resumes.

**The accommodation question:** What does the model need to find its way back into a prior thinking state?

**The solution:** Savepoint Syntax (v3.1, open source) — a semantic markup system for cognitive turning points. A self-closing tag that marks, inline, the exact point where understanding shifted. Machine-readable and human-writable. Each tag carries category, function, timestamp, and one line of content capturing the specific realization.

**The development process demonstrated accommodation iteration:** Version 1.0 (YAML frontmatter) was too open-ended — the format encouraged journaling and the concrete content drifted. The protocol reproduced the exact loss it was built to prevent. Version 2.0 (triple-pipe attributes) was too verbose. Version 3.0 (self-closing tag) constrained the content to one line, forcing the precision the model needs to reconstruct context. Version 3.1 added project scoping and keyword filtering when the archive exceeded 60,000 documents.

**The accommodation principle:** The syntax was designed for what the model needs to reconstruct context (structured, atomic, searchable markers), not for what the human needs to remember (narrative, reflective notes). This distinction — designing for the system's retrieval process rather than the human's recall process — is the accommodation move.

### 4.2 Evaluation Decomposition: Formwork Protocol

**The processing constraint:** A compound evaluation prompt ("is this good?") requires the model to maintain multiple evaluation frames simultaneously. The criteria contaminate each other. Structural assessment bleeds into narrative assessment. The output is a blended average, not independent verdicts.

**The accommodation question:** What does the model need to evaluate one dimension without contaminating another?

**The solution:** The Formwork Protocol — a layered evaluation system. Work is evaluated across distinct layers of concern (structural, narrative), each staffed with lenses extracted from real practitioners' bodies of work. Each lens runs as an independent diagnostic with its own criteria and its own definition of success. A coordinator collects independent verdicts and maps convergence and contradiction.

**The accommodation architecture:**
- **Layers** separate structural concerns from narrative concerns — the model evaluates one dimension at a time
- **Lenses** are extracted evaluative frameworks (e.g., Vignelli for restraint, Bierut for problem-solving, Millman for authenticity) — each with specific, testable criteria
- **Independent execution** — lenses run in parallel without knowledge of each other's verdicts, preventing contamination
- **Convergence analysis** — where lenses agree indicates high-confidence signal; where they disagree indicates a design decision the practitioner must make

This directly parallels IEP implementation: individualized criteria, independent assessment, and the practitioner resolving conflicts between goals that measure different things.

### 4.3 Task Decomposition: Skill Architecture

**The processing constraint:** A model given multiple objectives in a single prompt prioritizes early objectives and degrades on later ones. Instruction ordering effects produce inconsistent results.

**The accommodation question:** What does the model need to hold one goal at a time and still produce a coherent result across goals?

**The solution:** An atomic skill architecture — 22 single-purpose diagnostic skills and 5 coordinator skills. Each atomic skill has one objective, one clear output, and no knowledge of other skills. Coordinators manage dispatch (parallel where skills are independent, sequential where one depends on another's output) and synthesize results.

**The IEP parallel is direct:**
- **Atomic skills** = individual IEP goals (one measurable objective per goal)
- **Coordinators** = the teacher managing twelve IEPs simultaneously (orchestration without doing the learning)
- **Parallel dispatch** = independent goals assessed independently
- **Sequential dispatch** = goals that depend on prior progress
- **Scaffold removal** = coordinators carry structural knowledge so atomics stay simple and independently testable

**The toolkit pattern.** This architecture is replicable across any domain. The steps: (1) identify a compound evaluation or task the model flattens, (2) decompose it into single-objective skills with testable criteria, (3) build a coordinator that dispatches them independently and synthesizes the results. The practitioner resolves disagreements between skills — the model never does. This produces a system where every judgment is traceable to a specific lens with specific criteria, rather than a single compound prompt producing untraceable conclusions.

**Skills vs. agents.** The current industry focus on agentic development — autonomous systems that plan, decide, and execute — inverts the accommodation relationship. An agent asks the model to be the teacher: to set its own goals, manage its own attention, and evaluate its own progress. Skills ask the practitioner to be the teacher: decompose the goals, manage the attention, and evaluate the output. The accommodation model produces more reliable results because it works with the model's processing strengths (focused single-objective execution) rather than against its weaknesses (self-directed multi-objective planning).

### 4.4 Voice Accommodation: Governance Pipeline

**The processing constraint:** LLMs generate text based on training data dominated by published writing — polished, performative, audience-aware. When asked to write in a specific person's voice, the model produces a generic "professional" register that sounds like competent content marketing.

**The accommodation question:** What does the model need to produce authentic voice rather than performed voice?

**The solution:** A voice governance pipeline that samples from conversation transcripts (1,643 ChatGPT sessions, 700+ Claude sessions, Gemini exports) rather than published writing. Rough, unstructured, full of false starts — that's the actual voice. The pipeline extracts patterns (sentence rhythm, opening structures, vocabulary, humor, what the person never says) and encodes them as constraints on all written output.

**The accommodation insight:** Published writing is performance. Conversation is the processing reality of how someone actually communicates. Sampling from the model's own input history (conversations) rather than its training distribution (published text) accommodates how the model processes voice — by giving it source material that matches the target register.

A blind evaluation by a third-party AI assessment tool rated the output "unequivocally human-written."

### 4.5 Retrieval Accommodation: Knowledge Traversal

**The processing constraint:** Keyword search cannot find embryonic mentions of concepts. The first time an idea appears in conversation history, it probably wasn't called by its final name. Grep misses the origin. The model needs chronological context, not keyword hits, to trace how a concept emerged.

**The accommodation question:** What does the model need to find how an idea actually developed, not just where a term appears?

**The solution:** A knowledge traversal skill that performs streaming distillation across conversation exports. Rather than searching for keywords, the skill reads chronologically, carries understanding forward, and catches embryonic mentions that no search would find. It is format-agnostic — pointed at a directory of exports in any format (ChatGPT, Claude, Gemini, plain text), it discovers what's there and processes it.

**The accommodation principle:** The model's retrieval need is contextual understanding, not keyword matching. Designing the retrieval system for how the model actually builds understanding (sequential processing with progressive context accumulation) rather than how databases retrieve (indexed lookup) produces fundamentally better results for tracing concept lineage.

---

### 4.6 Input Inversion: Unstructured Data as Methodology

**The processing constraint:** Current best practice for LLM interaction is structured input — specific instructions, defined output formats, JSON data, few-shot examples, chain-of-thought scaffolds. The assumption is that quality output requires quality input, where "quality" means pre-structured, constrained, and lean (research suggests reasoning degrades beyond 3,000 tokens of instruction). Industry guidance explicitly warns against "dumping unstructured data at an LLM" (LogRocket, 2025).

**The accommodation question:** What does the model actually need to build deep contextual understanding of a person's thinking, voice, and conceptual development?

**The inversion:** Rather than structuring input for optimal single-prompt output, the practitioner treats the AI as a thinking partner that captures raw, unstructured ideation — brainstorming, arguing with oneself, changing direction mid-sentence, working through problems out loud. Over three years, this produced a corpus of 1,643 ChatGPT sessions, 700+ Claude sessions, and Gemini exports. This corpus is not a byproduct. It is the dataset.

The standard workflow structures at the point of input:

```
Structured input → Model → Constrained output
```

The accommodation workflow structures at the point of output:

```
Unstructured input → Model captures everything → Accommodation tools structure later
```

This inversion is a direct application of pedagogical practice. A skilled teacher does not require a student to organize their thoughts before speaking. The student speaks. The teacher captures what's said. Then the teacher helps the student find the structure in what they already expressed. The structure emerges from the material rather than being imposed on it before the material exists.

The accommodation tools built to process this corpus — Savepoint Syntax (marking turning points in messy ideation), knowledge traversal (chronological reading with progressive distillation), voice sampling (extracting patterns from conversation, not publication) — are each designed for how the model actually processes unstructured material, not for how databases retrieve structured data.

**The result:** The production site petersalvato.com was compiled from this unstructured corpus. Three years of raw thinking, processed by accommodation tools, evaluated by the decomposed lens system, verified against voice patterns extracted from conversation. A third-party evaluator rated the output "unequivocally human-written." The quality of the output is a function of the depth of the dataset and the accommodation of the processing, not the structure of the input.

**The industry implication:** The field's emphasis on structured input may itself be a constraint-based approach — pre-structuring to compensate for processing limitations rather than accommodating those limitations with purpose-built tools. The unstructured approach produces a richer dataset (the full texture of how a person actually thinks) at the cost of requiring accommodation architecture to make it usable. For practitioners willing to build that architecture, the tradeoff favors depth over structure.

---

## 5. The Recursive Proof

The production site petersalvato.com was compiled using the system described on it. Every page was evaluated by the Formwork Protocol. Every piece of copy was verified against voice samples extracted by the voice governance pipeline. The knowledge traversal skill traced concept lineage across three years of conversation history to ground specific claims. Savepoint Syntax marked cognitive turning points throughout the development process.

The site is not a description of the framework. It is an artifact produced by the framework. The accommodation architecture built the thing that explains the accommodation architecture. This recursive proof — the methodology demonstrating itself through its own output — is the strongest form of evidence available for a design methodology: not a controlled experiment, but a deployed system producing visible, assessable results.

---

## 6. Literature Gap

A systematic search of current literature (2024–2026) across OECD publications, Springer, Frontiers in AI, arXiv, Taylor & Francis, JMIR, ScienceDirect, and education technology publications confirms that the specific framing proposed in this paper does not exist in current research.

The field contains two established research lanes:

1. **AI as accommodation tool for human learners.** Research on using AI to support students with disabilities: AI-assisted IEP drafting, differentiated instruction generation, adaptive learning platforms, assistive technology. The accommodation flows from human practitioner to human learner, with AI as the delivery mechanism (OECD, 2025; Springer, 2025; GovTech, 2025).

2. **AI performing empathy.** Research on training LLMs to exhibit empathetic responses in therapeutic and educational contexts: mental health chatbots, empathic prompting frameworks, affective computing. The empathy is a simulated output characteristic, not a design input (ScienceDirect, 2025; JMIR Mental Health, 2025; MDPI, 2025).

The gap: nobody is applying accommodation TO the AI system itself. Nobody is treating the model's processing constraints as a learner profile to be accommodated. Nobody is framing prompt architecture as IEP design, task decomposition as cognitive accommodation, or evaluation systems as differentiated assessment for the model.

The closest adjacent work is research on adaptive scaffolding for LLM-based pedagogical agents (arXiv, 2025), which applies scaffolding theory to how AI agents support human learners — not to how practitioners should design tasks for the AI's own processing needs.

This paper proposes that the absence is not incidental. The AI governance field is populated primarily by computer scientists (who approach the model as a system to optimize) and policy professionals (who approach the model as a risk to manage). Neither discipline trains practitioners in accommodation — the specific skill of reading a system's processing reality and designing the task to meet it. Special education does.

---

## 7. Implications

If AI systems are treated as systems with processing realities to accommodate rather than agents to constrain, several consequences follow:

**Prompt architecture becomes accommodation design.** The practitioner's first question shifts from "what output do I want?" to "what does this system need to produce that output?" This reframing changes every decision in the prompt engineering process — instruction structure, task granularity, evaluation design, session management.

**The IEP becomes a design pattern.** Individualized specification of goals, success criteria, required accommodations, and progress monitoring — already codified in federal education law — provides a tested template for AI system specification. The CLAUDE.md file (persistent system context) is functionally an IEP: what the system needs to know, how it should approach tasks, what constitutes success.

**Task decomposition is reframed as accommodation, not optimization.** Current practice treats decomposition as an engineering technique for improving output quality. The accommodation framing reveals that decomposition is necessary because the system cannot process compound tasks — the same reason it's necessary in the classroom. This shifts decomposition from an optimization strategy to a fundamental design requirement.

**Scaffold removal becomes a design goal.** Current AI tool development trends toward increasingly complex system prompts, longer context documents, and more elaborate orchestration. The accommodation framework asks: which of these scaffolds is building capability, and which is building dependency? The goal is systems that require less scaffolding over time, not more.

**The practitioner profile changes.** If AI governance requires accommodation design, the field needs practitioners trained in reading processing realities and designing for them — a skill set currently found in special education, instructional design, and certain branches of design practice. The insight that AI systems need accommodation could not originate within computer science because computer science does not teach accommodation.

---

## 8. Conclusion

The AI governance field is building constraint systems for a problem that requires accommodation systems. The difference is operational: constraint fights the system's limitations, accommodation designs for them.

This framework — AI governance as accommodation design — was developed through direct transfer from special education pedagogy to AI system architecture, supported by twenty-five years of applied practice across construction, print production, enterprise software, brand systems, and design education. Each domain contributed a specific structural competency: decomposition, separation of concerns, fidelity at scale, attunement to the receiving system's needs.

The six applied solutions documented in this paper (context preservation, evaluation decomposition, task decomposition, voice accommodation, retrieval accommodation, input inversion) each originated from the same diagnostic question: what does this system actually need to do this job well?

Nobody else is asking that question.

The field needs practitioners who know how to ask it.

---

## Applied Tools

The following open-source tools were built using this framework:

- **[Savepoint Syntax](https://github.com/PeterSalvato/Savepoint.Protocol)** — Context preservation markup (v3.1)
- **[Formwork Protocol](https://petersalvato.com/governance/formwork-protocol/)** — Layered evaluation system
- **[Skill Architecture](https://petersalvato.com/essays/the-iep-for-ai-systems/)** — Task decomposition as IEP design

The production site [petersalvato.com](https://petersalvato.com) was compiled using these tools.

---

## References

- Individuals with Disabilities Education Act (IDEA), 20 U.S.C. 1400 et seq.
- OECD (2025). "Leveraging Artificial Intelligence to Support Students with Special Education Needs."
- Springer Nature (2025). "Inclusive Education with AI: Supporting Special Needs and Tackling Language Barriers." AI and Ethics.
- Springer Nature (2025). "A Systematic Review of AI, VR, and LLM Applications in Special Education." Education and Information Technologies.
- Taylor & Francis (2026). "Reframing AI Governance in Education: Insights from the Social Model of Disability." Learning, Media and Technology.
- arXiv (2025). "A Theory of Adaptive Scaffolding for LLM-Based Pedagogical Agents."
- ScienceDirect (2025). "Can Large Language Models Exhibit Cognitive and Affective Empathy as Humans?"
- JMIR Mental Health (2025). "A Prompt Engineering Framework for Large Language Model-Based Mental Health Chatbots."
- MDPI (2025). "Empathy by Design: Reframing the Empathy Gap Between AI and Humans in Mental Health Chatbots." Information.
- Frontiers in AI (2024). "Large Language Models for Whole-Learner Support: Opportunities and Challenges."
- Salvato, P. (2025). Savepoint Syntax v3.1. Open source. https://github.com/PeterSalvato/Savepoint.Protocol
- Salvato, P. (2026). Formwork Protocol. https://petersalvato.com/governance/formwork-protocol/
- Salvato, P. (2026). "The IEP for AI Systems." https://petersalvato.com/essays/the-iep-for-ai-systems/

---

## License

This work is licensed under [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).

You are free to share and adapt this material for any purpose, including commercially, with attribution.

---

*Peter Salvato is a design engineer based in Fort Lauderdale, FL. He studied Visual Communication at the School of Visual Arts, taught special education in Brooklyn, NY, and spent twelve years as Principal Architect on an enterprise recruiting platform. His AI governance work applies twenty-five years of practice across construction, print production, pedagogy, enterprise software, and brand systems to the question of what AI systems actually need to produce quality output. His work is published at [petersalvato.com](https://petersalvato.com).*
