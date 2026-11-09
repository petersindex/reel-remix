# Reel Remix

5 Claude skills that turn reels you like into one in your brand: find, break down, rebrand, storyboard, build.

Paste the links of reels you love. Claude ranks them, breaks down how the best one works frame by frame, swaps their look for yours, writes your storyboard, then builds and renders the video in code. Inspired by them, not a copy.

| Skill | Job | Output |
|---|---|---|
| **High Roller** | Find: ranks reels by how hard they pull comments | `RANK.md` |
| **Detective** | Break down: every cut, caption, motion and hook, frame by frame | `breakdown/<id>.md` |
| **Brand Cop** | Rebrand: your colours, fonts, host and voice replace theirs | `brand.md`, `TICKET.md` |
| **Director** | Storyboard: your script, every line paired with a picture | `STORYBOARD.md` |
| **Editor** | Build: the video in code, rendered and checked against the plan | `your-reel.mp4` |

## What you need

- **Claude Code** (the Code tab in the Claude desktop app, or the CLI) on a Pro or Max plan. It needs to run commands on your computer, which plain chat can't do.
- **Free tools:** Node.js 22+, FFmpeg and yt-dlp. On a Mac: `brew install node ffmpeg yt-dlp`. On Windows: `winget install OpenJS.NodeJS.LTS Gyan.FFmpeg yt-dlp.yt-dlp`. The first run checks these for you.
- **2 to 5 reel links** you want to learn from.
- **Your brand:** colours, fonts, and what goes on screen (your face-cam, a cut-out, a character, or just screen recordings). The Brand Cop asks for anything missing, once.
- **Your voice:** a voice memo, or a free built-in TTS voice.

Everything runs on your computer. No API keys, nothing to pay beyond your Claude plan.

## Install

In Claude Code:

```
/plugin marketplace add petersindex/reel-remix
/plugin install reel-remix@reel-remix
```

## Use

```
Remix these reels: <link> <link>
My reel is about <your topic>. Call to action: comment <KEYWORD>.
```

Claude stops twice for your go: once on the script and storyboard, once on the key frames before it animates. You can also run one agent on its own, for example "break down this reel: <link>".

## Inspired, not a copy

The remix keeps the structure, pacing and devices of the reels you pick, and rebuilds everything else with your own words, face, look, voice and music. No line of their script, frame of their footage or piece of their audio ends up in yours. The rules are in [`reference/not-a-copy.md`](reference/not-a-copy.md).

## Status

v0.1. Built on macOS. The find and break-down steps are tested on real Instagram reels. Instagram does not expose view counts this way, so ranking uses comments, likes and post date. A private or rate-limited reel may need your browser's Instagram session (the skill asks first).

## Built on

- [HyperFrames](https://github.com/heygen-com/hyperframes) (Apache-2.0): measuring, transcribing, building and rendering video from HTML.
- [yt-dlp](https://github.com/yt-dlp/yt-dlp): reading and downloading public reels.
- Optional: [rea-video](https://github.com/JuneYaooo/rea-video) (Apache-2.0) for a deeper per-shot analysis.

MIT licence. Made by [@petersindex](https://github.com/petersindex).
