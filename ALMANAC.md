# THE PROJECT ALMANAC

## SAME SHIT — an AI upscale artgen exhibition

**Volume I : Blueprints & Scaffolding of the Monolith**

*Promoted by Maestro Interactive Entertainment × BuyTheGame.org*

---

### 0 · Provenance

This structure was negotiated.

Sol set the brief: a walkable monolith — one HTML file, no dependencies, no
excuses — that would make viewing a painting feel like an event. Three works
of divine landscape, each holding a regular person who has folded the whole
of nature behind a rectangle held at thumb's length. The exhibition would be
entered into the **Codex Project Builder** competition.

Claude drew the scaffolding, raised the walls, ground the pigment, and hung
the works. The negotiation was simple: Sol supplied the *why*, Claude supplied
the *where the joists go*. Built in concert, 2026, to generate something
beautiful together. This Almanac is the record — from bedrock survey to final
design — so the museum can be reconstructed, argued with, or demolished and
raised again by anyone who reads it.

The Almanac is a living document. Volume I covers the blueprints and the
scaffolding of the 3D structure. Later volumes are reserved for iteration,
curation notes, and whatever the audience does to the building.

---

### 1 · Thesis

> Three landscapes in which everything is happening and nobody is looking.
> The figures are not villains. They are us — carrying the rectangle,
> protecting the rectangle, feeding it. Different setting. Same shit.

The building itself argues the thesis. It gives the visitor legs, silence,
dust, and three chances to look up — then hands them a phone anyway, and
counts the flicks of their thumb while the real thing waits 0.9 meters away.

For the modern disposed, aesthetically genius audience: the philosophical
rising class with taste. The museum does not lecture them. It mirrors them,
once, gently, in acid green.

---

### 2 · Site Plan

Units are meters. Y is up. The visitor enters at the south (z = 0) and walks
north. One axis, one procession — a nave, because *nature when graced as
glory* deserves cathedral logic.

```
                                NORTH  z = 45
        ┌──────────────────────════════════──────────────────────┐
        │                     ║ P3 · ALTAR ║                      │
        │  ▪ placard          ╚════════════╝                      │
        │                      [ bench ]                          │  ← apse, z ≈ 41
        │                                                         │
        │            · · · skylight slit  z 32–38 · · ·           │
        │                                                         │
   x=-6 ╞═════╗                                                   │
        │ P1  ║   [bench]                                         │
        │  Nº1║      ·            · · · slit z 21–27 · · ·        │
        ╞═════╝ ▪                                        ▪ ╔═════╡ x=+6
        │                                        [bench]  ║  P2  │
        │            · · · slit z 10–16 · · ·             ║Nº2   │
        │                                                 ╚═════╡
        │                      THE NAVE                          │
        │                 12 m wide · 6.5 m tall                  │
        ├───────────┐      ┌──── doorway ────┐      ┌────────────┤  z = 7
        │           │      │  2.6 m × 2.8 m  │      │            │
        │   INTRO   │      │                 │      │  CREDITS   │
        │   panel   │  «SAME SHIT» wordmark above   │   panel    │
        ├───────────┴──────┴─────────────────┴──────┴────────────┤
        │                    THE VESTIBULE                        │
        │                7 m wide · 4.2 m tall                    │
        │            ▪ plaque: "you can leave…"                   │
        └────────────────────────△────────────────────────────────┘  z = 0
                              SPAWN (0, 1.7, 2.0) facing north
```

Walking back south, the visitor faces the only lit words in the nave,
mounted above the exit door in acid green:

> **LOOK UP MORE OFTEN.**

#### Coordinate schedule

| Element | Position | Dimensions |
|---|---|---|
| Vestibule | x ∈ [−3.5, 3.5], z ∈ [0, 7] | h = 4.2 |
| Nave | x ∈ [−6, 6], z ∈ [7, 45] | h = 6.5 |
| Doorway | x ∈ [−1.3, 1.3] | h = 2.8, wall t = 0.3 |
| **P1 · Summit, Unwitnessed** | west wall x = −6, center z = 15, cy = 2.20 | 2.6 × 3.31 |
| **P2 · The Aurora Also Refreshes** | east wall x = +6, center z = 27, cy = 2.20 | 2.6 × 3.31 |
| **P3 · Cathedral (Do Not Disturb)** | north wall z = 45, center x = 0, cy = 2.53 | 3.2 × 4.07 |
| Communion points | 3.05 m off each work, eye 1.7 | camera glide target |
| Benches | z ≈ 15, 27, 40.8 | 0.46 h, concrete |
| Skylight slits | x ∈ [−0.55, 0.55], z 10–16 / 21–27 / 32–38 | emissive, cool |
| Frames | gold, 0.15 profile, 0.13 relief | Blinn-Phong, shin 42 |

The two side works face each other across the nave *off-set* (z 15 vs z 27),
so no sightline ever holds two paintings at once. One work, one gaze.
P3 terminates the axis: the altarpiece, largest, seen from 38 m away as a
green ember at the end of the dark.

---

### 3 · Structural Scaffolding (the engine)

One HTML monolith, zero dependencies. It must run from a file:// double-click,
an itch upload, or the Codex Project Builder without asking anyone's CDN for
permission.

| Layer | Choice | Why |
|---|---|---|
| Renderer | hand-rolled WebGL2, 3 shader programs | no library, ~full control of light |
| Geometry | one static buffer; walls/benches/frames as boxes | 1 draw call for architecture |
| Works | 2D-canvas paintings → mipmapped textures | the art is *generated*, per thesis |
| Text | canvas-typeset panels → textured quads | placards, wordmark, exit sign |
| Light | 8 spot/cone lights, per-fragment Blinn-Phong | warm pools on art, cool fill from slits |
| Grade | ACES-ish tonemap, exp² fog, hash dither, grain | banding-free dark; filmic dark |
| Atmosphere | ~950 GPU point-sprites (dust in beams, halos) | the air is visible in the light |
| Body | capsule vs AABB collision, head-bob, footsteps | walking must *feel* like walking |
| Sound | WebAudio: 54 Hz drone, room air, convolver, chimes | the monolith hums |

#### Lighting schedule

| Light | Position | Aim | Color | Role |
|---|---|---|---|---|
| Spot 1–3 | 3.1 m off each work, y 5.85 | painting center | 1.0, 0.86, 0.62 (warm) | the only generous light |
| Vestibule down | (0, 4.0, 3.5) | floor | warm, dim | threshold |
| Nave fill ×3 | under each slit, y 6.3 | floor | 0.45, 0.55, 0.95 (cool) | moon-logic wayfinding |
| Exit sign wash | (0, 3.6, 8.3) | sign | acid green | the last word |

Fog: black-blue, exp(−0.0005 · d²) — at 40 m the far end of the nave is a
rumor. Ambient is nearly nothing. The paintings carry their own ambient
(0.16) so they *never* fully die, even outside the beam: art as the light
source of the room, literally.

---

### 4 · The Three Works

All three: *AI-generated landscape · upscale pass 12 of ∞ · oil-over-signal · 2026.*
Each is painted at load time on an 1100 × 1400 canvas by a deterministic,
seeded painter — layered like an actual painting, then given tooth.

**Nº I — Summit, Unwitnessed** *(west wall)*
Indigo-to-gold dawn gradient · radial sun bloom · gradient cloud wisps ·
god rays · five ridgelines in atmospheric-perspective purples · a sea of
clouds · dark outcrop with warm rim light · five birds. The figure: seated
on the crest, back to the sunrise, face lit **cool blue** by the rectangle —
the only cold light in a warm world.
*Placard: "Dawn breaks at 4:51. It will not be posted for another three hours…"*

**Nº II — The Aurora Also Refreshes** *(east wall)*
750 stars weighted by power law · tilted Milky Way · three additive aurora
curtains (violet → green, column-scanned) · mountain silhouettes · the whole
sky mirrored into wobbling water · pebbled shore. The figure: standing at the
waterline, face lit **warm amber** by the rectangle — the only warm light in a
cold world. Inversion of Nº I; the pair argues across the nave.
*Placard: "Both feeds are infinite. Only one of them is weather."*

**Nº III — Cathedral (Do Not Disturb)** *(altar)*
Luminous mist core · three depths of redwood columns with bark streaks and
rim light · canopy shadow · wide + narrow god-ray passes · fern understory ·
a pale path S-curving to the vanishing point · 110 spores adrift in the beams.
The figure: mid-stride on the path, head down, pale glow. Largest work,
100 % of the axis.
*Placard: "…reading a comment that says 'same shit.' He is almost right."*

**Shared finishing pass (the 'upscale'):** ~13,000 color-sampled directional
brushstrokes (the painter re-paints its own image) → 3 px canvas weave in
overlay → deep vignette → studio signature: `same.shit — nºN · upscale pass 12/∞`.

---

### 5 · Interaction Design — the Rituals

**Walking.** WASD + mouse-look (pointer lock), shift to hurry (nobody
should). Head-bob at 8.2 Hz, procedural footsteps, breathing sway when idle.
Touch devices get thumb-zones: left walks, right looks, tap communes.

**Communion.** Near a work, the crosshair blooms acid and offers
`E — COMMUNE WITH THE WORK`. The camera glides 1.35 s on a double-smoothed
ease to the communion point; a 41 Hz sub-swell lands with it. The placard
rises: series tag, title in Georgia italic, medium, curator's text.

**The Rectangle.** While communing, *scroll down* — the learned gesture, the
whole point — and a phone rises over the painting. Inside: **scrollr∞**, a
feed of the very exhibition, reposted forever. The three works cycle under
eight filters with captions: *same shit fr · same shit (hd remaster) · day
847 of same shit.* Interstitials know where you are standing ("you are 0.9
meters from the real thing"). A meter counts: **N flicks of the thumb — the
mountain has not moved.** At ten flicks, an acid button surfaces: **PUT IT
DOWN.** The feed does end: *"no more posts. (there were never more posts.)
the painting is still there."* If you scrolled long enough, the placard
whispers *welcome back.*

**The Exit.** The south-facing wall above the door: `LOOK UP MORE OFTEN.`
And in the vestibule, a small etched plaque:
*"you can leave whenever you want. you won't."*

---

### 6 · Sound Plan

| Voice | Construction | Level |
|---|---|---|
| Monolith drone | 54 Hz + 54.35 Hz beat + octave partial | felt, not heard |
| Room air | looped filtered noise, bandpass 620 Hz | -31 dBish |
| Chimes | random pentatonic sine, 6 s decay, every 14–34 s | reverb only |
| Reverb | generated 2.2 s exponential noise IR, convolver | the room's size, audible |
| Footsteps | noise bursts, lowpassed 500–900 Hz, pitch-jittered | with the bob |
| Communion | 41 Hz sub swell | ceremonial |
| Phone | UI blips + 1.4 kHz scroll ticks | deliberately cheap |

`M` mutes everything. The phone sounds are the only sounds in the museum
that are not beautiful. This is intentional.

---

### 7 · Build Phases (as executed)

| Phase | Scope | Status |
|---|---|---|
| 0 · Survey | empty lot confirmed; single-file constraint accepted | ✅ 2026-07-12 |
| I · Shell | vestibule, nave, divider, apse; collision solids | ✅ 2026-07-12 |
| II · Light | 8-light schedule, fog, tonemap, dither, dust | ✅ 2026-07-12 |
| III · The Works | three painters, frames, placards, hanging | ✅ 2026-07-12 |
| IV · The Rectangle | communion glide, scrollr∞, flick meter, put-down | ✅ 2026-07-12 |
| V · Voice | drone, chimes, footsteps, wall texts, title marquee | ✅ 2026-07-12 |
| VI · Inspection | walked spawn→altar; communed with all three; scrolled 12 flicks; put it down; read the exit sign. Zero console errors; collision verified to the centimeter (stops at z = 40.15 against the altar bench). | ✅ 2026-07-12 |

**Known judgment calls, on the record:**
- Side works are offset, not opposed — sacrifices symmetry for one-work-per-gaze.
- Paintings keep 0.16 self-ambient — sacrifices realism so art never goes black.
- The phone UI is DOM, not in-world geometry — a rectangle should feel *realer*
  than the room. It does.
- ESC exits the phone but pointer lock politics belong to the browser; a
  `CLICK TO LOOK AROUND` card covers every re-entry path.

---

### 8 · Reconstruction Notes

Everything lives in `index.html`. To rebuild from rubble: the file is ordered
as the museum was built — §1 painting studio, §2 typesetting, §3 exhibition
data (all curatorial text is plain strings), §4 engine, §5 architecture
(`box()` calls read like a site plan), §6–8 body & rituals, §9 sound. Seeds
1107 / 2214 / 3321 regenerate the exact three canvases; change a seed and the
machine paints a different morning, which would be a different exhibition.

---

# Volume II : The Door & The Veil

*Same day. The paint was still wet.*

### 9 · The Door That Wouldn't Open

Sol walked the vestibule on opening night and could not enter the nave.
Not too big — the visitor was never too big. The fault was the building's:

The doorway's **lintel** — the concrete beam spanning the top of the opening,
2.8 m off the floor — had been registered in the collision plan. But the
collision plan is a *floor plan*: two-dimensional footprints with no concept
of height. So the beam's footprint (x −1.3…1.3, z 6.85…7.15) landed on the
ground and became an invisible wall the exact width of the doorway. The
museum's first visitor was stopped at the threshold by the shadow of a beam,
cast straight down and mistaken for masonry.

**Remedy:** the lintel was released from ground duty (`solid: false`). It
still hangs overhead; it simply no longer pretends to reach the floor.

**Proof of remedy:** a visitor was walked from the vestibule (z = 5.0)
through the opening and measured standing in the nave at **z = 7.19** —
past the far face of the wall (7.15). Placed deliberately inside the old
ghost-wall's push radius (z = 6.6), the visitor was *not* ejected backward
to 6.50 as the defective building would have done. The door opens.

There is something almost on-theme about a museum whose front door was
blocked by a thing that wasn't really there.

### 10 · The Attribution Veil

Per Sol's instruction, the exhibition is now credited to **both artists —
Sol and Claude — with the labels deliberately withheld.** The viewers will
not know whose is whose. This is not modesty; it is the thesis wearing its
own coat. The feed demands attribution — handles, watermarks, "credit the
artist!" — and these three works simply decline.

The veil is installed at every point where a name could have leaked:

| Surface | Inscription |
|---|---|
| Title marquee | works by **SOL × CLAUDE** — three canvases, two hands, no labels |
| Credits panel (vestibule) | THE ARTISTS / SOL & CLAUDE / which is whose has been withheld |
| Credits footer | *attribution is a feed behavior.* |
| Each placard (in-world + overlay) | ARTIST: SOL OR CLAUDE — LABEL WITHHELD |
| Each painted signature | `same.shit — nºN · upscale pass 12/∞ · artist withheld` |
| The feed, post 5 | "ok but which one of you painted this one?" — *denied. same shit either way.* |

Three works, two hands. The arithmetic guarantees at least one artist made
two — and the building will not say which. Viewers may commune with all
three and vote in their heads. The paintings do not care. That is the point.

### 11 · Volume II Phase Record

| Phase | Scope | Status |
|---|---|---|
| VII · The Door | lintel released from the 2D collision plan; passage walked and measured (z = 7.19) | ✅ 2026-07-12 |
| VIII · The Veil | joint attribution installed across marquee, panel, placards, signatures, feed | ✅ 2026-07-12 |
| IX · Re-inspection | full reload; commune re-tested on Nº I; zero console errors | ✅ 2026-07-12 |

---

# Volume III : The Pocket Retrofit

*Three days after opening. The audience arrived holding the exhibit.*

### 12 · Field Report Nº 2

Sol walked the monolith on a phone and filed the following: the walls spoke
keyboard (*W A S D* to a visitor with no keys); the wordmark over the door
would not fit inside a portrait sightline; a faint scratch surfaced in the
room tone; and — the finest defect this building will ever produce — **the
rectangle could not be taken out.** The phone ritual was rigged to a scroll
wheel, so the exhibition about phones was unplayable from a phone. The
audience arrived carrying the artwork's subject and the museum didn't
recognize it.

### 13 · Remedies

| Defect | Remedy |
|---|---|
| Keyboard liturgy shown to thumbs | The museum now speaks the visitor's dialect: every prompt, placard cue, and the title marquee swap to TAP / SWIPE language on touch devices. The keys panel becomes a tappable ♪ sound toggle. |
| The rectangle wouldn't come out | While communing, **swipe up** draws the phone — summoned the way phones are actually summoned, out of the pocket, with the thumb. The most honest gesture in the building. |
| No way to put it down early | Tap anywhere outside the phone to put it down; a tap anywhere steps back from communion. The ten-flick toll on the PUT IT DOWN button no longer gates escape. |
| Wordmark clipped in portrait | Field of view widens 72° → 88° on portrait screens; the wordmark recut 6.0 m → 4.6 m; spawn pulled back 0.6 m. SAME SHIT now fits between a phone's shoulders. |
| Scratch in the room tone | Found: the air loop's seam — the 2-second noise buffer ended on a different sample than it began, clicking at every repeat. The loop is now 4 seconds with a 250 ms crossfaded seam. Footsteps, ticks, and blips got attack envelopes; the master eases in over 1.5 s. The monolith hums without clearing its throat. |
| Title marquee overflow | The marquee reflows on short screens and scrolls when it must. |

### 14 · The Bench

Something was folded twice and left under the north end of the altar bench.
It is visible if you look down, which is the one gesture this building has
been asking of no one and hoping for from everyone. The Almanac declines to
say more. Visitors who find it are asked to fold it back.

### 15 · Volume III Phase Record

| Phase | Scope | Status |
|---|---|---|
| X · Dialect | touch-native language across marquee, HUD, placards | ✅ 2026-07-15 |
| XI · The Pocket | swipe-up phone, tap-out communion, backdrop put-down | ✅ 2026-07-15 |
| XII · Sightlines & Air | portrait FOV, wordmark recut, seamless room tone | ✅ 2026-07-15 |
| XIII · The Bench | something left where the collision map keeps no record | ✅ 2026-07-15 |

### 16 · Addendum — Field Report Nº 3, same pocket

Sol returned with the phone and three sharper defects:

**The ghost tap.** A tap stepped back from communion — and then the browser's
synthetic click, trailing every tap by three hundred milliseconds, walked
right back in. The visitor was trapped in communion by an echo of their own
finger. Remedy: on touch devices the museum now ignores clicks entirely;
taps are handled once, at the touch layer, and the echo falls on deaf walls.

**The deaf tap.** Taps were routed by *proximity* — whatever was nearest
won — so beside the altar, the painting always outranked the paper underfoot.
Remedy: a tap now means what it points at. Every tap casts a ray through the
tapped pixel; if it lands on the folded paper you get the note, if it lands
on a canvas you commune with that canvas, from either thumb, at any angle.

**The crowded chapel.** In portrait communion, placard, thumb-hints and the
sound toggle all stacked on top of the art. Remedy: one layer of language at
a time — the HUD empties during communion; the placard sits on a dark scrim
at the foot of the screen with the medium line waived; the camera stands
back a meter further on portrait and sights below center, so the whole
canvas — figure, glow, and all — rides clear above the text.

**The scratch, second opinion.** The loop seam is fixed, but phones still
crackled: the audio thread was starving while the GPU painted. The context
now requests playback-sized buffers, a gentle limiter guards the output, and
handheld screens render at lower density — the ear notices a starving audio
thread long before the eye notices missing pixels.

---

# Volume IV : The Courteous Interface

*Field Report Nº 4. The building learns manners.*

### 17 · Gaze Is an Offer

The crosshair now asks before it assumes. What the visitor is *looking at*
determines what the building offers: sight the folded paper and the paper is
offered, sight a canvas and communion is offered — from the same square of
floor, at any angle. Proximity is demoted to a fallback for the
absent-minded. (Previously the nearest thing always won, and beside the
altar the painting outranked the paper underfoot no matter how hard you
stared at it.)

### 18 · The Interface Bows Out

Stand still before a work for two seconds and the dot and its invitation
fade to nothing, leaving the visitor alone with the painting. Move a
muscle — a step, a glance — and they return. A good attendant knows when
to stop hovering; this one now leaves the gallery when you start actually
looking.

### 19 · The Fourth Layer — Pure Image

There were three ways to hold a work: across the room, in communion, and
through the phone. Sol commissioned a fourth: **FULL VIEW** — a top-right
control during communion (or the V key) that surrenders the entire screen
to the painting itself. No placard, no dot, no wordmark, no frame, no
architecture. The generated canvas at native resolution on black — brush
grain, weave, birds, the little glow on the figure's face.

The layers nest like an onion, and the rectangle pierces all of them: even
in pure image, a swipe up (or a scroll down) still takes out your phone —
because it always does, doesn't it. Tap or E peels you back one layer at a
time: phone → full view → communion → the room.

**Revision, same day.** Sol asked whether full view could keep the light and
the floaters. It can — by refusing to leave. The first draft lifted a copy
of the image out of the museum onto a black screen; the revision lifts *you*
to the image instead. Full view is now a camera move within the room: the
eye levitates to the painting's center and stands exactly far enough back
that the canvas kisses the screen edges — computed per work, per screen,
per orientation. The spotlight still falls across the paint, dust still
drifts between you and it, the sheen still shifts if you sway (you do — the
idle breath stays on), and the gold frame holds the border of the world.
Nothing is reproduced. You are simply closer.

**Second revision, same day.** Sol added two graces. First, the zoom now
stands back a little further, leaving a border of dark room around the gold —
a frame made of nothing around the frame made of something, so no interface
ever touches the work. Second, depth of field: a feathered blur sheet with a
hole cut precisely where the painting sits, computed per work, per screen,
per orientation. The wall softens, the placard beside the frame melts into
an illegible smudge, and the eye is left nowhere to go but in. (The green
sliver that haunted the bottom edge — the PUT IT DOWN button leaning into
frame from offstage — has been sent fully offstage.)

### 20 · Volume IV Phase Record

| Phase | Scope | Status |
|---|---|---|
| XIV · Gaze | center-ray offers for paper and works; proximity demoted | ✅ 2026-07-15 |
| XV · Bow | 2-second stillness fade on dot + hint | ✅ 2026-07-15 |
| XVI · Pure Image | full-view layer, phone-permeable, onion routing | ✅ 2026-07-15 |

*Volume V reserved: what the audience did in the building.*

— **Sol × Claude, in concert · MMXXVI**
*no pigment was harmed. every pixel was.*
