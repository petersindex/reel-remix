---
name: editor
description: Build and render an approved reel storyboard as a 1080x1920 video in code with HyperFrames, then check it against the plan. Use when a STORYBOARD.md is approved and the person wants the video made, or as step 5 of a remix.
---

# The Editor: build

Builds the approved `STORYBOARD.md` in code with HyperFrames (HTML rendered to MP4, free and local). HyperFrames' own `hyperframes` skill owns the composition rules; this skill owns the order of work and the checks against the plan. The approved storyboard is the brief: skip HyperFrames' intent interview, `BRIEF.md` and its storyboard file. Layout: `../../reference/project-layout.md`.

## Steps

1. **Scaffold.** In `remix/<slug>/`: `npx hyperframes init video --resolution portrait --non-interactive`. Load the `hyperframes` skill before writing any HTML; if it is not listed in this session, read `~/.claude/skills/hyperframes/SKILL.md` and follow it. Init may say to restart the agent to load skills; carry on in this session.
2. **Bring the brand in.** Copy every file named in `remix/brand.md` (fonts, logo, host footage or cut-outs, character art) into `video/assets/`. A font given only by name is a Google Font: download its file from the family's folder under `ofl/` in `github.com/google/fonts` into `video/assets/fonts/` and declare it with `@font-face`, since HyperFrames rejects a font without one. Set the palette and fonts from `brand.md` and `TICKET.md`; nothing from the reference's look survives.
3. **Voice first, it is the clock.**
   - Face-cam host: the footage carries the voice. Copy it to `video/assets/host.mp4` and transcribe that file. To stand the person on the brand ground instead of their room: `npx hyperframes remove-background video/assets/host.mp4 -o video/assets/host-cutout.webm`, and play the cut-out muted over a separate `<audio>` of the original.
   - The person's own voice memo: put it at `video/assets/vo.wav` (any format FFmpeg reads).
   - TTS: write the script to `video/assets/script.txt`, then `npx hyperframes tts video/assets/script.txt -v <voice> -s 1.0 -o video/assets/vo.wav` (`--list` shows voices; `-s` below 1 slows it down).

   Then `npx hyperframes transcribe video/assets/vo.wav --dir video --json > video/transcribe.log` for every word's time. Retime every shot so its chip lands on the word that says it; the storyboard's times were estimates. Clamp the last word's end to the audio's length.
4. **Pose key frames (gate two).** Build the composition with every shot posed at its key moment, then `npx hyperframes snapshot video --at <each shot's key time>` and show the person the contact sheet it writes (`contactSheets` in its JSON): one sheet, not one image per shot. Stop and wait for their go. Notes change only the shots they name.
5. **Animate.** Build the motion from the Detective's notes (entrances, swaps, punch-ins, with their frame counts) and the On screen column. A character acts with what exists: hops, squash and stretch, turning, carrying and moving props. New poses need new art; list any that are missing instead of faking them.
6. **Check.**
   - `npx hyperframes check video --json`: fix every error, and weigh every warning.
   - Snapshot every shot's key time again and compare each with its approved frame and its storyboard row: right chip, right picture, right host.
   - `npx hyperframes snapshot video --range <start>,<end> --frames 8` around every transition: text, colour and keys break mid-move where key frames look fine.
   - Hold every frame to `../../reference/safe-zones.md`: words in the safe zones, the picture filling the frame, blocks 40 px apart, each hero at least 760 px wide or 40% of the height.

   Fix and re-snapshot until every row matches.
7. **Preview.** `npx hyperframes preview video --background`, tell the person they can look and edit there, then `npx hyperframes preview video --stop` before rendering.
8. **Render.** `npx hyperframes render video --quality delivery --output <slug>-raw.mp4`.
9. **Loudness.** Normalise the render to -14 LUFS for social with FFmpeg's two-pass `loudnorm`. Measure with `ffmpeg -i <slug>-raw.mp4 -af loudnorm=I=-14:TP=-1.5:LRA=11:print_format=json -f null -`, then pass its `input_i`, `input_tp`, `input_lra`, `input_thresh` and `target_offset` back as `measured_I`, `measured_TP`, `measured_LRA`, `measured_thresh` and `offset` with `linear=true`, copying the video stream (`-c:v copy -c:a aac -b:a 256k -movflags +faststart`) into `<slug>.mp4`.
10. **Verify the file.**
    - `npx hyperframes audio <slug>.mp4 --json`: sound present, -16 to -14 LUFS integrated, true peak at or under -1 dB.
    - Pacing: when the reference is cut-based, compare `npx hyperframes measure cuts <slug>.mp4` per minute with its `cuts.json`; when it is one continuous canvas, compare how often the chips change instead.
    - Run the transcript overlap check from `../../reference/not-a-copy.md` on the final script.

Done when `check` passes, every storyboard row matches its frame, the file is normalised, and the verification numbers are reported. Say plainly that sound was measured, not heard.
