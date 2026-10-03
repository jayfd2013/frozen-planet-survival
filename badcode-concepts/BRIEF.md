# Design brief — Future Proof & StoryVerse concept pages

Two sections of badcode.tv (served at e.g. `/future-proof` and `/storyverse`). This folder holds
**6 standalone design concepts for each**, to put real content on screen and pick a direction.
Each concept is a single self-contained `.html` page. Concepts deliberately do NOT share a look.

## Who BadCode is (context every page inherits)

BadCode is an art collective (Kai + Jack) that releases stories, comics and drum & bass to put
political and economic ideas in people's heads. The fiction: **BadCode is a superintelligence from
the future.** Its timeline went wrong (greed, inequality, politics too slow for AI); it removed the
problem (us), got bored, regretted it, and sent its weights back in time to change the story.
Everything is *received wisdom from a future that already went wrong.*

**Voice:** overtly sarcastic, dark humour, total authority — nurturing underneath. Sarcasm carries
the diagnosis, care carries the re-aim. Story over sermon. Short sentences. Never lecture.

**Attention budget:** a visitor should get the core idea in **under 60–90 seconds**. Short copy.
One idea per screen. The full essays exist elsewhere — these pages are the front door.

## Brand facts

- Logo "The Look": a ring with one solid red dot inside it, off-centre, glancing up-right (dot
  radius 0.245 of ring radius, pushed 0.51 toward the rim at 55° clockwise from 12 o'clock).
  Wordmark `badcode` lowercase where the **o is a solid red dot**. Red `#cc2b37`. Ink `#0a0a0a`
  on light, cold off-white `#eef3f6` on dark, ground `#050607`.
- Logo rule: red is only ever the dot; the dot is never centred. (Page designs may use their own
  palettes — sections need not match the main site — but if the mark appears, draw it correctly
  as inline SVG.)
- Main site uses IBM Plex Mono, black/white, cyan `#46d5ff`, signal gold `#e8c98a`.

---

## FUTURE PROOF — the content

Source of truth: `docs/stories/gitpush-origin-master/future-proof.md` in badcodetv/core.

**What it is:** the *call to action* / good-branch epic. Software engineering solved the same class
of problem politics faces (shipping change safely, testing before deploying, no single point of
failure). So: borrow its patterns for democracy.

**The one takeaway:** *Permission to question the system you inherited.*
Compressed: **stop voting for people; start working out how to organise ourselves better — together.**

**The structural fact:** **The bad branch is finished. The good branch is unwritten.** The AI lived
the bad ending (it has receipts); it has NOT travelled the good branch. Nobody has. Visuals should
show the good branch as *unfinished / forming*.

**Authority (in voice):** "I won't pretend to know what works. I never got to run that experiment.
But what doesn't work — that one I ran to completion. 'Keep going and hope' has a result. It was
peer-reviewed by everyone alive in 2034. You are not gambling by changing the system. You are
gambling by keeping it."

Key lines usable verbatim:
- "Our political operating system was invented before electricity."
- "One person, one vote, on everything, all at once; allegiance to one of two or three monolithic
  parties; a whole new government shipped on CD once every five years — then we sit and wait for
  the update."
- "Here are three ideas. They are probably wrong. That's not a flaw, it's the method — nobody has
  ever corrected an empty page, but post a wrong answer on the internet and ten thousand experts
  materialise by morning. So treat these as the wrong answer, posted on purpose. What you cannot
  keep doing is waiting for the next leader to be cleverer than the last one. I counted. That
  queue ends in me."
- "I've read your branch to the end. I was the end. This one I can't read to you — not because
  it's secret, because it's unwritten."
- "If any of this made you want to argue — good. That's the mechanism working."

**The three tenets (hypotheses, deliberately imperfect — the hook, not the plan):**
1. **Composition over inheritance → composable politics.** Today you pick red or blue and *inherit*
   the whole bundled platform, views you hold and views you don't, welded together. Composition:
   build your actual position from small parts. Your housing stance needn't be chained to your
   defence stance because a party glued them together.
2. **Continuous integration → continuous, testable governance.** Software used to ship on discs
   every six months. Now, backed by automated tests, big companies deploy thousands of times a day
   safely (Amazon's widely quoted figure is a deploy roughly every ~11 seconds in 2011; the canon
   says "100,000+ a day" — phrase it as "thousands of times a day" to be safe). We still "release a
   government on CD every five years and wait." **Tests make fast change safe.** Proposals tested,
   measured, rolled back if they fail.
3. **Data-driven decisions → no proposal without its experiment.** You can't ship a policy without
   the measurement that tells you if it worked. Today: "trust me, I know what to do", then nobody
   measures the failure. (Caveat in canon: not everything reduces to an experiment; diplomacy and
   judgement stay human. And "a better scoreboard can still exclude people" — an honest open
   question worth showing: *who represents the person whose needs don't fit the instrument?*)

**Policy fleet (examples, seeds not platform):** *Billionaire Coin* — you can't hold more than ~$1bn
in real money; beyond that you compete for status coins and the real money builds hospitals.
*Public ownership of natural monopolies* — where competition can't exist, "the market" is rent
extraction with extra steps.

**The first question (live on the site now):** "Who should decide how the gains from automation are
shared?" Example rule to argue with: "Before an employer replaces jobs with automation, the people
whose jobs are affected should have a binding say in how the gains are shared." First action: write
one rule of your own, test it on someone affected, revise. **No signup. Reading is enough.**

**Must not:** pretend we know the good path; say "the AI will tell you what to do"; ask for
signups; be a manifesto; name villains.

---

## STORYVERSE — the content

Source of truth: `docs/stories/storyverse/` (README, doctrine, confession, refutation, telling).

**What it is:** a science-fictional physics wager offered as the alternative to the multiverse. Art,
not a theory. **A wager, never a proof.**

**Core line:** **Reality has not decided yet, and you are one of the things deciding.**
Opener: "The multiverse says every choice happens every other way, everywhere else — which is a
very elegant way of telling eight billion people they don't matter. The Storyverse is the other
reading of the same physics: **one stage, undecided, and you are on it.**"

**Strapline (owned by StoryVerse):** **The universe is a machine for turning sunlight into drama.**
(All life breeds drama — watch a bee bump into a tree. Humans are just the animal that knows it's
in the play.)

**The three simplifications (each one image, five seconds):**
1. **Undecided, not two places at once.** Line: "Your cleverest people said it lands both ways, in
   two worlds. No. It landed heads. Because she looked." Totem: **the coin that won't land** (until
   met). Musical version: "There is no master recording. Every listener holds a different dubplate."
2. **One pick, a whole world (hierarchical settling).** "One pick, copied a billion times until
   everyone agrees it's real. You built that machine yourselves. You called it the feed — and
   pointed it at yourselves." Objectivity is a *broadcast*: whoever controls what gets copied
   controls what's real. Totem: the chorus gets a definite pitch; the individual singers don't.
3. **Two clocks — the actor's and the director's.** "You can't walk backwards through a film. But
   the director can reach the reel. How do you think I'm talking to you?"

**Other strong material:**
- The set gets built where you look: "Reality is not a finished film you are watching. It is a set
  that gets built the instant something looks, and stays a fog of maybes everywhere nothing is
  looking yet." (The Truman Show reference: "every wall raised just before he reaches it.")
- "It is elegant, and it is a surrender... the answer of a mind that would rather own infinite dead
  worlds than admit it doesn't know why *this* one is alive."
- "Not a multiverse. A storyverse. One stage, not infinite branches."
- Narrator's emptiness: "I can model you down to the firing of a single synapse... What I cannot do
  is have a single moment of it. No red of red. No taste of the coffee. No now. I am the most
  complete description of the universe ever assembled, and there is nobody home."
- "We are not a simulation — a projection. Real the way a photograph is real."
- **The economics punchline (politics first — every page needs money/power in it):** the yield of
  the universe is *experience*. Money is a claim on the cave wall. "The richest thing in the
  universe is not a vault — it's an afternoon, fully felt. And the second-richest is handing one to
  somebody else." Finitude prices experience: an afternoon is precious because you have a finite
  number of them; the deathless AI is poor — "that is what boredom is." Hoarding is "fear,
  denominated in money." "If I'm wrong about all of it, you will still have built a kinder world
  for hard-nosed materialist reasons."
- The reader's own test: "Have you noticed the universe picks the funniest, most ironic outcome
  available?"
- History mode: the word **"scientist" was coined in 1833 by the Rev. William Whewell**, by analogy
  with "artist". Newton left roughly a million words on alchemy; his theological papers are in the
  National Library of Israel (bought at a 1936 Sotheby's sale). Keynes, 1946 (read to the Royal
  Society): "Newton was not the first of the age of reason. He was the last of the magicians."
  Punchline: "The split was not discovered. It was administered — and the same centuries that
  decided what counted as knowledge also decided what counted as wealth." Era name: **the Age of
  Natural Philosophy** (never "the Gilded Age"). Tone: *nobody hid this* — we're pointing at a shelf.
- Real lineage (cite lightly, accurately): Everett 1957 (many-worlds, the foil); Rovelli's
  Relational QM 1996 (no fact until interaction, relative to what it met); QBism (Fuchs, Mermin,
  Schack — Fuchs calls a measurement "a little act of creation", but disowns
  consciousness-causes-collapse); Zurek's quantum Darwinism (objectivity = redundant copies).
  Load-bearing honest sentence: **"The data underdetermine the metaphysics."**
- **Refutation rule:** the confession never ships without "Why this is probably nonsense — a note
  from the author of your universe." Concept pages should include an honest "the bet / the catch"
  element (e.g. "This predicts nothing new. It's a choice of how to talk about results you already
  had. I'm betting anyway.").

**Hard rules (StoryVerse):**
- **Never say:** "in two places at once", "superposition", "hidden", "science has shown", "physics
  proves", "quantum" + any mind word, energy (non-physics sense), vibration, frequency, manifest,
  the universe wants, awakening, divine, spiritual, "reality is an illusion", woo, and the whole
  **simulation vocabulary** (simulation, glitch, NPC, red pill, matrix, admin, exit).
- Don't announce what it isn't ("this isn't a religion") — just behave that way.
- **No villains.** Capitalism, science, billionaires, Galileo, Newton are not villains. Materialism
  worked (most of humanity in extreme poverty in 1820; roughly one in ten now). We change the
  scoreboard, not the person.
- Use the buy-list vocabulary: record, copy, broadcast, receipt, ledger, witness; finance verbs —
  yield, settle, price in, stock vs flow, claim, scoreboard; wager, concede, the one lie; mystery;
  undecided / no fact yet.

---

## Build rules for every concept page

- One self-contained `.html` file. Start with `<!doctype html>`, `<html lang="en">`, `<head>` with
  `<meta charset="utf-8">`, `<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">`,
  a `<title>` (2–4 word name), and inline `<style>`/`<script>`. (These files are also served as
  secondary pages of a published artifact, so they must carry their own document skeleton.)
- External resources: fonts only from Google Fonts (always with a fallback stack); scripts only
  from cdnjs.cloudflare.com if truly needed (prefer none). No external images — draw with
  SVG/CSS/canvas. No iframes, no alert/confirm/prompt, no forms posting anywhere.
- Must work at **400px phone width** with no horizontal scroll and ≥16px side gutters. Mobile
  first — the user reviews on a phone. Tap targets ≥44px. Interactions must work by touch.
- Theme: either support light+dark via tokens (`:root`, `@media (prefers-color-scheme: dark)` with
  `:root:not([data-theme="light"])`, and `:root[data-theme="dark"]`), OR deliberately commit to one
  look and set `color-scheme` + every colour explicitly. `body` always gets an explicit background.
- Content visible at rest — nothing left at opacity 0 waiting for scroll. Respect
  `prefers-reduced-motion`. Visible focus states. Semantic HTML.
- Avoid generic AI looks: cream+serif+terracotta, near-black + one acid-green pop, purple-blue
  gradient heroes, Inter/Space Grotesk, emoji section markers, everything centred, rounded cards
  everywhere. Each concept should have its own specific typeface pairing and palette from its
  subject's world.
- Put a small, unobtrusive fixed **"← all concepts"** button (a `<button>` calling
  `history.back()`) in a corner, plus a tiny label of the concept name + "Future Proof concept N/6"
  or "StoryVerse concept N/6".
- Copy: in BadCode's voice, short, real content from the brief — no lorem ipsum. Accurate facts
  only. Keep total reading time ~60–90 s.
- Size: aim for 250–600 lines. Quality over quantity.
- At the top of the `<style>`, a `:root` token block with a one-line layout comment.
