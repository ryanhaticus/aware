# Aware

Aware is a React Native mobile application built for low and no vision individuals to better improve individual mobility with camera-enabled smart glasses. Aware works by analyzing an environment with the smart glasses with a hosted LLM and then reading out alerts to the end-user. Alerts may be navigational (object in the way, approaching stairs, approaching curb, uneven surface, etc.), people related (the name of someone approaching, someone reached their hand out to shake hands, a notice the individual is approaching a dense crowd), transit-related (bus approaching, platform edges, car approaching), related to objects and belongings (dropped an item, last known location for an item), general hazards (wet floor signs, wet floors, out of order escalators/areas), animal related (cat on the floor, dog on the floor, etc.), weather (ice, puddles of water, etc.). Additionally, the user is able to setup their own alerts by describing what they'd like to be alerted about.

## Principles

- The app should be screen reader friendly and useable by those with full, low, or no vision. In some cases, full vision users may be individuals assisting the impaired person with setup. With that said, ALL functions should be able to be completed by someone with low or no vision independently.
- The app should be super accessible and feature generous margins, text sizes, contrasts, etc., and we should respect OS-level settings like accessibility options like increased test size.
- The app's technical function should prioritize low latency (reducing network roundtrips or streaming content wherever possible) as an alert given too late is completely worthless and actually worse in many circumstances (DO NOT over correct here, just let this be a guiding principle).
- The app is safety-critical and should be built as regulated software from the first commit: business logic is pure and unit tested, and the [critical paths](#critical-paths--100-branch-coverage-enforced) carry 100% branch coverage as an enforced merge gate. A missed curb or platform-edge alert is a physical-injury failure mode, and this product could one day be classified as a medical device.

## Features

### Realtime alerts
- **Environment analysis** — the glasses continuously stream the surroundings to a hosted LLM, which speaks concise alerts back to the user.
- **Alert categories** — grouped, toggleable sets of built-in alerts spanning navigation, streets & crossings, transit, people, objects & belongings, signs & wayfinding, hazards, animals, and weather. See [Realtime Alerts](#realtime-alerts) for the full catalog. Whole groups turn on or off at once.
- **Per-alert tuning** — every alert can be individually enabled and adjusted: **distance** to trigger at (e.g. 2 m / 5 m / 10 m), **urgency** (standard or urgent), the **sound** it plays, and whether the phone **buzzes (haptics)** alongside the spoken alert.
- **Custom alerts** — describe an alert in plain language ("tell me when my guide dog picks something up off the ground"). The LLM evaluates feasibility up front, tells the user how reliably it can detect it and what it will say, then tunes it like any built-in alert.

### Profiles & places
- **Profiles** — named sets of alert choices (e.g. *Commute*, *Indoors*, *Quiet*) that the user switches between, including by voice ("quiet mode").
- **Trusted places** — the app auto-switches profiles when arriving at a saved location, and always switches back to the street profile on leaving, announcing the change aloud.

### Reading
- **Reading mode** — press the **left button** on the glasses (or say "read this") and Aware reads whatever you're holding in front of the camera: a menu, pamphlet, letter, label, or package.
- **Framing guidance** — Aware coaches you to line up the page. If only part of it is in view it says which way to move ("text continues below — tilt down a little"); if it's too far to resolve it asks you to bring it closer ("hold it a few inches closer").
- **Navigate by voice** — follow-ups like "read the prices," "skip to desserts," or "read it again, slower."
- **Adjustable reading speed** and a list of recent reads.

### Ask Aware (push-to-talk)
- **Push-to-talk** — hold the **right button** on the glasses, ask a question or give a command, then release to send. No wake word needed, and it stays reliable in loud places where a spoken trigger fails.
- **Ask for anything Aware can do** — *"What's around me?"* · *"What bus is this?"* · *"Where did I leave my cane?"* · *"Read this."* · *"Switch to Quiet mode."* · *"Say that again, slower."*

### On-glasses controls
- **Everything reachable by feel** — the two buttons and the swipe bar handle the most-used actions so the phone can stay in your pocket: **left button = Reading**, **right button = push-to-talk**, **swipe bar = volume** (tap to silence the current speech). Assignments are configurable in Settings. See [Glasses Controls](#glasses-controls) for the full mapping.

### Audio & voice
- **Audio routing** — choose where Aware speaks: the glasses' open-ear speakers (default, keeps ears open to the street), paired earbuds, the phone, or an external speaker.
- **Voice control** throughout, with a selectable voice, speaking speed, and reading speed.

### Setup & account
- **Guided onboarding** — pair the smart glasses over Bluetooth and grant three clearly-explained permissions (Bluetooth, Microphone, Location).
- **Accounts** — settings follow the user to any phone; standard sign-up / sign-in.
- **Trial & subscription** — 90-day free trial with an in-app paywall and reminders before billing begins.

### History & privacy
- **History** — a reviewable, filterable log of everything Aware said, tappable to hear again; kept on-device and auto-deleted after 30 days.

### Accessibility (foundational, not a feature toggle)
- Built for low- and no-vision users first: conforms to **WCAG 2.2 Level AAA**, with 7:1 text contrast, ≥ 56 px touch targets, ≥ 17 px body text resizable to 200%, visible focus, never color alone, and full VoiceOver structure — so every function is completable independently by someone with no vision, while remaining usable by sighted caregivers assisting with setup.

## Hardware

Aware runs on the [Mentra Live](https://mentraglass.com/live) camera glasses — a
lightweight, open pair running MentraOS. Aware uses the camera and microphones for
environment analysis and reading, the stereo speakers for open-ear audio, and the
two buttons plus swipe bar for [on-glasses controls](#glasses-controls).

**Frame & design**
- Weight: 43 grams
- Matte black finish
- 162 mm L × 148 mm W × 47 mm H
- Two buttons and a touch swipe bar

**Camera**
- 119° field of view, landscape orientation
- HD 1080p video
- HD 3264 × 2448 images

**Audio**
- Stereo speakers, 3 microphones
- Voice commands and calls

**Battery**
- 260 mAh (glasses), 2,200 mAh (case)
- 12+ hours mixed use
- Charge via Infinity Cable or charging case

**OS & connectivity**
- Runs MentraOS with full app and SDK support
- Wi-Fi + Bluetooth
- Compatible with iOS 15.1+ and Android 12+

## Glasses Controls

The glasses carry the controls you reach for on the move, so the phone can stay in
your pocket. Everything here is operable by feel — no screen required — and the two
button assignments can be swapped in Settings.

### Left button — Reading
- **Press** to start Reading mode: Aware reads whatever you're holding in front of the camera (menu, pamphlet, document, label, package).
- **Framing guidance** — if the whole page isn't in view, Aware tells you which way to move it (*"text continues below, tilt down"* · *"a little to the left"*); if it's too far to resolve, it says *"hold it a few inches closer."*
- **Navigate by voice** while reading — *"skip to desserts,"* *"read the prices,"* *"read that again, slower."*
- **Press again** to stop reading.

### Right button — Push-to-talk (Ask Aware)
- **Hold** the button, ask a question or give a command, then **release** to send. No wake word, and it stays reliable in loud places.
- Ask for anything Aware can do — *"What's around me?"* · *"What bus is this?"* · *"Where did I leave my cane?"* · *"Read this."* · *"Switch to Quiet mode."* · *"Say that again."*

### Swipe bar — Volume & speech
- **Swipe forward / back** to raise / lower the speaking volume; Aware confirms the new level aloud.
- **Tap** to silence whatever Aware is currently saying — a long readout or an alert you've already caught — without turning anything off. Urgent alerts still come through.

## Realtime Alerts

Realtime alerts are Aware's core: the glasses stream the surroundings to a hosted
LLM, which speaks short, actionable alerts back through the glasses' open-ear
speakers. Alerts are grouped into the categories below. Every alert can be turned
on or off and tuned per profile (trigger distance, urgency, sound, phone haptics).

**How alerts are spoken.** Each alert leads with distance or timing, then what it
is, then where, then what to do — shortest useful form first, e.g. *"Curb down two
paces ahead, about 6 inches."* Direction is given plainly (left / right / ahead),
with clock positions used only when fine precision matters (reaching for an object,
a tight gap). Distances are spoken in your chosen units (feet or meters, set in
Settings); stairs are counted in steps. Alerts marked **[urgent]** below use a more
insistent sound and haptic and interrupt lower-priority speech.

### Navigation & Mobility
- **Obstacle in path** — *"Obstacle ahead, about 6 feet — a parked scooter blocking the right side. Bear left."*
- **Stairs going down** *[urgent]* — *"Stairs going down just ahead, about 3 steps. Handrail on both sides."*
- **Stairs going up** — *"Stairs going up, at least 8 steps, starting a few feet ahead. Handrail on your right."*
- **Curb down** — *"Curb down two paces ahead, about 6 inches."*
- **Curb up** — *"Curb up just ahead — one step onto the sidewalk."*
- **Curb ramp** — *"Curb ramp ahead, sloping down toward the crossing."*
- **Uneven / broken surface** — *"Uneven pavement starts here — cracked and rutted for about 20 feet."*
- **Overhead obstacle (head height)** *[urgent]* — *"Low branch at head height straight ahead — duck or step right."*
- **Narrow passage** — *"Path narrows to about shoulder width ahead — wall on your left, railing on your right."*
- **Doorway** — *"Door about 6 feet ahead — pull the handle on the right."*
- **Automatic / revolving door** — *"Sliding doors ahead, opening now."* · *"Revolving door ahead on your right; a regular door is just to its left."*
- **Drop-off / unprotected edge** *[urgent]* — *"Edge ahead — the ground drops about 3 feet, roughly 6 feet in front of you. Stop."*
- **Escalator** — *"Escalator going up on your right, moving — the steps flatten out right in front of you."*
- **Elevator** — *"Elevator ahead, doors open. Call buttons on the wall to your right."*
- **Slope / incline** — *"The path slopes downhill from here."*
- **Path fork** — *"The path splits ahead — left follows the building, right heads toward the street."*
- **Pole / post / hydrant in path** — *"Signpost right in your path, about 4 feet — step left to pass."*
- **Dead end / wall ahead** — *"Wall straight ahead, about 4 feet."*

### Streets & Crossings
- **Approaching crosswalk** — *"Crosswalk ahead, curb in about 6 feet. Signal button on the pole to your right."*
- **Walk signal on** — *"Walk signal is on — you have the light to cross."*
- **Don't-walk / wait** — *"Signal's red — wait here at the curb."*
- **Signal countdown** — *"Walk signal counting down, about 7 seconds left — safer to wait for the next one."*
- **Crossing layout** — *"Two lanes to cross, traffic runs left to right."*
- **Vehicle approaching, slowing** — *"Car coming from your left, slowing to stop."*
- **Vehicle approaching, not slowing** *[urgent]* — *"Car from the right, not slowing down — wait."*
- **Turning vehicle** *[urgent]* — *"A car is turning across the crosswalk from behind you on the left."*
- **Cyclist / e-scooter** *[urgent]* — *"Cyclist passing close on your left."*
- **Traffic island / median** — *"You're at the island — about halfway; the next curb is a few feet ahead."*
- **Driveway crossing** — *"Driveway ahead — watch for cars pulling out on your right."*

### Transit
- **Bus approaching (route visible)** — *"Bus 44 arriving on your left."*
- **Bus route & destination** — *"The bus pulling up is the 8 to Downtown."*
- **Bus doors** — *"Bus doors are just ahead, about 3 feet to your right."*
- **Platform edge** *[urgent]* — *"Platform edge about 3 feet ahead — stay behind the bumpy strip."*
- **Train arriving** — *"Train arriving — the doors will stop right in front of you."*
- **Mind the gap** — *"Mind the gap — about 8 inches between the platform and the train."*
- **Your stop / next stop** — *"Next stop is yours: Pike & 3rd."*
- **Empty seat** — *"Empty seat two steps ahead on your right."*
- **Grab pole / handhold** — *"There's a pole right in front of you to hold."*
- **Rideshare / taxi arrival** — *"A silver sedan just stopped at the curb ahead — plate ends 4-2-9, could be your ride."*

### People & Social
- **Someone approaching** — *"Someone's walking toward you, about 10 feet ahead."*
- **Recognized person (enrolled)** — *"Marcus is coming up on your right."*
- **Handshake offered** *[urgent]* — *"Someone's offering a handshake, right in front of you."*
- **Someone getting your attention** — *"Someone on your left is waving to get your attention."*
- **Line / queue** — *"There's a line here — about four people ahead; the back of the line is a few feet to your right."*
- **Crowd density** — *"It's getting crowded ahead — a dense group of people; you may want to slow down."*
- **Someone close behind** — *"Someone's standing close behind you on your left."*
- **Small child / low person** — *"A small child is right in front of you, about knee height."*
- **Someone pointing / gesturing** — *"The staff member is pointing off to your left."*

### Objects & Belongings
- **Dropped an item** — *"You just dropped something near your right foot — looks like your keys."*
- **Leaving an item behind** — *"Heads up — you're leaving your bag on the chair to your left."*
- **Last known location (on request)** — *"Your cane was last by the table on your right, a few minutes ago."*
- **Reaching for an object** — *"Your coffee cup is at your 1 o'clock, about 8 inches from your hand."*
- **Being handed something** — *"Someone's handing you a receipt, chest height in front."*
- **Empty / clear surface** — *"The chair on your right is empty and clear."*
- **Finding a named object** — *"Your phone is on the counter, about a foot to your left."*

### Signs, Text & Wayfinding
- **Room / unit numbers** — *"Room 214 is the door on your right."*
- **Restroom signs** — *"Men's room on your left, women's on your right, accessible restroom straight ahead."*
- **Exit / entrance** — *"Exit is ahead and to the right."*
- **Storefront / business name** — *"You're passing Café Presse on your right."*
- **Open / closed & hours** — *"The shop on your right is closed — the sign says it opens at 9."*
- **Overhead / directional signage** — *"Overhead sign points to Gate B, straight ahead."*
- **Menus, labels, mail** — on request: say *"read this"* and Aware reads it aloud (see Reading).

### Hazards
- **Wet floor** — *"Wet floor sign ahead — the floor's wet for the next several steps."*
- **Spill** — *"There's a spill on the floor just ahead on your left."*
- **Out of order** — *"This escalator's out of order — the stairs are just to its left."*
- **Construction / blocked path** — *"Caution tape ahead — the walkway's blocked; detour to your right."*
- **Broken glass / debris** — *"Broken glass on the ground ahead — step around it to the left."*
- **Protruding object** — *"A cart handle is sticking out at hip height on your right."*
- **Wet paint** — *"Wet paint on the railing to your right — best not to touch it."*
- **Hot surface** — *"The stovetop in front of you is on."*
- **Smoke / fire / alarm** *[urgent]* — *"A fire alarm is sounding."* · *"Smoke ahead — move back."*

### Animals
- **Animal in path** — *"A dog's lying on the floor right in your path, about 3 feet ahead."*
- **Loose / approaching animal** *[urgent]* — *"A loose dog is coming toward you from the left."*
- **Another service animal** — *"There's another guide dog working, just ahead on your right."*
- **Animal waste** — *"Dog poop on the pavement just ahead on your right."*

### Weather & Terrain
- **Ice** *[urgent]* — *"Icy patch ahead — the pavement looks frozen for the next few steps."*
- **Puddle** — *"Puddle across the path ahead — step right to get around it."*
- **Wet / slippery ground** — *"Ground's wet and slick here."*
- **Snow / slush** — *"Slushy snow underfoot for the next stretch."*
- **Standing / deep water** — *"Deep water ahead across the path — best to find another way."*
- **Wet leaves / mud** — *"Wet leaves ahead — they can be slippery."*

### Custom Alerts
Beyond the built-ins, describe any alert in plain language and Aware evaluates and
runs it (see Features › Custom alerts) — e.g. *"Biscuit picked something up."*

## ML Models

Two models sit in the realtime path: one that looks at the scene and writes the
alert text, and one that turns that text into speech. Everything between them
streams — nothing waits for a complete response before starting the next stage.

### Environment analysis — `google/gemini-2.5-flash-lite`

Served via OpenRouter. Chosen for the combination of latency, vision quality, and
price that this app actually needs:

| | |
|---|---|
| Time to first token | ~440 ms |
| Throughput | ~79 tokens/sec |
| Price | $0.10 / M input, $0.40 / M output |
| Context | 1M tokens |
| Input modalities | text + image + video |

It is the cheapest model in its latency class that is genuinely strong at the two
things alerts depend on: reading small real-world text (route numbers, room
numbers, "wet floor" signage) and spatial grounding (where the curb edge or stair
nosing is relative to the user). It takes video natively, so the glasses can send
a short rolling clip rather than a single frame where motion matters (a vehicle
that is or isn't slowing, an escalator's direction). Five provider routes on
OpenRouter, all at 99%+ uptime.

**Set the thinking budget to 0 on the realtime path.** Flash Lite is a reasoning
model; leaving thinking enabled spends the entire latency budget before the first
token appears.

The custom-alert feasibility check — where the user describes an alert in plain
language and Aware judges whether it can detect it reliably — is *not*
latency-bound and should use a stronger model. Reasoning is worth paying for
there, since the answer sets the user's expectations about their own safety.

*Figures are OpenRouter medians as of July 2026 and drift; re-check before
treating them as a budget.*

### Speech — ElevenLabs Flash v2.5 (`eleven_flash_v2_5`)

~75 ms model inference, 32 languages. Driven over the **multi-context WebSocket**,
not the REST endpoint — text is fed in progressively as Gemini emits it, so synthesis
starts on the first clause instead of waiting for the full alert:

```
wss://api.elevenlabs.io/v1/text-to-speech/{voice_id}/multi-stream-input
  ?model_id=eleven_flash_v2_5
  &auto_mode=true
```

**`auto_mode=true`** disables the chunk schedule and its buffers, so ElevenLabs
generates as soon as a phrase terminates instead of stalling until enough characters
have accumulated. With the scheduler on, a 125-character chunk schedule holding a
50-character alert would sit there waiting for text that is never coming — *"Curb
down two paces ahead"* is the entire utterance. That stall is the whole latency
budget.

The trade is that `auto_mode` expects **complete phrases, not partial words** — it
has no buffer left to assemble them. That is exactly why the pipeline below chunks
Gemini's output on clause boundaries before it reaches the socket rather than
forwarding raw tokens; the two settings only work as a pair.

**One socket per session, one context per utterance.** `multi-stream-input` carries
multiple independent generations — each with its own `context_id` and its own state —
over a single connection, so the socket is opened once when a session starts and
every alert after that is an `InitialiseContext` rather than a fresh WebSocket and
TLS handshake. Aware's speech is bursty and short: a single crossing can produce a
curb, a signal, and a traffic alert within a few seconds. Paying a handshake per
utterance would put connection setup on the hot path repeatedly, and it is the one
cost in the [budget above](#streaming-strategy) that buys nothing.

Contexts also give us the cancel semantics the product already promises:

- **Overlapping alerts** — a new alert opens its own context and plays immediately
  while `CloseContextClient` drops the one it supersedes. No socket teardown, and no
  waiting for the previous utterance to drain. An *[urgent]* alert speaks on-device
  (below) and doesn't need the socket at all, but it still closes whatever cloud
  context is mid-utterance so the two don't talk over each other.
- **Swipe-bar tap to silence** ([controls](#swipe-bar--volume--speech)) — close the
  active context and stop playback; the connection stays warm for whatever comes next.
- **Reading vs. alerts** — a long [Reading](#left-button--reading) readout holds one
  long-lived context while alerts come and go on their own, instead of the two
  fighting over one serialized stream.
- **Quiet stretches** — `KeepContextAlive` resets the inactivity timeout so an idle
  walk doesn't cost a reconnect on the next alert.

Two constraints worth recording. Voice is in the **path**, not the context, so all
contexts on a connection share one voice — a per-profile voice change means a new
socket, not a new context. And this does nothing for the *first* utterance of a
session; that one still pays the handshake, so the socket should be opened when the
glasses connect, not when the first alert fires.

### Streaming strategy

Frame → Gemini → ElevenLabs → speaker, with every hop streaming:

1. Glasses stream to the phone continuously; the phone forwards a short rolling clip
   to the analysis call already in flight.
2. Gemini's output is accumulated to the next clause boundary and flushed to the
   ElevenLabs socket — whole phrases, as required by `auto_mode`, so prosody stays
   natural.
3. Audio chunks play as they return; playback begins before synthesis finishes.

Rough time-to-first-audio budget:

| Stage | Cost |
|---|---|
| Frame → Gemini first token | ~440 ms |
| First clause buffered | ~125 ms |
| Flash v2.5 inference | ~75 ms |
| Network + playback overhead | ~50–100 ms |
| **Total** | **~700–750 ms** |

Waiting for the complete text before calling TTS costs ~1.1 s instead — the
streaming handoff is worth roughly 400 ms, which is the difference between a curb
warning that lands and one that doesn't.

#### Capture — a low-framerate stream, not a photo every second

Continuous video is the single largest draw on the glasses' 260 mAh battery, so the
obvious alternative is to poll `requestPhoto()` about once a second and skip video
entirely. We stream anyway, at a low framerate, for three reasons:

- **1 fps stills can't answer what the alerts ask.** A large share of the catalog is
  about *motion*, not scene contents — is that car slowing or not, which way is the
  escalator running, is the crossing signal counting down, is the bus pulling in or
  pulling out. None of that survives independent frames a second apart, and it is
  exactly why the [model choice](#environment-analysis--googlegemini-25-flash-lite)
  leans on native video input.
- **The photo path is a round-trip, and the budget can't absorb it.**
  `requestPhoto()` captures, JPEG-encodes, and uploads to a webhook, so every frame
  pays a full-resolution readout plus a fresh multipart upload — serialized, before
  analysis starts, on top of the ~700–750 ms above, with jitter we don't control. A
  stream keeps one connection open and lets frames reach a call already in flight.
- **The battery saving is smaller than it looks.** Camera draw is dominated by
  keeping the sensor and ISP awake, which polling doesn't avoid, and inter-frame
  compression means a few fps of H.264 is *fewer* bytes than one full-resolution JPEG
  per second. The camera light is always on for both capture modes, so polling only
  trades a steady LED for a blinking one.

The battery is won by duty-cycling the stream, not by avoiding it:

| Context | Framerate |
| --- | --- |
| Stationary (no motion from the phone's accelerometer) | stream stopped |
| Walking — default | 3–5 fps |
| Street crossing, transit platform edge | burst to 10–15 fps |

**Capture rate and inference rate are decoupled.** The glasses stream at 3–5 fps;
Gemini runs at roughly 1–2 Hz over a rolling ~2 s clip, with near-identical frames
dropped by frame-differencing on the phone before anything is sent. Model spend stays
bounded no matter how fast the camera is running.

**`requestPhoto()` still earns its place** — for [Reading](#left-button--reading) and
face enrolment, where the capture is user-initiated, one-shot, and wants the full
3264 × 2448 for small text rather than a compressed video frame. Pass `sound: false`.

*Open question — outdoor transport.* Video needs Wi-Fi bandwidth, and outdoors the
glasses are not on a network. The SDK's `sendWifiCredentials()` and
`setHotspotState()` point at the intended path: the glasses join the phone's hotspot
and stream to a local WHIP endpoint on the phone, which frame-diffs before spending
tokens. The framerates above and the real drain curve need measuring on hardware
before they're treated as a budget.

**Urgent alerts use on-device TTS.** `AVSpeechSynthesizer` on iOS and
`TextToSpeech` on Android are zero network and zero cost. Outdoors — walking to a
bus stop, crossing a street — the network is the unreliable part, and that is
exactly when an alert marked *[urgent]* cannot fail. Voice quality is irrelevant
for "Stairs going down just ahead"; delivery is everything. On-device is also the
automatic fallback whenever the ElevenLabs socket is slow or dead.

**Pre-synthesize the fixed vocabulary.** A large share of built-in alerts are a
bounded phrase set ("Wet floor sign ahead", "Platform edge", "Curb up just
ahead"). Render those to audio files at build time and play them from disk,
dropping TTS out of the hot path entirely for the alerts that matter most. Only
the variable parts — distances, route numbers, a recognized person's name — need
live synthesis.

## Implementation

### Monorepo (Turborepo)

Everything lives in one [Turborepo](https://turborepo.com) so the app, site, and
API share types and tooling and build/deploy together.

```
aware/
├── apps/
│   ├── mobile   # React Native (Expo) app (the product)
│   ├── web      # Next.js marketing site
│   └── api      # Express.js backend (orchestrates LLM as well)
└── packages/
    ├── core     # shared TypeScript types + Zod schemas (alerts, profiles, API contracts)
    └── config   # shared eslint / tsconfig / prettier
```

Sharing the alert/profile types in `packages/core` means the mobile app, API, and
LLM prompt-builders all agree on one schema — a per-alert tuning object is defined
once and reused everywhere. The mobile app is the only substantial API consumer, so
its typed API client lives inside `apps/mobile` rather than in a shared package;
the marketing site's light account/billing calls go through Next.js server routes
against the same `packages/core` contracts.

### Applications

- **`apps/mobile` — React Native (Expo).** The product. Pairs with the
  [Mentra Live](#hardware) glasses over Bluetooth via
  [`@mentra/bluetooth-sdk`](https://www.npmjs.com/package/@mentra/bluetooth-sdk)
  (see [below](#glasses-connectivity--mentrabluetooth-sdk)), streams the camera/mic
  feed, plays alerts (see the on-device TTS strategy above), and hosts all
  configuration (profiles, per-alert tuning, trusted places, settings). History is
  stored locally.
- **`apps/web` — Next.js.** Marketing site and account/subscription management.
  Served through Cloudflare's CDN.
- **`apps/api` — Express.js.** Auth, settings/profile sync, subscription/billing,
  trusted-place and face-recognition services, and the LLM orchestration layer.

### Glasses connectivity — `@mentra/bluetooth-sdk`

The phone talks to the glasses through
**[`@mentra/bluetooth-sdk`](https://www.npmjs.com/package/@mentra/bluetooth-sdk)**,
Mentra's React Native / Expo SDK for connecting directly to Mentra smart glasses
over Bluetooth. It ships an Expo config plugin plus native Android (`com.mentra:bluetooth-sdk`)
and iOS (`MentraBluetoothSDK`) code, and exposes both an imperative `BluetoothSdk`
object and React hooks under `@mentra/bluetooth-sdk/react`.

It carries the whole device relationship, which is why we don't hand-roll BLE:

- **Pairing** — `scan(DeviceModels.MentraLive, …)` backs the onboarding picker; the
  chosen `Device` is persisted and restored with `setDefaultDevice()` /
  `connectDefault()` so the glasses reconnect silently on later launches.
- **Connection state** — `useMentraBluetooth()` exposes `glasses.connection` as a
  discriminated union (`disconnected` / `scanning` / `connecting` / `bonding` /
  `connected` + `fullyBooted`), which drives the spoken connection status and
  reconnect prompts, plus battery and Wi-Fi state.
- **Controls** — `useBluetoothEvent('button_press' | 'touch_event', …)` delivers the
  two buttons and the swipe bar that power [Glasses Controls](#glasses-controls).
- **Camera** — `startStream({video: {fps}})` / `keepStreamAlive()` (keep-alives ~every
  15s) feeds the realtime alert path, at the duty-cycled framerates set out in
  [Capture](#capture--a-low-framerate-stream-not-a-photo-every-second);
  `requestPhoto()` handles full-resolution one-shots for
  [Reading](#left-button--reading) and face enrolment.
- **Microphone** — `setMicState(true)` plus the `mic_pcm` event gives us raw PCM for
  push-to-talk. We call `setVoiceActivityDetectionEnabled(false)` so glasses-side VAD
  doesn't clip audio destined for our own STT, and `setOwnAppAudioPlaying()` keeps
  playback and capture from fighting.

**Expo, but not Expo Go.** The SDK contains native code, so Expo Go can't load it —
`apps/mobile` runs on Expo development builds (`expo prebuild` → `expo run:ios` /
`expo run:android`) and ships as a standard production native build. That also sets
our floors: Expo 49+, React Native 0.72+, Android minSdk 28, iOS 15.1+ — consistent
with the [hardware](#hardware) compatibility above. The config plugin wires in the
Bluetooth, microphone, and location permissions surfaced during
[onboarding](#setup--account) (Android 12+ needs location permission and Location
services on before BLE scan callbacks arrive).

### Backend & LLM

The Express API brokers every model call through **[OpenRouter](https://openrouter.ai)**,
so we can route each task to the best-fit provider and fail over automatically
without vendor lock-in: a fast vision model on the realtime alert path, a stronger
model for custom-alert feasibility evaluation and reading comprehension. Keeping
provider keys and routing server-side (never on the glasses or phone) also lets us
enforce budgets and rate limits centrally.

Per the **latency principle**, the realtime path is kept as short as possible:
the glasses stream to the API over a persistent connection, the API calls the
vision model and streams spoken output straight back — no database round-trip on
the hot path. Alert *configuration* is loaded once per session and cached (see
below), so deciding *whether* to speak an alert never waits on I/O.

### Data

**Primary store — PostgreSQL** (managed on Railway). Holds everything durable that
must follow the user to any phone:

| Data | Shape | Notes |
| --- | --- | --- |
| Accounts, auth | relational | |
| Subscription & trial state | relational | transactional — billing needs ACID |
| Profiles + per-alert tuning | `JSONB` | flexible, alert-shaped config without a rigid column per setting |
| Custom alerts | `JSONB` | natural-language description + LLM evaluation result |
| Trusted places | geo | geofence via `earthdistance`/PostGIS radius queries |
| Enrolled faces | `pgvector` | embeddings for "recognized person" alerts, similarity search |

One ACID store covers relational, document (`JSONB`), geospatial, and vector
(`pgvector`) needs — so we get transactional integrity for billing *and* flexible
config *and* face-embedding search without operating a second primary database.

**Hot-path & ephemeral — Redis** (managed on Railway). Serves the latency
principle and short-lived state:

- Cached active-profile config for sub-millisecond reads on the alert path
- Device/session state (connection, current profile, audio route)
- Last-known item locations ("where did I leave my cane?")
- Geofence lookups

**On-device — SQLite.** Alert **history** stays on the phone and auto-deletes after
30 days (a privacy guarantee, not just a storage choice), so it needs no server DB.

*Why not MongoDB:* Postgres `JSONB` already gives us the document flexibility the
config needs, while adding the relational integrity billing requires and vector +
geo search in the same engine. A single primary store is simpler to operate and
keeps the data model honest.

### Infrastructure

- **Railway** — hosting for `api` and `web`, plus managed PostgreSQL and Redis.
- **Cloudflare** — DNS for all domains, and CDN/proxy in front of the marketing site.

## Testing & Safety

Aware tells a blind user whether it is safe to take the next step. A wrong or
missing alert at a curb, a platform edge, or a crossing is a physical-injury failure
mode, not a bug report. Treat the codebase accordingly.

**This will plausibly be regulated software.** A product that assists mobility and
warns of hazards sits close to the line for **software as a medical device** —
FDA's device software framework in the US, **EU MDR** Rule 11 in Europe — and the
standards we would then be measured against are **IEC 62304** (medical device
software lifecycle, safety classes A/B/C) and **ISO 14971** (risk management). Under
62304, software whose failure can contribute to serious injury is Class C, which is
where the mobility alert path lands.

We are not claiming any classification or certification today. The point is narrower
and entirely practical: the engineering practices those standards require —
traceability from requirement to test, documented risk controls, evidence that the
safety-relevant code is exercised — are extremely expensive to retrofit onto a
codebase and nearly free to adopt from the first commit. Build as though the
classification is coming.

### Critical paths — 100% branch coverage, enforced

The following modules are **critical paths**. They carry 100% coverage as a merge
gate, and CI fails the build below it — not a warning, not a dashboard:

| Critical path | Why |
| --- | --- |
| Alert decision & gating | Decides whether a hazard is spoken at all |
| Distance, unit & step conversion | A feet/meters or off-by-one error is a physical hazard |
| Urgency ranking & interrupt | Determines what a user hears when alerts collide |
| Per-alert tuning & profile resolution | Wrong resolution silently disables a hazard alert |
| Fallback & degradation logic | Network loss, socket death, glasses disconnect |
| Trusted places / geofencing | Suppresses alerts by location — a suppression bug hides hazards |
| History retention & deletion | The 30-day auto-delete is a stated privacy guarantee |

**Branch coverage, not statement coverage.** Statement coverage is close to
meaningless on this kind of logic: a threshold comparison, an urgency tie-break, or
a profile-precedence rule executes its line under every input while taking only one
of its branches. The number that means something here is whether both sides of every
decision have been exercised.

**Coverage is a floor, not the goal.** 100% branch coverage proves no branch is
*unexercised*; it proves nothing about whether the branch is *correct*. It is the
cheap, automatable half of the job. The other half is deliberate case design —
boundary values at every configured trigger distance, unit-conversion round trips,
collision cases where two alerts fire in the same frame, and every degradation path
enumerated as a test rather than discovered in the field.

**Failure paths get tested first, not last.** The alerts that matter most are the
ones that fire when something is already going wrong: the ElevenLabs socket is dead,
the network dropped mid-crossing, the glasses disconnected, the stream stalled. Those
paths are the least exercised in day-to-day development and the most consequential in
use. Every fallback described in this document — on-device TTS, pre-synthesized
audio, stream restart — needs a test that forces the failure, not a test that assumes
the happy path and hopes.

### Business logic is unit tested, and kept unit testable

Everything that decides *what the user is told* lives in pure, dependency-free
functions in `packages/core` — inputs in, alert decision out, no I/O, no clock, no
network. That is partly a testing convenience and mostly an architectural
requirement: logic entangled with a Bluetooth socket or a live model call cannot be
exhaustively tested, and untestable safety logic is the thing we are specifically
trying not to build.

The shared alert and profile schemas in `packages/core` are what make this
enforceable in one place — the mobile app, the API, and the prompt builders resolve
alerts through the same tested functions rather than each reimplementing the rules.

### The model is evaluated, not unit tested

Coverage does not apply to `gemini-2.5-flash-lite`, and pretending otherwise is the
easiest way to get false confidence. Model behavior is non-deterministic and changes
under us when a provider updates a route. It needs a different instrument:

- **A held-out evaluation set** of real scenes per alert category, with expected
  outcomes, scored on every prompt change and every model or routing change.
- **False negatives weighted above false positives** on the hazard categories. A
  missed stair is not symmetric with a spurious one, and a single aggregate accuracy
  number hides exactly that distinction.
- **Recorded results per version.** Which model, which routing, which prompt, which
  scores — this is the evidence trail a regulator would ask for, and it is also just
  how you find out a provider silently degraded your alert quality.

What *is* unit tested around the model is everything deterministic that surrounds it:
prompt construction, response parsing and schema validation, and the gating that
decides whether a model-produced alert is spoken given the user's profile.

### Traceability

Every alert in the [Realtime Alerts](#realtime-alerts) catalog maps to named tests
covering its trigger threshold, its suppression rules, and its urgency behavior. The
catalog is the requirement list; the mapping from each entry to its tests is the
artifact a 62304 audit asks for, and keeping it current from the start costs a line
per alert. Reconstructing it later means re-deriving intent from code.

Custom alerts inherit this through their feasibility check — the evaluation that
tells a user whether Aware can reliably detect what they described is itself a
safety-relevant decision, since its answer sets what someone believes their glasses
will warn them about.

## Design

Use the claude_design MCP (https://api.anthropic.com/v1/design/mcp, auth via /design-login) to import this project:
https://claude.ai/design/p/261a5c23-790f-4cc1-9231-000d9130e561?file=Aware.dc.html

Focus on these files (the whole project is readable):
- `Aware.dc.html`

Also read these files the selection imports:
- `_ds/broadsheet-9f4982d8-29a2-4336-a9d6-769b234ebb38/_ds_bundle.js`
- `_ds/broadsheet-9f4982d8-29a2-4336-a9d6-769b234ebb38/styles.css`
- `ios-frame.jsx`
- `support.js`