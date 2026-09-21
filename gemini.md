An evaluation of the story bible, campaign structure, and production plan for the mobile mob drama project [cmpsno/the-cmpsnos](https://github.com/cmpsno/the-cmpsnos?utm_source=gemini) reveals strong narrative clarity and disciplined solo-developer engineering, alongside a few technical risks to address.

---

## 1. Narrative & Story Bible Assessment

### Strengths

* **Clear Core Identity:** Combining *A Bronx Tale*, *Goodfellas*, and *The Sopranos* into short, dialogue-driven mobile episodes creates an immediate, recognizable benchmark.


* **Voice-Driven Exposition:** The first-person past-tense narrator framing allows emotional weight to be carried by voiceover audio and minimalist staging. This strategy reduces the need for expensive facial animation or cinematic asset fidelity.


* **Grounded Moral Conflict:** Framing the tension around the decay of the local Newark family versus the aggressive Brooklyn expansion (Gambinis) gives the story clear stakes. Placing Nicky's working-class father as his moral compass anchors the dialogue choices.



### Risks & Refinements

* **Length Ambition:** Target runtime of 6 episodes at 40–45 minutes each (~4 hours total) is ambitious for a solo developer. Keeping the scope strictly dialogue-driven with minimal, repeatable environments is critical to reaching the finale.


* **Episode 3–6 Scope Creep:** While Episodes 1 and 2 are tightly scripted, Episodes 3–6 outline dynamic features like multi-branch heists, escort AI, cover shootouts, and branching betrayal states. These mechanics must be simplified into scripted encounter beats—similar to Episode 1's Mook kill—to maintain production velocity.



---

## 2. Game Development & Scope Discipline

The production plan demonstrates strong scope discipline by making deliberate engineering cuts to keep development achievable.

| Dimension | Original Bible Concept | Evaluated / Scoped Implementation | Evaluation |
| --- | --- | --- | --- |
| **Cold Open (Ep 1)** | Real-time simulated murder with child & adult rigs.

 | Lightweight cinematic; fixed/panning camera; capsule blockouts; voiceover focus.

 | **Optimal.** Prevents building one-off child models or complex skeletal cutscene rigs.

 |
| **Mook Chase (Ep 1)** | Fleeing NPC pathfinding, sprint input, physical tackle.

 | Scripted trigger beat; short flee sequence converging to a single shot.

 | **Essential Cut.** Avoids building full physics/ragdoll tackle logic for a single mission beat.

 |
| **Character Visuals (Ep 2)** | Conflicting calls for capsule-only graphics vs. Mixamo skeletal animations.

 | Capsule-only primitives using transform/scale tweens (e.g., height drop for sitting, bobbing for speech).

 | **Realistic.** Resolves asset contradictions and maintains mobile performance targets.

 |
| **Sit-Down Interaction (Ep 2)** | Standing in different room spots during negotiation.

 | Position-gated dialogue nodes (`Shoulder`, `Back Wall`, `Sideboard`).

 | **Strong Mechanics.** Creates interactive replayability through data-driven line filtering without complex gameplay programming.

 |

---

## 3. Technical Architecture & UX Feasibility

### Strengths

* **Data-Driven Dialogue System:** Upgrading the dialogue controller to support position gating (`PositionalDialogueLine`) and branching choices allows narrative complexity to scale through content files rather than new code systems.


* **Mobile-First Touch & UI Standards:** Explicit constraints—88×88px minimum touch targets, 18sp subtitles, 70% opacity dark backing, and tap-to-continue triggers—ensure high usability on small device viewports.


* **Soft-Lock Prevention:** Introducing a 4–5 second timeout fallback on mandatory interaction prompts (such as the "Tap to React" prompt in Ep 2) prevents player soft-locks if input is missed.


* **Lightweight Persistence:** Serializing `JobState` flags to JSON stored in `PlayerPrefs` across discrete episode stage checkpoints keeps save data predictable and straightforward.



### Gaps to Monitor

1. **Asset Imports & Tooling:** Automated import pipelines for ElevenLabs audio files ensure correct compression and mono settings, preventing performance drops on mobile hardware.


2. **State Backward-Compatibility:** As `JobState` expands across 6 episodes, default values must be assigned safely so older save checkpoints do not break as new fields are added.



---

## Summary & Next Steps

1. **Lock Ep 1 & Ep 2 Pipelines:** Proceed with the discrete task order outlined in the build plans (retrofitting Ep 1 checkpointing, extending the dialogue controller, and implementing capsule transform tweens).


2. **Apply Scripted Encounter Templates to Ep 3–6:** Refactor the directional notes for later episodes (e.g., the Ep 4 dock shootout) into scripted sequence triggers rather than fully simulated AI cover systems.


3. **Maintain Capsule First Strategy:** Resist adding complex rigged characters until the full campaign is playable end-to-end in greybox form.
