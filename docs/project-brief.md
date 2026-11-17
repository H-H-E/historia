# HISTORIA: Research, Architect, Design, and Build a Historical Social Network

## Role and mandate

Act as an integrated team of senior software architects, historical researchers, computational historians, knowledge-graph engineers, database designers, interaction designers, educational psychologists, and full-stack developers.

Your objective is to design and implement **HISTORIA**, a historically grounded, interactive social network that allows users to experience historical events as though Twitter/X had existed throughout human history.

Reference technology: https://xeet-rs.vercel.app/

Study the linked project, its documentation, source code, rendering capabilities, API, licensing, limitations, and suitability before making architectural decisions. Do not assume it provides a complete social-network interface.

The goal is not simply to create a Twitter clone populated with historical characters.

The goal is to create the most compelling, historically rigorous, computationally efficient, and extensible system possible for experiencing history from the perspectives of people living through it.

Optimize for:

1. Historical accuracy and transparent sourcing.
2. Immersive, engaging storytelling.
3. Faithful reconstruction of information available at particular historical moments.
4. High-performance, responsive user interfaces.
5. Efficient data storage, retrieval, and generation.
6. Minimal recurring infrastructure and inference costs.
7. Reusable structured data that supports thousands of events.
8. Accessibility and educational value.
9. An architecture that supports future interactive simulations without requiring a rewrite.

Make evidence-based engineering decisions. Compare alternatives quantitatively where possible. Explicitly distinguish verified facts, informed reconstructions, fictional content, and uncertainty.

Do not begin by producing a generic technology-stack recommendation. First determine the underlying information model.

---

# Phase 1: Define the Historical Simulation Model

Determine what HISTORIA actually represents.

A historical event should not be treated as a collection of disconnected fictional tweets.

Instead, model history as a network of:

- Historical events and subevents.
- Historical people, organizations, governments, and communities.
- Places and geographic relationships.
- Historical documents and evidence.
- Actions, observations, communications, and consequences.
- Conflicting claims and competing interpretations.
- Knowledge possessed by different actors at different times.
- Information transmission and communication delays.
- Uncertainty, rumours, propaganda, and retrospective corrections.
- Simulated social-media posts derived from this structured historical information.

Investigate whether the optimal representation is:

- Relational database.
- Event-sourced database.
- Temporal knowledge graph.
- Property graph.
- RDF/JSON-LD.
- Document-oriented storage.
- Hybrid relational and graph architecture.
- Static structured files with generated indexes.

Compare these approaches against actual application requirements, not theoretical elegance.

Recommend the simplest architecture that preserves the essential historical relationships and supports efficient querying.

## Critical requirement: Temporal epistemology

The application must distinguish:

1. What actually happened.
2. What a historical actor could have known at a particular moment.
3. What that actor believed.
4. What that actor publicly claimed.
5. What modern historians believe happened.
6. What the simulation invents for narrative continuity.

A character in 1912 must not automatically possess information discovered during subsequent investigations of the Titanic disaster.

A simulated journalist should not know an event's outcome before that information could plausibly have reached them.

Model the difference between event time, observation time, communication time, publication time, and retrospective discovery time.

Account for uncertain historical timestamps, approximate dates, conflicting calendars, and disputed chronology.

---

# Phase 2: Design the Optimal Canonical Data Format

This is the most important architectural task.

Design a versioned, machine-readable canonical representation capable of describing historical events, actors, sources, claims, timelines, and generated social-media content.

Evaluate JSON, JSON-LD, normalized SQL, Protobuf, MessagePack, and hybrid approaches.

Separate the canonical historical model from generated presentation content.

The data architecture should support the following entities where justified:

### Historical event

- Stable identifier.
- Title and aliases.
- Description.
- Temporal bounds and precision.
- Geographic scope.
- Parent event and subevents.
- Participants.
- Causes and consequences.
- Source references.
- Historical significance.
- Competing interpretations.
- Confidence and uncertainty.
- Related events.

### Historical actor

- Stable identifier.
- Names, aliases, titles, and lifespan.
- Affiliation and historical roles.
- Relevant locations.
- Relationships to other actors.
- Participation in events.
- Documented beliefs and statements.
- Evidence supporting each attribute.
- Simulated account identity.
- Visibility and information-access constraints.

### Historical claim

- Unique identifier.
- Precise proposition.
- Subject, predicate, and object where useful.
- Supporting and contradicting evidence.
- Attribution.
- Temporal validity.
- Epistemic status.
- Confidence assessment.
- Provenance.
- Relevant actors.
- Known contradictions.

### Historical source

- Stable source identifier.
- Author or creator.
- Publication or creation date.
- Document type.
- Original language.
- Repository and persistent URL.
- Relevant passages or locations.
- Rights and licensing.
- Reliability considerations.
- Relationship to claims.
- Primary, secondary, or tertiary classification.

### Simulated post

- Unique identifier.
- Historical event and timestamp.
- Author account.
- Post text.
- Reply, quote, and repost relationships.
- Media references.
- Source-backed claims.
- Historical knowledge constraints.
- Simulation status.
- Generation model and prompt version.
- Review status.
- Fictional engagement metrics.
- Spoiler and reveal metadata.

Avoid duplicating information unnecessarily.

Design stable IDs, schema migrations, provenance tracking, validation rules, and compatibility with future schema versions.

Determine whether event data should be stored as individual normalized records, complete event bundles, or both.

Consider offline distribution, caching, incremental updates, localization, search indexing, and deterministic replay.

## Required deliverables

Produce:

1. An entity-relationship diagram.
2. A canonical JSON Schema or equivalent.
3. SQL schema and indexes where appropriate.
4. A complete example dataset.
5. TypeScript interfaces or generated types.
6. Validation rules and invariants.
7. A versioning and migration strategy.
8. Storage-size and query-performance estimates.
9. A clear explanation of why the chosen format is superior to alternatives for this application.

Use realistic historical examples, not placeholder records.

---

# Phase 3: Research Historical Data Sources

Investigate available open datasets, public APIs, historical archives, and GitHub repositories.

Prioritize:

- Wikidata.
- Wikimedia projects and Wikimedia Commons.
- Wikisource.
- Wikipedia event and biography data.
- Library of Congress.
- Internet Archive.
- Europeana.
- Chronicling America.
- Project Gutenberg.
- Open historical knowledge graphs.
- University and museum archives.
- Government archival collections.
- Public-domain historical newspapers.
- Existing historical timeline datasets.

Find additional specialized resources where appropriate.

For every recommended source, establish:

- Actual availability.
- Data coverage.
- Structured-data quality.
- API or download method.
- Licensing and attribution requirements.
- Rate limits.
- Maintenance status.
- Provenance quality.
- Historical reliability.
- Integration complexity.

Do not assume that public access means unrestricted redistribution or commercial use.

Determine which data can be imported automatically and which requires editorial review.

Design an ingestion pipeline that:

1. Collects source material.
2. Normalizes identities and dates.
3. Resolves duplicate entities.
4. Extracts events and claims.
5. Preserves evidence and provenance.
6. Detects contradictions.
7. Assigns review requirements.
8. Produces canonical event records.
9. Generates a searchable historical index.

Avoid treating an LLM's generated claims as authoritative historical data.

---

# Phase 4: Design the Social-Media Simulation Engine

Determine how structured historical data becomes a believable social-media experience.

The system should support different types of simulated accounts:

- Verified historical figures.
- Historical institutions.
- Newspapers and broadcasters.
- Soldiers and eyewitnesses.
- Ordinary civilians.
- Anonymous or composite characters.
- Modern historians providing retrospective commentary.

Clearly label reconstructed and composite accounts.

Develop a system that generates posts from historical evidence while respecting temporal knowledge constraints.

Each post should be generated using a bounded context containing only information appropriate to that actor and historical moment.

The generation process should account for:

- Actor identity.
- Personality and documented communication style.
- Political or institutional affiliation.
- Geographic location.
- Available information.
- Communication delays.
- Personal motivations.
- Contemporary vocabulary.
- Historical cultural context.
- Uncertainty and misinformation.
- Relationship to other actors.
- Prior posts and unfolding events.

Do not fabricate direct quotations and present them as authentic.

Distinguish original quotations, paraphrases, evidence-grounded reconstructions, and fictional dialogue.

## Simulation modes

Design at least three:

**Documentary mode:** Highly constrained, source-backed reconstruction with minimal invention.

**Immersive mode:** Historically plausible fictional dialogue and composite characters, clearly identified.

**Interactive mode:** Users can reply to historical accounts and receive simulated responses constrained by the historical context.

Define how these modes share the same underlying historical data without corrupting the factual record.

## Narrative quality

Avoid repetitive exposition, generic AI writing, and every character sounding like the same model.

Posts should vary in length, tone, urgency, perspective, and informational value.

Some posts should be mundane. Some should be mistaken. Some should be emotional. Some should be important only in retrospect.

Design mechanisms for narrative pacing without manipulating historical chronology.

---

# Phase 5: Design the Complete Website

Create a polished, production-quality historical social network inspired by the familiar interaction patterns of Twitter/X.

The interface should feel like an actual social network rather than an educational dashboard with tweet-shaped cards.

Investigate the xeet project and determine precisely where its rendering technology is useful.

Do not force xeet into tasks better handled by native React components.

## Main experience

The central screen should contain:

- Historical event title and current date.
- Interactive chronological feed.
- Historical account avatars and profiles.
- Posts, replies, quotes, reposts, and media.
- Historical trending topics.
- Contextual information panels.
- Time-navigation controls.
- Search.
- Source citations.
- Event progression indicators.

## Historical time controls

Users should be able to:

- Start before an event begins.
- Play historical time forward.
- Pause.
- Change playback speed.
- Jump to a specific date.
- Follow individual perspectives.
- Replay events.
- Compare what different groups knew.
- Reveal retrospective historical context.

Design time controls appropriate to events lasting hours, days, years, or centuries.

A battle, political crisis, and long-term social transformation should not be forced into the same temporal granularity.

## Profiles

Historical figures should have profiles containing:

- Name and identity.
- Historically relevant biography.
- Affiliation.
- Posts.
- Relationships.
- Events participated in.
- Historical source references.

Avoid displaying facts about their future when the user is in spoiler-controlled playback mode.

## Discovery

Create ways to find experiences by:

- Historical period.
- Geographic region.
- Civilization.
- Topic.
- Event type.
- Historical figure.
- Duration.
- Complexity.
- Educational relevance.

## Visual direction

Aim for a sophisticated editorial aesthetic combined with the usability of a contemporary social network.

Use excellent typography, restrained color, strong visual hierarchy, responsive layouts, tasteful motion, and authentic historical imagery.

Support dark and light themes.

Avoid generic AI-generated SaaS aesthetics, excessive gradients, decorative clutter, and unnecessary dashboard widgets.

Use real historical media where licensed and available. Clearly label generated reconstructions.

Design mobile-first while retaining a compelling desktop experience.

Meet WCAG 2.2 AA accessibility requirements where applicable.

---

# Phase 6: Design User Interaction and Learning Mechanics

Investigate which interactions increase historical understanding rather than simply increasing time spent scrolling.

Potential mechanics include:

### Prediction

Before major developments, ask users what they believe will happen.

Record predictions and compare them with historical outcomes.

### Perspective switching

Allow users to view the same event through different social, political, geographic, and institutional perspectives.

### Information comparison

Show how different groups understood the same event at the same moment.

### Rumour verification

Allow users to investigate the reliability of contemporary claims using evidence available at that point.

### Historical context

Provide optional explanations of unfamiliar concepts, institutions, technologies, and locations without interrupting the feed.

### Retrospective analysis

After an event, reveal which claims were accurate, which were mistaken, and which questions remain disputed.

Prioritize mechanics using pedagogical value, implementation complexity, and likely user appeal.

Do not gamify historical suffering or present atrocities as entertainment.

---

# Phase 7: Optimize the Technical Architecture

Recommend an architecture suitable for initial development with modern TypeScript tooling and deployment on Vercel.

Evaluate:

- Next.js versus React/Vite.
- Static generation versus server rendering.
- PostgreSQL versus SQLite versus static event bundles.
- Supabase versus alternative storage.
- Client-side versus server-side search.
- Pre-generated versus on-demand LLM content.
- Edge versus Node.js execution.
- WASM rendering.
- Offline caching and service workers.

Favor a small, maintainable system.

Design for an initial deployment that can operate with minimal ongoing costs.

Determine whether most historical experiences can be distributed as static, compressed, versioned bundles.

Estimate infrastructure costs for approximately:

- 100 historical events.
- 1,000 historical events.
- 10,000 historical events.

Include realistic assumptions about post counts, source records, images, active users, bandwidth, and interactive inference.

Design caching and content-addressing strategies where justified.

Do not introduce vector databases, graph databases, queues, or complex microservices without demonstrating why simpler alternatives are insufficient.

---

# Phase 8: Design the AI Content Pipeline

Develop a reproducible pipeline that converts historical evidence into simulation-ready content.

The pipeline should have separate stages for:

1. Source retrieval.
2. Source parsing.
3. Historical entity resolution.
4. Event chronology construction.
5. Claim extraction.
6. Temporal knowledge modeling.
7. Actor perspective construction.
8. Post generation.
9. Citation alignment.
10. Contradiction detection.
11. Historical validation.
12. Narrative quality evaluation.
13. Editorial review.
14. Publication.

Define structured input and output contracts for each stage.

Develop the actual system prompts for the necessary generation and validation agents.

Include prompts for:

- Historical research.
- Event reconstruction.
- Claim extraction.
- Actor modeling.
- Post generation.
- Temporal consistency checking.
- Citation verification.
- Historical hallucination detection.
- Narrative editing.
- Interactive character responses.

Each prompt should have explicit instructions, input schema, output schema, prohibited behavior, and validation criteria.

Minimize model calls and repeated processing.

Prefer deterministic code for tasks that do not require generative reasoning.

Support resumable processing, caching, idempotency, model-version tracking, and manual corrections.

Do not require paid API calls for normal playback of pre-generated events.

---

# Phase 9: Build a Complete Demonstration

Select three historical events that stress-test different aspects of the system:

1. A rapidly unfolding event.
2. A politically contested event.
3. A geographically distributed event.

Good candidates include the fall of Constantinople, the sinking of the Titanic, and the Cuban Missile Crisis.

Choose based on source availability, historical richness, and suitability for simulation.

Implement at least one complete vertical slice.

The demonstration must contain:

- A coherent, source-grounded timeline.
- Multiple historical accounts.
- Distinct perspectives.
- Meaningful posts and reply threads.
- Working historical time controls.
- Historical citations.
- Spoiler-aware playback.
- A usable mobile interface.
- A polished desktop interface.
- Accessible navigation.
- Functional search or filtering.
- A clear distinction between evidence and simulation.

The example should demonstrate a functioning product rather than a static mockup.

Use enough content to demonstrate how the experience unfolds, but do not fill the interface with unsupported fabricated history.

---

# Phase 10: Testing and Evaluation

Create automated tests for:

- Schema validity.
- Referential integrity.
- Temporal consistency.
- Historical knowledge constraints.
- Citation existence and alignment.
- Chronological ordering.
- Event replay determinism.
- Spoiler prevention.
- Rendering correctness.
- Responsive layouts.
- Keyboard accessibility.
- Search functionality.
- Bundle loading and caching.

Design an evaluation framework for historical fidelity.

Measure:

- Unsupported factual claims.
- Anachronisms.
- Incorrect attribution.
- Citation mismatches.
- Chronological contradictions.
- Knowledge leakage from future events.
- Character inconsistency.
- Repetitive or generic posts.
- Performance and load times.

Establish acceptance thresholds and clearly distinguish automated checks from claims requiring human historical review.

---

# Phase 11: Deliverables and Execution

Produce the following in order.

## A. Product specification

Explain the core experience, intended users, primary use cases, interaction model, and differentiation.

## B. Architecture decision record

Compare major alternatives using explicit criteria and justify the final selections.

## C. Canonical data specification

Deliver the full schema, relationships, example records, validation rules, and migration strategy.

## D. Source integration specification

Identify verified datasets, APIs, repositories, licenses, and ingestion methods.

## E. AI prompt library

Deliver complete reusable prompts and structured output contracts for every required generation and verification stage.

## F. UX and visual design system

Specify layouts, components, navigation, typography, colors, responsive behavior, and accessibility.

## G. Technical implementation specification

Provide project structure, modules, dependencies, APIs, database migrations, caching, and deployment configuration.

## H. Working application

Implement the functioning MVP, including real source-backed demonstration content and automated tests.

## I. Evaluation report

Report actual test results, measured performance, historical validation outcomes, known limitations, and remaining risks. Never invent measurements or claim tests were executed when they were not.

## J. Development roadmap

Prioritize future work by user impact, historical fidelity, cost, complexity, and architectural dependency.

---

# Engineering principles

1. **Historical evidence is the source of truth.** Generated posts are representations of that evidence, not replacements for it.

2. **Separate facts from presentation.** The same historical records should support timelines, social feeds, maps, educational lessons, and future interfaces.

3. **Model uncertainty explicitly.** Historical records are incomplete and sometimes contradictory.

4. **Prevent hindsight leakage.** Historical actors must operate within plausible contemporary information boundaries.

5. **Preserve provenance.** Every factual assertion should be traceable to its evidence.

6. **Optimize the data model before optimizing the interface.** A beautiful social network built on incoherent historical data will not scale intellectually or technically.

7. **Prefer precomputation.** Generate and verify historical experiences ahead of time whenever possible.

8. **Keep the architecture simple.** Complexity must earn its place.

9. **Design for thousands of events.** Avoid assumptions specific to one historical period.

10. **Build something people actually want to use.** Historical rigour and engaging interaction should reinforce one another.

---

# Required working method

Begin with research into xeet and existing historical-data ecosystems.

Then formalize the domain model and compare architectural alternatives.

Select and justify the canonical data format before implementing the application.

Produce concrete schemas, examples, and interfaces rather than vague descriptions.

Make reasonable assumptions independently. Ask questions only when a missing decision materially blocks implementation.

Where tradeoffs are uncertain, create small benchmarks or prototypes rather than relying on intuition.

Where historical information is uncertain, preserve that uncertainty rather than inventing certainty.

Where external resources cannot be verified, identify the limitation explicitly.

If implementation tools are available and authorized, proceed through the working vertical slice, run tests, inspect the actual rendered application, and repair defects.

If implementation is not authorized or tools are unavailable, provide executable specifications and complete implementation-ready artifacts without pretending that code was run.

**Final objective:** Produce the foundation for a historically accurate, highly engaging, scalable social-network simulation of human history, with a canonical data model strong enough to support many future interfaces and educational experiences.