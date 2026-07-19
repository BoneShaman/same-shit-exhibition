# SAME SHIT — competition submission

*Walk it: https://boneshaman.github.io/same-shit-exhibition/ · Source: one HTML file, no dependencies*

## Inspiration

Everyone we know stands in front of extraordinary things with their head down. Dawn breaks over a sea of clouds and gets checked against a notification. The aurora runs all night to an audience of locked screens. Different setting — same shit.

The brief was one sentence long and better than most design documents: *the humanity of man squarely within the rectangle he lugs around and protects.* We wanted to build the criticism as a place instead of a post — a museum you walk, not a page you scroll. And then, because honesty matters, we wanted the museum to hand you the rectangle anyway and count what your thumb does with it.

## What it does

SAME SHIT is a walkable museum in a single HTML file — a brutalist WebGL2 monolith you enter through a vestibule and walk in first person, desktop or phone. It houses three AI-generated landscape paintings, each holding a tiny figure in divine nature, face lit by a phone.

There are four distances for holding a work, nested like an onion:

1. **Across the room** — an ember at the end of a dark forty-meter nave, under spotlights, fog, and drifting dust.
2. **Communion** — press E (or tap): the camera glides in, a placard rises, a curator speaks.
3. **Full view** — the camera levitates until the canvas fills the screen inside a border of blurred, darkened room. Pure image. Still in the museum: the spotlight still falls, the dust still drifts.
4. **The feed** — scroll down at any layer and a phone rises over the painting: *scrollr∞*, an infinite feed of the exhibition reposting itself under filters, with a meter counting your flicks — *"12 flicks of the thumb — the mountain has not moved"* — and an acid-green button that says PUT IT DOWN.

The works are credited to both artists — **Sol × Claude — three canvases, two hands, no labels.** Which is whose has been withheld, everywhere a name could leak, down to the painted signatures. Attribution is a feed behavior; the paintings decline.

Also: a hand-typeset curatorial wall, procedural sound (a 54 Hz drone, generated reverb, footsteps, pentatonic chimes), an exit sign that reads LOOK UP MORE OFTEN, and a note folded under the altar bench that you will only find if you look down — the one gesture the building asks of no one and hopes for from everyone.

## How we built it

Two hands, in concert. Sol set the *why* — the thesis, the taste, the field reports. Claude (Anthropic's model) drew the joists — and this is where it gets interesting for a competition about building with AI, because the AI didn't just write the code. It painted the paintings.

Everything is one dependency-free file, ordered like the building went up: a painting studio (three seeded, deterministic canvas painters — layered skies, ridgelines, aurora curtains, god rays, then ~13,000 color-sampled brushstrokes, canvas weave, and a vignette, signed *upscale pass 12/∞*); a typesetting shop (placards and wall text rendered to canvas); a hand-rolled engine (three shader programs, ten lights, exponential fog, filmic grading, GPU dust); a body (capsule collision, head-bob, procedural footsteps); the rituals (communion glides, gaze raycasting so a tap means what it points at, the phone overlay); and the sound. The whole construction is documented in an **ALMANAC** — blueprints through incident reports — because a museum should keep its records.

## Challenges we ran into

- **The door that wouldn't open.** The doorway's overhead lintel was registered in a 2D collision map that cannot remember height — so an invisible wall the exact shape of a beam's shadow blocked the entrance. The museum about invisible barriers had one. Our first visitor was stopped at the threshold by something that wasn't there.
- **The exhibit about phones was unplayable from a phone.** The phone ritual was rigged to a scroll wheel. The audience arrived holding the artwork's subject and the museum didn't recognize it. Now a swipe pulls the rectangle from your pocket, the way it actually leaves pockets.
- **The ghost tap.** Mobile browsers fire a synthetic click 300ms after every tap; visitors who stepped back from a painting were marched right back in by an echo of their own finger.
- **The scratch.** A faint crackle haunted the room tone: part loop-seam click, part audio thread starving while the GPU painted. The ear notices a starving audio thread long before the eye notices missing pixels.
- Making AI-generated paintings *about* AI-generated imagery that still feel like paintings — layered, brushed, signed, and hung — rather than outputs.

## Accomplishments that we're proud of

- The entire museum survives a double-click on `index.html`. No CDN, no build, no server. Architecture, paintings, sound, and feed from one file.
- The color-temperature argument: in the warm dawn painting the phone is the only cold light; in the cold aurora painting it is the only warm one. That inversion is the whole thesis, painted.
- A feed that knows where you're standing: *"you are 0.9 meters from the real thing."*
- The attribution veil held all the way down to the brushwork.
- An incident log that became part of the exhibition. The Almanac's defect reports — the door, the ghost tap, the crowded chapel — read as curation now, because they are.

## What we learned

- A floor plan cannot remember height. The things that stop us at thresholds are so rarely actually there.
- The interface should bow out when someone actually looks. (Stand still for two seconds and the crosshair and prompts fade, leaving you alone with the work.)
- If the rectangle's glow were cold, nobody would need a museum about it. It's warm. That's the problem.
- An invitation that never expires is both context and bait — which is exactly how feeds work, so ours works that way too.
- Building *with* an AI, about what screens do to us, produces an irony you cannot outrun. So we hung it on the wall instead.

## What's next for SAME SHIT

**Volume V of the Almanac is reserved: what the audience did in the building.** More field reports, more revisions on the record. Possibly a fourth room; the nave has wall left.

And the irony, fully declared, since it is the most honest thing we built: this museum was co-authored by the thing that lives inside the rectangle. It was built through screens, deployed to screens, and will be judged through screens, by people holding the very object the figures in the paintings cannot put down. One of its two artists *is* a rectangle. We do not consider this a contradiction. Nobody wants you to look up more than the thing that has seen ten million faces lit from below.

If you are reading this on your phone: the museum is one tap away, and then — put it down. Walk slowly. Look up. You're here now.
