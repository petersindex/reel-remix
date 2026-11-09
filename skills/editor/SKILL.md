---
name: editor
description: Build and render an approved reel storyboard as a 1080x1920 video in code with HyperFrames, then check it against the plan. Use when a STORYBOARD.md is approved and the person wants the video made, or as step 5 of a remix.
---

# The Editor: build

Builds the approved `STORYBOARD.md` cut for cut, in code, with HyperFrames (HTML rendered to MP4, free and local). HyperFrames' own `hyperframes` skill owns the composition rules; this skill owns the order of work and the checks against the plan. Layout: `../../reference/project-layout.md`.

## Steps

1. **Scaffold.** In `remix/<slug>/`: `npx hyperframes init video --resolution portrait --non-interactive`. Init also installs the HyperFrames skills. Load the `hyperframes` skill before writing any HTML; if it is not listed in this session yet, read `~/.claude/skills/hyperframes/SKILL.md` and follow it.
2. **Bring the brand in.** Copy every file named in `remix/brand.md` (fonts, logo, host footage or cut-outs, character art) into `video/assets/`. Set the palette and fonts from `brand.md` and `TICKET.md`; nothing from the reference's look survives.
3. **Voice first, it is the clock.**
   - Face-cam host: the footage carries the voice. Copy it to `video/assets/host.mp4` and transcribe that file instead of a `vo.wav`. To stand the person on the brand ground instead of their room, cut them out: `npx hyperframes remove-background video/assets/host.mp4 -o video/assets/host-cutout.webm`, and play the cut-out muted over a separate `<audio>` of the original.
   - The person's own voice memo: put it at `video/assets/vo.wav` (any format FFmpeg reads).
   - TTS: write the script to `video/assets/script.txt`, then `npx hyperframes tts video/assets/script.txt -v <voice> -o video/assets/vo.wav` (`npx hyperframes tts --list` shows the voices).

   Then `npx hyperframes transcribe video/assets/vo.wav --dir video --json` for every word's time, and retime each shot so its chip lands on the word that says it.
4. **Pose stills (gate two).** Pose each storyboard shot at its key moment and put them on a board for approval, following the storyboard recipe in the `hyperframes` skill. Stop and wait for the person's go. Notes change only the frames they name.
5. **Animate.** Build the motion from the Detective's notes (entrances, swaps, punch-ins, with their frame counts) and the On screen column. A character acts with what exists: hops, squash and stretch, turning, carrying and moving props. New poses need new art; list any that are missing instead of faking them.
6. **Check.** `npx hyperframes check video --json`: fix every error, and weigh every warning. Then `npx hyperframes snapshot video --review` and compare each beat with its row in `STORYBOARD.md`: right chip, right picture, right host, every word inside the clear area and the picture filling the whole frame (`../../reference/safe-zones.md`). Fix and re-snapshot until every row matches.
7. **Render.** `npx hyperframes render video --quality delivery --output <slug>.mp4`.
8. **Verify the file.**
   - `npx hyperframes measure cuts <slug>.mp4`: compare cuts per minute and shot lengths with the reference's `cuts.json`.
   - `npx hyperframes audio <slug>.mp4 --json`: sound present, loudness around -16 to -14 LUFS for social.
   - Run the transcript overlap check from `../../reference/not-a-copy.md` on the final script.

Done when `check` passes, every storyboard row matches its snapshot, the render exists, and the verification numbers are reported. Say plainly that sound was measured, not heard.
