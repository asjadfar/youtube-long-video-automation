# YouTube Long-Video Automation Skill

A Claude skill for end-to-end YouTube long-video automation, built for Asjad's nursery-rhyme channel. Claude handles all the work end to end — niche, script, video prompts, voiceover, edit/stitch, thumbnail, title/description/hashtags, upload checklist and analytics review — with the owner involved only for approval at the upload step and for channel/Google account setup. It also includes a monetization plan for the YouTube Partner Program (1,000 subscribers + 4,000 public watch hours) with a progress tracker.

## What it does

Takes a video from niche to upload in one repeatable workflow:

1. **Niche / trend check** — confirm the topic fits the channel and is trending in the target audience (USA).
2. **Script** — an 18-30-scene, 3-5-minute "What sound does it make?" episode, 16:9 horizontal landscape, 1280x720.
3. **Visuals** — Flow-ready, visual-only image/video prompts (no children speaking or dialogue in the prompt).
4. **Voiceover** — a separate brief, simple voiceover script, recorded / generated apart from the visuals.
5. **Edit / stitch** — ffmpeg joins the scene clips into one 1280x720 horizontal video.
6. **Thumbnail** — 1280x720 guidance for a clear, readable video thumbnail.
7. **Title / description / hashtags** — a fixed template so every upload is consistent.
8. **Upload** — checklist + approval gate. Nothing uploads without the owner's approval.
9. **Analytics follow-up** — what to check after publishing, and what to change next time.
10. **Monetization** — a realistic plan to reach the YouTube Partner Program (1,000 subscribers + 4,000 public watch hours in the last 12 months, then AdSense), with a progress tracker Claude updates after every upload. Monetization is NOT instant, Claude cannot fake views or subscribers, and no views or subscribers are guaranteed — see the Monetization section in `SKILL.md`.

## Who does what — Claude handles all the work end to end

Claude runs every step — niche, script, video prompts, voiceover, edit/stitch, thumbnail, title/description/hashtags, upload checklist, analytics review and the monetization tracker. The owner is involved only at two points: (1) channel / Google account setup (pick the Google account, create the channel, choose name/handle, complete any Google sign-in or OAuth on their own device), and (2) approval of the exact final video, title, description, hashtags and thumbnail before upload. The two device-bound exceptions are the video clips (Claude writes the Flow-ready prompts; the owner generates the clips in Flow, because video generation is region-unavailable on the owner's Muse account) and the upload sign-in itself (on the owner's own device). Everything else is Claude's work — do not hand it back to the owner as homework.

## The channel

- **Channel:** Bunny Sounds
- **Handle:** @BunnySoundsKids (https://www.youtube.com/@BunnySoundsKids)
- **Google account:** asjadfarooqch@gmail.com
- **Location:** United States
- **Language:** English
- **Created:** Nov 13, 2026
- **Format:** "What sound does it make?" — interactive guessing format. 18-30 scenes x ~10 seconds, 3-5 minutes total, bunny host, animals / vehicles / instruments, a 2-second pause before revealing each sound, seamless-loop finale.
- **Ratio:** 16:9 horizontal landscape, 1280x720, for YouTube long-form videos.
- **Style:** soft 2D storybook cartoon — warm sunlight, painterly backgrounds, big expressive eyes, gentle soft colors. Dialogue brief and simple.

## Files

```
youtube-automation-skill/
├── README.md                                  # this file
└── youtube-long-video-automation/
    ├── SKILL.md                               # the Claude skill — the workflow itself
    ├── scripts/
    │   └── stitch.sh                          # ffmpeg: concat scene clips into one 1280x720 video
    └── templates/
        ├── episode-script.md                  # blank episode script template
        └── upload-checklist.md                # pre-upload checklist + approval gate
        └── monetization-tracker.md            # YPP progress tracker (subs + watch hours)
```

## Setup

### 1. Create the YouTube channel first

Pick a Google account, then create the channel and choose its name and handle. The skill cannot create the channel for you, and it cannot pick the Google account — that is the owner's decision.

### 2. Choose an upload route (one of these)

**Route A — Browser upload (recommended to start).** Upload in the browser with the owner's Google sign-in and approval. The agent prepares the finished video file, title, description, hashtags and thumbnail, and the owner uploads (or approves the browser upload) in YouTube Studio. No API key needed.

**Route B — YouTube Data API with OAuth.** Set up a Google Cloud project, enable the YouTube Data API v3, create OAuth credentials, and complete the consent flow on the owner's own device. The skill then follows the API upload steps. This is more setup, and it is the only route that lets an agent upload without the browser.

Do not use any other upload route. Do not paste API keys, passwords or credentials into the skill files, into chat, or into the repo — credentials live only in the owner's secure storage / OAuth flow.

### 3. Video clips

Clips come from Google Flow (or another video tool the owner chooses). The skill's prompts are visual-only on purpose: Flow blocks children speaking / dialogue prompts, so dialogue is never in the visual prompt — it goes in the separate voiceover script instead.

### 4. Use in Claude

Copy the `youtube-long-video-automation/` folder into a Claude skills directory (for example a Claude Code skills folder, or a repo Claude is pointed at), or keep this whole repo and point Claude at `youtube-long-video-automation/SKILL.md`. Then ask Claude to run the workflow, for example: "Make Episode 2 of the What Sound channel using the youtube-long-video-automation skill."

## Honest limits — read before using

- **No direct YouTube connector.** Claude does not have a built-in YouTube connection like it does for some other apps. Upload is browser (owner's sign-in + approval) or YouTube Data API with OAuth the owner sets up. Never claim direct auto-upload without one of those.
- **Video generation is region-unavailable on the owner's Muse account.** The skill does not promise that Muse/Claude can generate video clips itself. Clips are made in Flow (by the owner) or another tool, then stitched by ffmpeg.
- **Google Flow blocks children speaking / dialogue.** All visual prompts in this skill are visual-only for that reason. Dialogue lives only in the voiceover script.
- **No credentials in the skill.** No API keys, passwords, OAuth tokens or secrets are stored in these files. If a step needs a login, the owner does it on their own device.
- **Approval gate is mandatory.** No video, title, description or thumbnail is published or uploaded until the owner approves the exact final version. A changed caption, clip order or thumbnail needs fresh approval.
- **One speaker per line in voiceover.** Each line is spoken by one character only; do not put two speakers in one voiceover line.

## How to run one episode

1. Pick the episode topic (animal / vehicle / instrument set).
2. Fill in `templates/episode-script.md`.
3. Generate the 18-30 scene visuals from the prompts in `SKILL.md` (Flow-ready, visual-only).
4. Record / generate the voiceover from the voiceover script.
5. Run `scripts/stitch.sh` to join the clips into one 1280x720 video.
6. Make the thumbnail (1280x720).
7. Fill in `templates/upload-checklist.md` and get the owner's approval.
8. Upload via Route A or Route B.
9. Check analytics after 24–48 hours and note what to change next time.
