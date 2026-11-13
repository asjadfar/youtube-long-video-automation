---
name: youtube-long-video-automation
description: End-to-end YouTube long-video automation for a nursery-rhyme channel in the "What sound does it make?" format — Claude handles all the work end to end (niche/trend check, 18-30-scene script for a 3-5 minute video, Flow-ready visual-only prompts, voiceover script, ffmpeg stitch to 1280x720 horizontal, thumbnail, title/description/hashtags, upload checklist with approval gate, and analytics review), with the owner involved only for approval at the upload step and for channel/Google account setup. Includes a monetization plan for the YouTube Partner Program (1,000 subscribers + 4,000 public watch hours) with a progress tracker. Use when the user asks to make, plan, edit, or upload a YouTube video, especially a nursery-rhyme / kids' guessing-format video.
---

# YouTube Long-Video Automation

## When to use

Use this skill when the user asks to make a YouTube long-form video from idea to upload — especially a nursery-rhyme video in the "What sound does it make?" interactive guessing format — or asks for a script, video prompts, a thumbnail, titles/descriptions, or an upload for such a video.

Do not use it for live streams, or for any platform other than YouTube long-form videos, unless the user explicitly asks to adapt it.

## Who does what — Claude handles all the work end to end

Claude runs every step of the workflow below — niche/trend check, script, video prompts, voiceover, edit/stitch, thumbnail, title/description/hashtags, upload checklist, analytics review, and the monetization tracker. The owner is involved only at two points:

1. **Channel / Google account setup** — the owner picks the Google account, creates the channel, chooses its name/handle, and completes any Google sign-in or OAuth consent on their own device. Claude cannot do these for the owner.
2. **Approval at the upload step** — the owner approves the exact final video, title, description, hashtags and thumbnail before anything is uploaded (see Step 8). Nothing is published without that approval.

Two device-bound exceptions, stated honestly so the "end to end" claim is not overstated:

- **Video clips:** Claude writes the Flow-ready visual prompts, but the clips themselves are generated in Google Flow by the owner, because video generation is region-unavailable on the owner's Muse account (see Hard limits). Claude then stitches the finished clips with ffmpeg.
- **Upload sign-in:** the Google sign-in / OAuth for the upload happens on the owner's own device (browser route) or through OAuth the owner set up. Claude never handles the owner's password or tokens.

Everything else — research, writing, prompts, voiceover script, stitching, thumbnail guidance, titles, descriptions, hashtags, checklist, analytics review, tracker updates — is Claude's work. Do not hand any of it back to the owner as homework.

## Channel facts (do not invent others)

- Channel does NOT exist yet. Google account and channel name/handle are still to be chosen. Suggested names: Bunny Sounds, What Sound Is That?, Little Bunny Tunes, Tiny Sounds Club.
- Format: "What sound does it make?" — 18-30 scenes x ~10 seconds, 3-5 minutes total, bunny host, animals / vehicles / instruments, 2-second pause before revealing each sound, seamless-loop finale.
- Ratio: 16:9 horizontal landscape, 1280x720, for YouTube long-form videos.
- Style: soft 2D storybook cartoon — warm sunlight, painterly backgrounds, big expressive eyes, gentle soft colors. Dialogue brief and simple.

## Hard limits — state them honestly, do not work around them

- **No direct YouTube connector.** There is no built-in YouTube connection. Upload is only via (A) the browser in YouTube Studio with the owner's Google sign-in and approval, or (B) the YouTube Data API v3 with OAuth the owner sets up. Never claim direct auto-upload without one of those.
- **Video generation is region-unavailable on the owner's Muse account.** Do not promise Muse/Claude can generate the video clips itself. Clips come from Google Flow (made by the owner) or another video tool the owner chooses, then are stitched with ffmpeg.
- **Google Flow blocks children speaking / dialogue.** Every visual prompt below is visual-only for that reason. Never put spoken dialogue in a Flow / image / video prompt. Dialogue lives only in the separate voiceover script.
- **No credentials in the skill.** Never put an API key, password, OAuth token or secret in a skill file, in chat, or in the repo. Logins happen on the owner's own device.
- **Approval gate is mandatory.** Nothing is published or uploaded until the owner approves the exact final video, title, description, hashtags and thumbnail. A changed caption, clip order or thumbnail needs fresh approval.
- **One speaker per voiceover line.** Each line is spoken by one character only.

## Workflow

### Step 1 — Niche / trend check

1. Confirm the episode topic fits the channel: animals, vehicles, or instruments a young child knows.
2. Check what is trending in the target audience (USA) right now — search the web / news for the topic, do not guess from training data.
3. Keep the topic evergreen if no trend fits: a cow, lion, car and drum will work any week; a fad will not.
4. Pick 16-28 guessing items for the episode (one per middle scene), plus the bunny host and the finale, to reach 3-5 minutes total. Group them into rounds to keep the video varied, for example Round 1: Animals, Round 2: Vehicles, Round 3: Instruments, then a mixed final round. Do not use fewer than 16 items — the video must be 3-5 minutes long, not 1 minute.

### Step 2 — Script (18-30-scene "What sound" format, 3-5 minutes)

Write the script using `templates/episode-script.md`. Keep every line brief and simple. Structure:

| Scene | Time | What happens | Visual | Voiceover / sound |
|---|---|---|---|---|
| 1 — Hook | 0:00–0:10 | Bunny host appears and asks the question | Bunny in a sunny meadow, waving | "What sound does it make? Let's guess!" |
| 2 — Item 1 | 0:10–0:20 | First animal / vehicle / instrument appears, 2-second pause, then its sound | Item in a storybook setting, no text on screen | "[Item] says… MOO!" |
| 3 — Item 2 | 0:20–0:30 | Same guessing beat | Item in a storybook setting | "[Item] says… ROAR!" |
| 4 — Item 3 | 0:30–0:40 | Same guessing beat | Item in a storybook setting | "[Item] says… BEEP BEEP!" |
| 5 — Item 4 | 0:40–0:50 | Same guessing beat | Item in a storybook setting | "[Item] says… BOOM BOOM!" |
| 6–17 — Items 5–16 | 0:50–2:50 | Repeat the same guessing beat, one item per scene, in rounds | One item per scene, storybook setting | "[Item] says… [SOUND]!" each time |
| 18 — Finale (3-minute version) | 2:50–3:00 | All items parade together, loop back to the hook | All characters together, sunny, joyful | "You guessed them all! Again!" (loops to scene 1) |
| 18–29 — Items 17–28 (for a 5-minute version) | 2:50–4:50 | More guessing rounds, same beat, one item per scene | One item per scene, storybook setting | "[Item] says… [SOUND]!" each time |
| 30 — Finale (5-minute version) | 4:50–5:00 | All items parade together, loop back to the hook | All characters together, sunny, joyful | "You guessed them all! Again!" (loops to scene 1) |

Count the scenes before generating anything: hook (1) + guessing items (16-28) + finale (1) = 18-30 scenes at ~10 seconds each = 3-5 minutes total. A 3-minute episode has 18 scenes; a 5-minute episode has 30 scenes. Never deliver a 6-scene / 1-minute episode — that is too brief.

Rules:
- One guessing item per scene. No scene teaches two sounds.
- A 2-second silent pause before each sound reveal, so the child can guess.
- No dialogue in the visual prompt — only in the voiceover column.
- The finale must loop seamlessly back to the hook, so the video replays cleanly.

#### Example — Episode 1 (the reference episode, 3-minute version, 18 scenes)

- Scene 1 — Bunny host in a sunny meadow: "What sound does it make? Let's guess!"
- Scene 2 — Cow in a green field, 2-second pause: "Cow says… MOO!"
- Scene 3 — Lion in warm sunlight, 2-second pause: "Lion says… ROAR!"
- Scene 4 — Red car on a road, 2-second pause: "Car says… BEEP BEEP!"
- Scene 5 — Drum in a music corner, 2-second pause: "Drum says… BOOM BOOM!"
- Scene 6 — Dog in a garden: "Dog says… WOOF!"
- Scene 7 — Cat on a windowsill: "Cat says… MEOW!"
- Scene 8 — Duck in a pond: "Duck says… QUACK!"
- Scene 9 — Elephant in the savanna: "Elephant says… TRUMPET!"
- Scene 10 — Horse in a field: "Horse says… NEIGH!"
- Scene 11 — Frog on a lily pad: "Frog says… RIBBIT!"
- Scene 12 — Sheep in a meadow: "Sheep says… BAA!"
- Scene 13 — Train on a track: "Train says… CHOO CHOO!"
- Scene 14 — Bus on a street: "Bus says… BEEP!"
- Scene 15 — Airplane in the sky: "Plane says… WHEEE!"
- Scene 16 — Guitar in a music room: "Guitar says… STRUM!"
- Scene 17 — Piano in a music room: "Piano says… PLINK PLINK!"
- Scene 18 — Bunny, cow, lion, car, drum and all the animals, vehicles and instruments parade together: "You guessed them all! Again!"

For a 5-minute version, add 12 more guessing scenes (items 17-28) in the same beat before the finale, for example more animals, vehicles and instruments, keeping one item per scene.

#### Blank template

Use `templates/episode-script.md` for every new episode. Fill in all 16-28 items, the setting for each, and the exact sound word for each before generating any visuals.

### Step 3 — Image / video prompts (Flow-ready, visual-only)

Write one prompt per scene. Every prompt must:

- Start with the style lock: "Soft 2D storybook cartoon, warm sunlight, painterly backgrounds, big expressive eyes, gentle soft colors, 16:9 horizontal landscape, 1280x720."
- Describe only what is seen: character, setting, action, expression, colours. No spoken words, no dialogue, no children speaking, no text on screen.
- Keep the bunny host and each item visually consistent across scenes — same colours, same character design, same setting style. Copy the character description word for word into each prompt.
- Keep each clip ~10 seconds. If the tool makes clips under 10 seconds, note the actual length and adjust the stitch step. Count the clips: 18 clips for 3 minutes, 30 clips for 5 minutes.

Example prompt (Scene 2, cow):
> Soft 2D storybook cartoon, warm sunlight, painterly backgrounds, big expressive eyes, gentle soft colors, 16:9 horizontal landscape, 1280x720. A friendly black-and-white cow standing in a sunny green meadow with flowers, looking at the camera with a happy expression, tail swishing, soft clouds in a blue sky. No text, no dialogue, no speaking.

Example prompt (Scene 1, bunny host):
> Soft 2D storybook cartoon, warm sunlight, painterly backgrounds, big expressive eyes, gentle soft colors, 16:9 horizontal landscape, 1280x720. A cute white bunny with long ears and a small blue bow, standing in a sunny meadow, waving one paw in greeting, flowers around, warm morning light. No text, no dialogue, no speaking.

Check each generated frame before using it: character on-model, no extra limbs, no text burned in, 16:9 ratio. Name errors plainly and regenerate the bad scene — do not ship it.

### Step 4 — Voiceover script

Write the voiceover separately from the visuals, one line per scene, one speaker per line. Follow the same pattern for every guessing scene:

- Scene 1: "What sound does it make? Let's guess!"
- Scene 2: "Cow says… MOO!"
- Scene 3: "Lion says… ROAR!"
- Scene 4: "Car says… BEEP BEEP!"
- Scene 5: "Drum says… BOOM BOOM!"
- Scenes 6–17 (3-minute version) or 6–29 (5-minute version): "[Item] says… [SOUND]!" — one line per item, in scene order.
- Final scene: "You guessed them all! Again!"

Keep it in the episode script file, in the voiceover column. The voiceover is recorded / generated as audio and laid over the stitched video — it is never part of the visual prompt. If lip-sync is attempted, sync only the speaking character and only on their own line; if it misattributes, fall back to plain voiceover with no lip-sync.

### Step 5 — Edit / stitch with ffmpeg

Join the scene clips into one horizontal video with `scripts/stitch.sh`. Requirements:

- Output: one file, 16:9 horizontal landscape, 1280x720, 3-5 minutes total.
- Verify the output dimensions with `ffprobe` after stitching; if the tool delivered another ratio, scale / pad to 1280x720 before uploading.
- Keep the scene order exactly as scripted. If a clip is under 10 seconds, do not stretch it silently — note the real total length and adjust the voiceover timing to match. The finished video must still be 3-5 minutes long.
- Keep the finished file and the scene clips together so the episode can be re-cut later.

See `scripts/stitch.sh` for the exact command and usage.

### Step 6 — Thumbnail (1280x720)

- Size: 1280x720. Use the bunny host plus one item, big and readable at small size.
- One brief hook on the thumbnail at most (for example "What sound?"), large bold text, high contrast. No more than 4 words.
- Same storybook style as the video. Do not use a frame with burned-in text or a dialogue bubble.
- Show the thumbnail to the owner with the title before upload — it is part of the approval gate.

### Step 7 — Title / description / hashtags

Use this template every time. Do not change the structure without the owner's approval.

**Title template:**
`What Sound Does It Make? 🐰 Cow, Lion, Car & Drum | Fun Guessing Game for Kids`

Replace the item list with the episode's items. Keep it under 100 characters including the emoji.

**Description template:**
```
What sound does it make? 🐰
Guess the sound with Bunny! Cow, Lion, Car and Drum — can you guess them all?

Watch, listen and guess along — perfect for toddlers and preschool kids.

#KidsVideos #KidsSongs #NurseryRhymes
```

Replace the item list with the episode's items. Add the channel name once the channel exists.

**Hashtags (use 3–5, no more):**
`#KidsVideos #KidsSongs #NurseryRhymes #WhatSound #LearnWithBunny`

Keep hashtags in the description, not in the title.

### Step 8 — Upload checklist + approval gate

Complete `templates/upload-checklist.md` for the episode. Then stop and get the owner's approval for the exact final video file, title, description, hashtags and thumbnail.

Upload only after approval, via one of the two routes in the README:

- **Route A — Browser / YouTube Studio:** owner signs in with Google on their own device and uploads, or approves a browser upload. Verify the uploaded video plays, is horizontal, and shows the right title/description.
- **Route B — YouTube Data API with OAuth:** only if the owner has set up OAuth. Never paste credentials into the skill or chat.

After upload, return the public link (or the scheduled time with its timezone) to the owner. A draft saved in Studio, a scheduled video and a live video are different states — report which one it is.

### Step 9 — Analytics follow-up

24–48 hours after publishing, check and record:

- Views, average view duration / retention, likes, comments, new subscribers from the video.
- Which guessing item held attention best (if retention data shows a drop, name the scene).
- What to change next time: one change only (for example opening line, item order, or thumbnail), so the result shows what made the difference.

Do not chase a single video's numbers by re-uploading the same video. Note the lesson in the next episode's script file instead.

## Monetization — YouTube Partner Program (long-form videos)

### The goal

Qualify for the YouTube Partner Program (YPP) for long-form videos, then set up AdSense to earn from ads. The thresholds are:

- **1,000 subscribers**, and
- **4,000 public watch hours in the last 12 months**.

Only after BOTH thresholds are met can the channel apply for YPP. After acceptance, connect AdSense (the owner does this on their own device, with their own payment details) and ads can run on the videos.

### Be honest about this — do not overpromise

- **Monetization is NOT instant.** No money is earned before the thresholds are met and the application is accepted. Early episodes earn $0.
- **Claude cannot fake views or subscribers.** Do not buy views, buy subscribers, use view bots, or use any trick to inflate the numbers — that can get the channel rejected from YPP or removed. Growth comes only from real viewers watching real videos.
- **No views or subscribers are guaranteed.** The plan below improves the odds; it does not promise a number or a date. If growth is slow, the answer is better retention and more consistent episodes, not shortcuts.

### The realistic plan to reach 1,000 subscribers + 4,000 watch hours

1. **Consistent 3-5 minute episodes.** Publish on a fixed schedule the owner can sustain — for example 2 episodes per week on the same days — and do not miss weeks. Every episode is 3-5 minutes long, so each full view adds 3-5 minutes of watch time.
2. **Retention hooks in every episode.**
   - A question in the first 10 seconds ("What sound does it make? Let's guess!") so the viewer stays to find out.
   - A new sound every ~10 seconds, so there is always a reason to keep watching.
   - A finale parade that loops back to the hook, so the video replays and adds watch time.
3. **Series and playlists.** Keep every episode in the same "What Sound Does It Make?" series, with the same bunny host, same style and same title pattern, so one video leads viewers to the next. Put episodes into a playlist ("What Sound Does It Make? — Full Series") and link the playlist in every description.
4. **SEO titles and descriptions.** Use the Step 7 template every time: the question + the item names in the title, the same items in the first two lines of the description, and 3-5 relevant hashtags. Titles and descriptions must match what is actually in the video — no clickbait that makes viewers leave early, because early exits hurt retention and watch hours.
5. **Upload schedule.** Agree the schedule with the owner before the first episode (for example Tuesdays and Fridays), publish at a consistent time, and keep it. If the schedule changes, update it in the tracker file, do not just skip silently.
6. **Progress tracker.** After every upload, Claude updates `templates/monetization-tracker.md` with the current subscriber count and public watch hours (last 12 months) from YouTube Studio / Analytics, the gap left to each threshold, and the episodes published so far. The owner reads the numbers from Studio; Claude records them. Review the tracker after each episode and say plainly how far is left — never round the gap away.

### What happens after qualifying

1. Apply for YPP in YouTube Studio when both thresholds are met.
2. The owner sets up AdSense on their own device with their own payment details.
3. Once accepted, turn ads on for the long-form videos and keep publishing — earnings come from real watch time, so retention stays the priority even after monetization starts.
4. Keep the tracker going after monetization: record monthly watch hours and estimated revenue from Analytics, and note which episodes earned the most watch time.
