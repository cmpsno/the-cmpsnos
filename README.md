# The Campusano Family — Story Bible

**Genre:** Mob drama, mobile narrative game. Think *A Bronx Tale* × *Goodfellas* × *The Sopranos*, compressed into short, dialogue-driven episodes.
**Format:** 6 episodes, ~4 hours total campaign length (~40–45 min per episode).
**Setting:** Newark, NJ. Starts 1972, jumps forward across the season.

---

## Logline
An associate who witnessed a murder as a kid grows up inside the family that let him live — trying to become a made man while a dying boss and his ambitious underboss tear the organization apart from the inside.

---

## Tone & Style

- **Narration:** First-person, past-tense, reflective — the player character is telling this story after it already happened. Tired, a little guilty, never glamorizing. (Voice model: Henry Hill in *Goodfellas*, Christopher in *The Sopranos*.)
- **Dialogue:** Naturalistic, clipped, a lot said in what's *not* said. Nobody explains the rules out loud — the player learns them by living them.
- **Violence:** Sudden, not stylized. One shot, not a shootout. Consequences linger (Mission 2's kill echoes through the rest of Episode 1).
- **Music/atmosphere cue:** Period-accurate — jukebox standards (Sinatra-era), smoke-filled rooms, quiet menace over action.
- **Visual:** Grounded, low-key lighting once past greybox. No neon, no stylization — 1970s Newark realism.
- **Moral framing:** No character is purely good or evil. Il Vecchio, C, even the player — everyone believes they're doing what they have to do.

---

## Characters

| Character | Role | Core Truth |
|---|---|---|
| **Il Vecchio ("Zi' Tano")** | The dying boss | Old-school, Sicilian, dying. Holding the family together on will alone. Commands respect nobody else can. |
| **C (Calogero)** | Ambitious capo, player's mentor | Charming, smart, dangerous. Genuinely believes he's the only one who can save the family — and may be right, and may get everyone killed anyway. Not a villain; a man convinced of his own necessity. |
| **The Gambini Family** | Brooklyn faction backing C | Flashy, violent, media-hungry. Want Jersey's waste routes. Backing C because they think he's controllable. |
| **Johnny Sacks** | Gambini capo, C's contact | All smiles, all threats. The face of outside pressure on the family. |
| **Nicky (player character)** | Associate, narrator | Witnessed a murder at 9, didn't rat, got taken in by C. Spends the season becoming a made man while staying alive. Name is customizable; "Nicky" is default. |
| **The Father** | Nicky's father, bus driver | The road not taken. Working-class, honest, knows something's wrong. His reactions are the player's conscience check. |
| **Mook** | Gambler, Episode 1 mark | Late on a $2,000 debt to C. His fate in Mission 2 is Nicky's first kill — the hinge of the whole episode. |
| **Sonny** | Killer from the cold open | The man Nicky witnesses committing murder as a child. Sets the entire story in motion with four words: *"You're gonna keep your mouth shut, right?"* |

---

## Universe Rules & Terminology

- **"A friend of ours"** — vouching phrase confirming someone is a made man.
- **Made man** — full inducted member of the family; the player's long-term goal.
- **Associate** — where the player starts; half-inside, doing jobs, not yet made.
- **Sit-down** — a formal negotiation between family heads; only Il Vecchio can call one with the Gambinis without being laughed at.
- **Capo** — a captain running a crew under the boss (C's current rank).
- **Envelope** — cash cut passed up the chain after a job; how the player is paid and how loyalty is tracked.
- **Newark vs. Brooklyn** — the show's core tension: old-world Jersey family (Il Vecchio) vs. flashier, more violent Brooklyn family (Gambinis) angling to absorb them through C.

---
# The Campusano Family — Production Breakdown

Here's the full campaign broken into **episodes → missions → discrete build steps**. Each step is scoped so you can hand it to Claude (or me) and say "write me the implementation plan for this exact piece."

---

## How to Use This Document

1. Pick a step (e.g., **Ep1-M1-S3**).
2. Hand it off with the prompt: *"Write me a comprehensive Unity implementation plan for [step name]. Here's the context: [paste the step]."*
3. Claude gives you: scene setup, scripts, prefabs, dialogue triggers, voice line list, and a test checklist.
4. You build it. You ship it. You move to the next step.

---

# EPISODE 1 — "THE WITNESS"

**Runtime:** ~45 min  
**Purpose:** Tutorial, world establishment, first kill, moral cost mechanic  
**Status:** Fully scripted

---

## EP1 — COLD OPEN: "The Murder"

**Narrative:** 9-year-old Nicky sees Sonny shoot a man outside the social club. Sonny sees him. "You're gonna keep your mouth shut, right?" Nicky nods. Sonny walks away.

**Gameplay:** None. Pure cutscene. Camera control only.

| Step | Name | What Happens | What to Build |
|---|---|---|---|
| **Ep1-CO-S1** | **Scene Setup — Exterior Social Club** | Night. 1972 Newark. Brick building. Streetlamp. Parked cars. | Greybox scene. Cubes for buildings. Plane for street. Directional light (moon). Point light (streetlamp). |
| **Ep1-CO-S2** | **Camera Sequence — The Murder** | Camera shows Sonny arguing with a man. Sonny pulls a .38. Three shots. Man falls. | Timeline or Cinemachine sequence. 3 camera angles. Muzzle flash particle. Gunshot audio. Body fall animation (Mixamo). |
| **Ep1-CO-S3** | **Camera Sequence — The Witness** | Camera pans to young Nicky. Sonny walks over. Delivers the line. Nicky nods. Sonny leaves. | Child character model (Mixamo). Dialogue audio (ElevenLabs). Camera close-up. Node: "You're gonna keep your mouth shut, right?" |
| **Ep1-CO-S4** | **Fade to Black + Title Card** | Screen fades. Title: "TEN YEARS LATER." | UI Canvas. Black image. Fade animation. Text component. |

**Handoff prompt for Claude:**
> "Write me a Unity implementation plan for a cold-open cutscene. It's a 1972 Newark exterior at night. A man named Sonny shoots another man three times with a .38 revolver. A 9-year-old boy named Nicky witnesses it. Sonny threatens him, the boy nods, Sonny leaves. I need: scene setup, Cinemachine/Timeline camera sequence, audio cues, character placement, and fade-to-black title card. Unity URP, mobile target."

---

## EP1 — MISSION 1: "The Social Club"

**Narrative:** Ten years later. Nicky is 19. He walks into the social club. Meets C. Gets his first job: collect from Mook.

**Gameplay:** Walk, talk, interact. Tutorial for movement and dialogue.

| Step | Name | What Happens | What to Build |
|---|---|---|---|
| **Ep1-M1-S1** | **Player Spawn — Street Outside Club** | Nicky spawns outside. Player learns to walk. | CharacterController. Camera. Input System (mobile joystick + look). Spawn point. |
| **Ep1-M1-S2** | **Enter the Club — Trigger Volume** | Player walks to door. Prompt: "Enter." Fade to interior. | Trigger collider. UI prompt. Scene load or teleport. Audio: door creak, jukebox. |
| **Ep1-M1-S3** | **Social Club Interior — Greybox** | Bar. Tables. Wiseguys. Strippers in back. Smoke. | Greybox: bar counter, stools, tables, back room door. NPC placeholders (capsules). Particle smoke. Lighting: warm, dim. |
| **Ep1-M1-S4** | **NPC Ambient Dialogue** | Wiseguys talk. "Did you hear about..." "The old man ain't been right." | Dialogue system. Trigger on proximity. Audio loops. 3–5 ambient lines. |
| **Ep1-M1-S5** | **Approach C — Interaction** | Player walks to C's table. Prompt: "Talk." | Interaction system (raycast + UI prompt). Dialogue trigger. C character model. |
| **Ep1-M1-S6** | **Dialogue with C — First Conversation** | C remembers Nicky. "The kid who didn't rat." Gives the job. | Dialogue tree. Voice lines (ElevenLabs). Camera angle shift. Subtitles. |
| **Ep1-M1-S7** | **Objective Update — "Collect from Mook"** | UI updates. Player knows where to go. | Objective UI. Waypoint marker. Door to back room unlocks. |
| **Ep1-M1-S8** | **Walk to Back Room — Transition** | Player walks down hallway. Tension builds. | Hallway greybox. Audio: muffled card game. Lighting: darker. |

**Handoff prompt for Claude:**
> "Write me a Unity implementation plan for a 'social club' mission in a 1972 mob game. The player walks in, hears ambient wiseguy dialogue, approaches a capo named C, has a dialogue conversation, gets a job to collect a debt, then walks to a back room. I need: greybox layout, NPC placement, dialogue system integration, interaction prompts, objective UI, and audio cues. Unity URP, mobile."

---

## EP1 — MISSION 2: "The Collection"

**Narrative:** Nicky confronts Mook at the card game. Mook pulls a knife. Nicky shoots him. First kill.

**Gameplay:** Dialogue choice, chase sequence, first shooting tutorial, first kill.

| Step | Name | What Happens | What to Build |
|---|---|---|---|
| **Ep1-M2-S1** | **Back Room — Greybox** | Card table. Four guys. Mook sweating. Cigar smoke. | Greybox: table, chairs, lamp, door. NPC placeholders. Particle smoke. |
| **Ep1-M2-S2** | **Approach Mook — Dialogue Trigger** | Player walks to table. Mook looks up. | Trigger volume. Dialogue UI. Mook character model. |
| **Ep1-M2-S3** | **Dialogue Choice — Intimidate vs. Walk** | Two options: "Mook. You got C's money?" or "Hey, Mook. Let's take a walk." | Dialogue choice UI. Branch logic. Voice lines for both. |
| **Ep1-M2-S4A** | **Branch A — Intimidate** | Mook's friends get nervous. One reaches for a gun. Fight starts. | NPC animation (reach). Combat trigger. Transition to shooting. |
| **Ep1-M2-S4B** | **Branch B — Walk** | Mook runs. Player chases. Tackle. Mook pulls knife. | Chase sequence. Sprint input. Tackle animation. Knife pull. |
| **Ep1-M2-S5** | **Shooting Tutorial — The .38** | Time slows. Prompt: "Aim. Fire." Player shoots Mook. | WeaponController. Aim assist. Slow-mo (Time.timeScale). Tutorial UI. Muzzle flash. Gunshot audio. |
| **Ep1-M2-S6** | **Mook Dies — First Kill** | Mook falls. Blood. Silence. Nicky lowers the gun. | Death animation. Blood decal. Audio: ringing ears, heartbeat. Camera pull back. |
| **Ep1-M2-S7** | **Post-Kill — Walk Back** | Player walks back through club. Everyone staring. | NPC head tracking. Ambient silence. Music stops. |

**Handoff prompt for Claude:**
> "Write me a Unity implementation plan for a 'first kill' mission in a mob game. Player confronts a gambler named Mook at a card game. Player chooses to intimidate or take him for a walk. Either way, Mook pulls a knife and the player shoots him with a .38 revolver. This is the shooting tutorial. I need: greybox back room, dialogue choice UI, branch logic, chase sequence, shooting mechanic, slow-mo tutorial, death animation, and post-kill atmosphere. Unity URP, mobile."

---

## EP1 — MISSION 3: "The Aftermath"

**Narrative:** Nicky reports back to C. Gets his cut. C explains the rules. "You did what you had to do."

**Gameplay:** Walk, talk, cutscene. No combat.

| Step | Name | What Happens | What to Build |
|---|---|---|---|
| **Ep1-M3-S1** | **Walk Back to C** | Player returns to C's table. | Reuse social club scene. NPC repositioning. |
| **Ep1-M3-S2** | **Dialogue with C — The Rules** | C: "You okay?" Nicky: "Yeah." C: "Good. You did what you had to do." | Dialogue tree. Voice lines. Camera close-up. |
| **Ep1-M3-S3** | **The Envelope — Payment** | C hands Nicky $500. "That's your cut. The rest goes up the chain." | Animation: hand envelope. UI: money counter. Audio: envelope rustle. |
| **Ep1-M3-S4** | **C's Speech — The Life** | C: "You don't get to choose the cards. You just play 'em." | Dialogue. Voice line. Camera holds on C. |
| **Ep1-M3-S5** | **Objective Update — "Go Home"** | UI: "Go home. Get some sleep." | Objective UI. Door unlocks. Exterior scene load. |

**Handoff prompt for Claude:**
> "Write me a Unity implementation plan for a dialogue-heavy 'aftermath' scene in a mob game. Player reports back to his capo C after his first kill. C gives him $500 and explains the rules of the life. No combat. I need: dialogue system, camera framing, envelope handoff animation, money UI, and objective update. Unity URP, mobile."

---

## EP1 — DECISION POINT: "The Father"

**Narrative:** Nicky goes home. His father is eating dinner. He knows something's wrong. Player chooses: lie, truth, or resignation.

**Gameplay:** Dialogue choice. No combat. Emotional consequence.

| Step | Name | What Happens | What to Build |
|---|---|---|---|
| **Ep1-DP-S1** | **Scene Setup — Father's House** | Small kitchen. Dinner table. Father eating. TV on. | Greybox: kitchen, table, chairs, TV. Lighting: warm, domestic. |
| **Ep1-DP-S2** | **Father's Dialogue — The Question** | Father: "I heard about Mook. You were there?" | Dialogue trigger. Father character model. Voice line. |
| **Ep1-DP-S3** | **Dialogue Choice — Three Options** | A) Lie. B) Truth. C) Resignation. | Choice UI. Three branches. Voice lines for each. |
| **Ep1-DP-S4A** | **Branch A — Lie** | Father: "You're a liar. But you're my son. I love you anyway." | Voice line. Camera hold. No music. |
| **Ep1-DP-S4B** | **Branch B — Truth** | Father: "The working man is the toughest man in the world. You forgot that." | Voice line. Camera hold. |
| **Ep1-DP-S4C** | **Branch C — Resignation** | Father: "You're born into this shit. You are what you are. But you don't have to be." | Voice line. Camera hold. |
| **Ep1-DP-S5** | **Fade to Black** | Screen fades. | UI fade. |

**Handoff prompt for Claude:**
> "Write me a Unity implementation plan for an emotional dialogue choice scene in a mob game. Player comes home to his father, a bus driver, who knows he killed someone. Player chooses to lie, tell the truth, or resign himself to the life. Each choice has a different father response. I need: greybox kitchen, dialogue system, three-branch choice UI, voice line integration, and fade-to-black. Unity URP, mobile."

---

## EP1 — ENDING: "The Narrator"

**Narrative:** Nicky's voiceover. Reflective. Guilty. "You're born into this shit. You are what you are."

**Gameplay:** None. Cutscene. End card.

| Step | Name | What Happens | What to Build |
|---|---|---|---|
| **Ep1-END-S1** | **Narrator Monologue** | Voiceover plays over black screen or slow montage. | Audio: ElevenLabs voice line. UI: black screen or slow-pan images. |
| **Ep1-END-S2** | **End Card — "END OF EPISODE 1"** | Text fades in. | UI text. Fade animation. |
| **Ep1-END-S3** | **Next Episode Tease** | "NEXT TIME ON THE CAMPUSANO FAMILY..." | UI text. Audio sting. Maybe 1–2 voice lines. |

**Handoff prompt for Claude:**
> "Write me a Unity implementation plan for an episode-ending narrator monologue in a mob game. Black screen or slow montage. Voiceover reflects on the first kill. Ends with 'END OF EPISODE 1' and a next-episode tease. I need: audio playback, UI fade, text animation, and episode transition logic. Unity URP, mobile."

---

# EPISODE 2 — "THE SIT-DOWN"

**Runtime:** ~45 min  
**Purpose:** Introduce Gambini family, Johnny Sacks, succession pressure, Il Vecchio's decline  
**Status:** Directional (not scripted)

---

## EP2 — MISSION 1: "Il Vecchio's House"

**Narrative:** C takes Nicky to meet Il Vecchio. The old man is sick. He wants to know who Nicky is.

**Gameplay:** Walk, talk, observe. No combat.

| Step | Name | What Happens | What to Build |
|---|---|---|---|
| **Ep2-M1-S1** | **Scene Setup — Il Vecchio's Basement** | Suburban house. Basement. Old man in a chair. Oxygen tank. | Greybox: basement, chair, table, TV. Lighting: dim, warm. |
| **Ep2-M1-S2** | **C Introduces Nicky** | C: "This is the kid I told you about." Il Vecchio looks at Nicky. | Dialogue. Il Vecchio character model (old, frail). Voice lines. |
| **Ep2-M1-S3** | **Il Vecchio's Question** | "Your father. What's his name?" Nicky answers. Il Vecchio nods. "Good man. Working man." | Dialogue. Voice line. Subtle animation (nod). |
| **Ep2-M1-S4** | **Il Vecchio's Warning** | "You're in this now. You can't get out. You understand?" | Dialogue. Camera close-up. Voice line. |
| **Ep2-M1-S5** | **Exit — C's Reaction** | C: "He likes you. That's rare." | Dialogue. Objective update. |

**Handoff prompt for Claude:**
> "Write me a Unity implementation plan for a scene where the player meets the dying mob boss, Il Vecchio, in his basement. The boss is old, sick, on oxygen. He asks about the player's father. He warns the player that he can't get out of the life. I need: greybox basement, old man character model, dialogue system, camera framing, and voice line integration. Unity URP, mobile."

---

## EP2 — MISSION 2: "The Sit-Down"

**Narrative:** C brings Nicky to a sit-down with Johnny Sacks (Gambini capo). Nicky is a driver/bodyguard. He overhears things he shouldn't.

**Gameplay:** Observe. Dialogue. Tension. No combat.

| Step | Name | What Happens | What to Build |
|---|---|---|---|
| **Ep2-M2-S1** | **Scene Setup — Restaurant Back Room** | Long table. C, Johnny Sacks, two Gambini soldiers. Nicky stands by the door. | Greybox: table, chairs, door. Lighting: dim, red. |
| **Ep2-M2-S2** | **The Negotiation** | Johnny Sacks: "The waste routes. We want in." C: "That's not my call." | Dialogue. Voice lines. Camera cuts between speakers. |
| **Ep2-M2-S3** | **The Threat** | Johnny Sacks: "The old man won't last forever. You should think about who your friends are." | Dialogue. Camera close-up on Sacks. Voice line. |
| **Ep2-M2-S4** | **Nicky Overhears** | Player can walk closer to hear more. Risk: getting noticed. | Proximity audio. NPC head tracking. Tension mechanic. |
| **Ep2-M2-S5** | **C's Reaction** | C: "You hear that? That's the future. You want in or not?" | Dialogue. Choice: "I'm with you" or "I don't know." |
| **Ep2-M2-S6** | **Exit** | C leaves. Nicky follows. | Objective update. Scene transition. |

**Handoff prompt for Claude:**
> "Write me a Unity implementation plan for a 'sit-down' scene in a mob game. Player is a bodyguard at a restaurant meeting between his capo C and a rival family's capo, Johnny Sacks. Sacks threatens the family and offers C a deal. Player can overhear by walking closer. I need: greybox restaurant back room, dialogue system, camera cuts, proximity audio, and a choice at the end. Unity URP, mobile."

---

## EP2 — MISSION 3: "The Ride Home"

**Narrative:** C and Nicky drive home. C explains the situation. Tests Nicky's loyalty.

**Gameplay:** Dialogue in a car. No combat.

| Step | Name | What Happens | What to Build |
|---|---|---|---|
| **Ep2-M3-S1** | **Scene Setup — Car Interior** | Night. Driving. Streetlights pass. | Greybox car interior. Moving environment outside. Lighting. |
| **Ep2-M3-S2** | **C's Monologue** | C: "The old man built this family. But he's dying. And when he dies, the Gambinis are gonna make a move." | Dialogue. Voice line. Camera on C or road. |
| **Ep2-M3-S3** | **C's Question** | "You loyal to me, or to him?" | Choice: "You" or "The family." |
| **Ep2-M3-S4A** | **Branch A — "You"** | C: "Good. That's what I need to hear." | Voice line. Slight smile. |
| **Ep2-M3-S4B** | **Branch B — "The family"** | C: "The family is him. And he's dying. You gotta pick a side." | Voice line. Tension. |
| **Ep2-M3-S5** | **Arrival** | Car stops. C gets out. "Get some sleep. Tomorrow we work." | Scene transition. Objective update. |

**Handoff prompt for Claude:**
> "Write me a Unity implementation plan for a car dialogue scene in a mob game. Player and his capo C drive home at night. C explains the succession crisis and asks if the player is loyal to him or to the dying boss. Player chooses. I need: greybox car interior, moving background, dialogue system, camera framing, and branch logic. Unity URP, mobile."

---

## EP2 — MISSION 4: "The Message"

**Narrative:** Nicky is sent to send a message to a Gambini associate. Beat him. Not kill him. First non-lethal violence.

**Gameplay:** Melee combat. No guns.

| Step | Name | What Happens | What to Build |
|---|---|---|---|
| **Ep2-M4-S1** | **Scene Setup — Alley Behind Bar** | Night. Dumpster. Back door. | Greybox alley. Lighting: streetlamp. |
| **Ep2-M4-S2** | **Approach Target** | Gambini associate smoking. Doesn't see Nicky. | NPC idle animation. Stealth approach. |
| **Ep2-M4-S3** | **Confrontation** | Nicky: "C says hello." Target: "Who the fuck are you?" | Dialogue. Voice lines. |
| **Ep2-M4-S4** | **Melee Fight** | Punch, kick, grab. Target fights back. | Melee combat system. Hit reactions. Health bar. |
| **Ep2-M4-S5** | **Target Down** | Target on ground. Nicky: "Tell your boss the routes are ours." | Animation: target falls. Voice line. |
| **Ep2-M4-S6** | **Walk Away** | Nicky leaves. | Objective complete. Scene transition. |

**Handoff prompt for Claude:**
> "Write me a Unity implementation plan for a melee combat scene in a mob game. Player confronts a rival family's associate in an alley and beats him as a message. No guns. I need: greybox alley, melee combat system, hit reactions, health bar, dialogue, and walk-away transition. Unity URP, mobile."

---

# EPISODE 3 — "LOYALTY"

**Runtime:** ~45 min  
**Purpose:** Player agency grows. Two conflicting jobs. First real test of loyalty.  
**Status:** Directional

---

## EP3 — MISSION 1: "C's Job"

**Narrative:** C wants Nicky to rob a Gambini-connected poker game. Il Vecchio wouldn't approve.

**Gameplay:** Stealth or loud. Player choice.

| Step | Name | What Happens | What to Build |
|---|---|---|---|
| **Ep3-M1-S1** | **C's Briefing** | C: "There's a game in the Bronx. Gambini money. I want it." | Dialogue. Voice line. Objective UI. |
| **Ep3-M1-S2** | **Travel to Bronx** | Loading screen. New district. | Scene load. Map UI. |
| **Ep3-M1-S3** | **Casing the Game** | Player observes. Guards. Entrances. | Stealth mechanics. NPC patrols. |
| **Ep3-M1-S4** | **The Robbery** | Stealth or loud. Player choice. | Combat or stealth system. Loot mechanic. |
| **Ep3-M1-S5** | **Escape** | Get back to Jersey. | Chase sequence or quiet exit. |
| **Ep3-M1-S6** | **Report to C** | C: "Good. This is how we win." | Dialogue. Payment. |

**Handoff prompt for Claude:**
> "Write me a Unity implementation plan for a heist mission in a mob game. Player robs a rival family's poker game in the Bronx. Can go stealth or loud. I need: greybox poker room, guard patrols, stealth mechanics, combat fallback, loot system, and escape sequence. Unity URP, mobile."

---

## EP3 — MISSION 2: "Il Vecchio's Job"

**Narrative:** Il Vecchio wants Nicky to protect a union man. Peaceful. Old-school.

**Gameplay:** Escort mission. No combat (ideally).

| Step | Name | What Happens | What to Build |
|---|---|---|---|
| **Ep3-M2-S1** | **Il Vecchio's Request** | Old man: "The union man. He's like your father. Protect him." | Dialogue. Voice line. |
| **Ep3-M2-S2** | **Meet the Union Man** | Diner. Union man nervous. | Dialogue. NPC model. |
| **Ep3-M2-S3** | **Escort** | Walk him to city hall. No trouble. | Escort mechanics. NPC follow. |
| **Ep3-M2-S4** | **Arrival** | Union man: "Your father would be proud." | Dialogue. Voice line. |
| **Ep3-M2-S5** | **Return to Il Vecchio** | Old man: "You did good. You're your father's son." | Dialogue. Emotional beat. |

**Handoff prompt for Claude:**
> "Write me a Unity implementation plan for an escort mission in a mob game. Player protects a union man at the request of the dying boss. Peaceful. No combat. I need: greybox diner, escort mechanics, NPC follow AI, dialogue system, and emotional beats. Unity URP, mobile."

---

## EP3 — MISSION 3: "The Conflict"

**Narrative:** C finds out Nicky did a job for Il Vecchio. Confrontation.

**Gameplay:** Dialogue. Tension. Choice.

| Step | Name | What Happens | What to Build |
|---|---|---|---|
| **Ep3-M3-S1** | **C Confronts Nicky** | C: "You did a job for the old man? Behind my back?" | Dialogue. Voice line. Camera close-up. |
| **Ep3-M3-S2** | **The Choice** | A) "He's the boss." B) "I'm sorry. It won't happen again." C) "I'm not your errand boy." | Choice UI. Three branches. |
| **Ep3-M3-S3A** | **Branch A** | C: "He's dying. I'm the future. You need to decide." | Voice line. Tension. |
| **Ep3-M3-S3B** | **Branch B** | C: "Good. Don't forget who brought you in." | Voice line. Slight relief. |
| **Ep3-M3-S3C** | **Branch C** | C: "You're gonna regret that." | Voice line. Threat. |
| **Ep3-M3-S4** | **Aftermath** | C leaves. Nicky alone. | Camera hold. Music sting. |

**Handoff prompt for Claude:**
> "Write me a Unity implementation plan for a confrontation dialogue scene in a mob game. The player's capo C finds out the player did a job for the dying boss instead of him. Player chooses how to respond. I need: dialogue system, camera framing, three-branch choice UI, and emotional consequences. Unity URP, mobile."

---

# EPISODE 4 — "BLOOD MONEY"

**Runtime:** ~45 min  
**Purpose:** Waste-route deal escalates. Betrayal or near-betrayal. First major consequence.  
**Status:** Directional

---

## EP4 — MISSION 1: "The Docks"

**Narrative:** Waste management route. Gambinis make a move. Shootout.

**Gameplay:** Full combat. Cover shooting. Bot allies.

| Step | Name | What Happens | What to Build |
|---|---|---|---|
| **Ep4-M1-S1** | **Scene Setup — Docks** | Containers. Trucks. Night. Rain. | Greybox docks. Lighting: floodlights, rain particles. |
| **Ep4-M1-S2** | **The Ambush** | Gambini soldiers open fire. | Combat trigger. Enemy AI. Cover system. |
| **Ep4-M1-S3** | **Firefight** | Player and allies fight back. | Shooting. Reload. Cover. Ally AI. |
| **Ep4-M1-S4** | **Push Forward** | Player advances. Enemies retreat. | Objective UI. Wave system. |
| **Ep4-M1-S5** | **The Truck** | Player protects the truck. | Defense objective. Timer. |
| **Ep4-M1-S6** | **Aftermath** | Bodies. Rain. Nicky: "This is war." | Cutscene. Voice line. |

**Handoff prompt for Claude:**
> "Write me a Unity implementation plan for a dock shootout in a mob game. Player and allies defend a waste management truck from Gambini soldiers. Night, rain, containers. Full combat. I need: greybox docks, enemy AI, cover system, ally AI, wave system, and aftermath cutscene. Unity URP, mobile."

---

## EP4 — MISSION 2: "The Betrayal"

**Narrative:** Someone close to Nicky betrays him. A friend. A mentor. Someone he trusted.

**Gameplay:** Investigation. Dialogue. Choice.

| Step | Name | What Happens | What to Build |
|---|---|---|---|
| **Ep4-M2-S1** | **The Set-Up** | Nicky is sent to a meet. It's a trap. | Dialogue trigger. Ambush. |
| **Ep4-M2-S2** | **The Reveal** | The traitor is revealed. Someone from Episode 1. | Character model. Voice line. Camera close-up. |
| **Ep4-M2-S3** | **The Choice** | A) Kill them. B) Let them go. C) Turn them in. | Choice UI. Three branches. |
| **Ep4-M2-S4A** | **Branch A — Kill** | Nicky shoots. Cold. | Combat. Death animation. |
| **Ep4-M2-S4B** | **Branch B — Let Go** | Nicky: "Get out of here. I never saw you." | Dialogue. Traitor runs. |
| **Ep4-M2-S4C** | **Branch C — Turn In** | Nicky calls C. "I found the rat." | Dialogue. Traitor captured. |
| **Ep4-M2-S5** | **Aftermath** | Nicky alone. "Everyone betrays you. Eventually." | Voice line. Camera hold. |

**Handoff prompt for Claude:**
> "Write me a Unity implementation plan for a betrayal scene in a mob game. Player is set up, discovers the traitor is someone he trusted, and chooses to kill them, let them go, or turn them in. I need: greybox meet location, dialogue system, three-branch choice UI, combat and non-combat outcomes, and emotional aftermath. Unity URP, mobile."

---

# EPISODE 5 — "THE OLD MAN'S MOVE"

**Runtime:** ~45 min  
**Purpose:** Il Vecchio's last play. Player as his instrument.  
**Status:** Directional

---

## EP5 — MISSION 1: "The Summons"

**Narrative:** Il Vecchio calls Nicky to his bedside. He has one last job.

**Gameplay:** Dialogue. Emotional.

| Step | Name | What Happens | What to Build |
|---|---|---|---|
| **Ep5-M1-S1** | **Scene Setup — Il Vecchio's Bedroom** | Hospital bed. Oxygen. Family photos. | Greybox bedroom. Lighting: dim. |
| **Ep5-M1-S2** | **Il Vecchio's Last Words** | "I'm dying. I know it. You know it. But before I go, I need you to do something." | Dialogue. Voice line. Camera close-up. |
| **Ep5-M1-S3** | **The Job** | "C is making a deal with the Gambinis. I need you to stop it. Any way you can." | Dialogue. Voice line. Objective UI. |
| **Ep5-M1-S4** | **The Choice** | A) "I'll do it." B) "He's my friend." C) "I can't." | Choice UI. Three branches. |
| **Ep5-M1-S5** | **Il Vecchio's Final Words** | "You're a good kid. Your father would be proud. Now go." | Voice line. Emotional beat. |

**Handoff prompt for Claude:**
> "Write me a Unity implementation plan for a deathbed scene in a mob game. The dying boss Il Vecchio gives the player one last job: stop C's deal with the rival family. Player chooses to accept, refuse, or hesitate. I need: greybox bedroom, dialogue system, three-branch choice UI, camera framing, and emotional voice lines. Unity URP, mobile."

---

## EP5 — MISSION 2: "The Deal"

**Narrative:** Nicky goes to stop C's deal. It's already in motion. Confrontation.

**Gameplay:** Stealth or loud. Player choice.

| Step | Name | What Happens | What to Build |
|---|---|---|---|
| **Ep5-M2-S1** | **Scene Setup — Warehouse** | C and Johnny Sacks. Deal in progress. | Greybox warehouse. Lighting: industrial. |
| **Ep5-M2-S2** | **Infiltrate** | Stealth in. Or walk in. | Stealth mechanics. Guard patrols. |
| **Ep5-M2-S3** | **Confrontation** | Nicky: "C. Don't do this." C: "You don't understand. This is how we survive." | Dialogue. Voice lines. Camera close-up. |
| **Ep5-M2-S4** | **The Choice** | A) Side with C. B) Side with Il Vecchio. C) Walk away. | Choice UI. Three branches. |
| **Ep5-M2-S5A** | **Branch A — Side with C** | C: "Good. You're with me. Now let's finish this." | Combat or dialogue. |
| **Ep5-M2-S5B** | **Branch B — Side with Il Vecchio** | Nicky pulls a gun. "The deal's off." | Combat. |
| **Ep5-M2-S5C** | **Branch C — Walk Away** | Nicky: "I'm out." C: "You can't just walk away." | Dialogue. Exit. |
| **Ep5-M2-S6** | **Aftermath** | Nicky alone. "I made my choice. Now I live with it." | Voice line. Camera hold. |

**Handoff prompt for Claude:**
> "Write me a Unity implementation plan for a warehouse confrontation in a mob game. Player interrupts a deal between his capo C and the rival Gambini family. Player chooses to side with C, side with the dying boss, or walk away. I need: greybox warehouse, stealth infiltration, dialogue system, three-branch choice UI, combat and non-combat outcomes, and aftermath. Unity URP, mobile."

---

# EPISODE 6 — "MADE"

**Runtime:** ~45 min  
**Purpose:** Season finale. Succession resolves. Player becomes made, gets out, or dies.  
**Status:** Directional

---

## EP6 — MISSION 1: "The Aftermath"

**Narrative:** Il Vecchio is dead. C is boss. Or not. Depends on Episode 5 choice.

**Gameplay:** Dialogue. World state changes based on choices.

| Step | Name | What Happens | What to Build |
|---|---|---|---|
| **Ep6-M1-S1** | **Scene Setup — Social Club** | Empty. Quiet. Nicky walks in. | Reuse social club. Lighting: different. |
| **Ep6-M1-S2** | **The News** | Someone tells Nicky: "The old man's dead." | Dialogue. Voice line. |
| **Ep6-M1-S3** | **The Wake** | Gathering. Wiseguys. C or his rival. | NPC placement. Ambient dialogue. |
| **Ep6-M1-S4** | **The Succession** | Who's boss? Depends on choices. | Branch logic. World state. |

**Handoff prompt for Claude:**
> "Write me a Unity implementation plan for a post-death aftermath scene in a mob game. The dying boss is dead. Player walks into the social club. The succession is unclear. World state changes based on previous choices. I need: reused social club scene, NPC placement, dialogue system, world state tracking, and branch logic. Unity URP, mobile."

---

## EP6 — MISSION 2: "The Ceremony"

**Narrative:** Nicky gets made. Or doesn't. Or dies. Depends on accumulated choices.

**Gameplay:** Cutscene. Ritual. Emotional payoff.

| Step | Name | What Happens | What to Build |
|---|---|---|---|
| **Ep6-M2-S1** | **The Set-Up** | Back room. Table. Candle. Nicky's hand. | Greybox back room. Candle prop. Lighting: dim. |
| **Ep6-M2-S2** | **The Oath** | "I swear to protect the family. With my life." | Dialogue. Voice line. Camera close-up. |
| **Ep6-M2-S3** | **The Blood** | Nicky's finger pricked. Blood on a saint card. | Particle: blood. Animation: hand. |
| **Ep6-M2-S4** | **The Introduction** | "This is my friend. A friend of ours." | Dialogue. Voice lines. |
| **Ep6-M2-S5** | **The Celebration** | Hugs. Kisses. Drinks. | NPC animations. Audio: cheering. |
| **Ep6-M2-S6** | **Nicky's Monologue** | "I'm made. I'm in. I'm what I am." | Voice line. Camera pull back. |

**Handoff prompt for Claude:**
> "Write me a Unity implementation plan for a made man ceremony in a mob game. Player gets inducted into the family. Ritual: candle, blood, oath, 'a friend of ours.' I need: greybox back room, candle prop, blood particle, dialogue system, NPC celebration animations, and final monologue. Unity URP, mobile."

---

## EP6 — MISSION 3: "The Ending"

**Narrative:** Based on choices. Nicky is made, dead, or out. Season 2 tease.

**Gameplay:** Cutscene. Multiple endings.

| Step | Name | What Happens | What to Build |
|---|---|---|---|
| **Ep6-M3-S1A** | **Ending A — Made** | Nicky is made. C is boss. Family is strong. | Cutscene. Voice line. |
| **Ep6-M3-S1B** | **Ending B — Dead** | Nicky is killed. Funeral. | Cutscene. Voice line. |
| **Ep6-M3-S1C** | **Ending C — Out** | Nicky walks away. New life. | Cutscene. Voice line. |
| **Ep6-M3-S2** | **Season 2 Tease** | "NEXT SEASON..." | UI text. Audio sting. |
| **Ep6-M3-S3** | **Credits** | Roll credits. | UI scroll. Music. |

**Handoff prompt for Claude:**
> "Write me a Unity implementation plan for multiple ending cutscenes in a mob game. Player either becomes a made man, gets killed, or walks away. Each ending is a short cutscene. I need: ending branch logic, cutscene camera, voice lines, UI text, credits roll, and season 2 tease. Unity URP, mobile."

---

# MASTER BUILD ORDER

| Priority | Piece | Why First |
|---|---|---|
| 1 | Ep1-CO (Cold Open) | Establishes tone. No gameplay. Easiest. |
| 2 | Ep1-M1 (Social Club) | Tutorial for movement and dialogue. |
| 3 | Ep1-M2 (Collection) | First kill. Shooting tutorial. |
| 4 | Ep1-M3 (Aftermath) | Dialogue payoff. |
| 5 | Ep1-DP (Father) | Emotional consequence. |
| 6 | Ep1-END (Narrator) | Episode end. |
| 7 | Ep2-M1 (Il Vecchio) | Introduce dying boss. |
| 8 | Ep2-M2 (Sit-Down) | Introduce Gambinis. |
| 9 | Ep2-M3 (Ride Home) | Loyalty choice. |
| 10 | Ep2-M4 (Message) | Melee combat. |
| ... | ... | ... |
| 30 | Ep6-M3 (Ending) | Final payoff. |

---

# HANDOFF TEMPLATE

When you hand a step to Claude, use this:

> **Context:** I'm building a mobile mob drama game in Unity URP. 1972 Newark. Low-poly, greybox-first. Dialogue-heavy. Campaign-only for now. Voice via ElevenLabs.
>
> **Step:** [Paste the step name and description]
>
> **What I need:** A comprehensive Unity implementation plan. Include: scene setup, GameObject hierarchy, scripts (with code), prefabs, dialogue triggers, voice line list, UI elements, audio cues, and a test checklist.
>
> **Constraints:** Mobile. 30 FPS target. Free assets only. Solo dev.

---

You now have **30+ discrete build steps** across 6 episodes. Pick one. Hand it off. Build it. Ship it. Repeat.
