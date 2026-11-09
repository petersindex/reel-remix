---
name: brand-cop
description: Build the person's brand sheet (colours, fonts, host, voice) and swap a reference reel's look for theirs. Use when they set up their brand for reels, or as step 3 of a remix, before any storyboard.
---

# The Brand Cop: rebrand

Pulls over everything in the reference that isn't the person's and writes the swap. No storyboard is written until `remix/brand.md` exists.

## 1. The brand sheet (once per person)

If `remix/brand.md` exists, read it, show a three-line summary, and ask only whether anything changed. Otherwise build it from `templates/brand.md`:

1. Look before asking. Check the working directory for a logo, brand guide, fonts, or a website URL the person mentioned; pull hex values and fonts from those, and say where each came from.
2. Ask for what is still empty, a few fields per message, offering a concrete recommendation each time ("Your logo's blue is #1F4FD8; use it as the accent?"). For colours with no source, propose a palette from one physical scene that suits their niche (a gym's chalk, rubber and steel) instead of an abstract mood.
3. **Host files** decide what the Editor can build, so pin them to real files: a face-cam clip, a transparent cut-out, character art. A person filming themselves needs nothing made: after the Director's script is approved, they record it as a phone selfie (vertical, eyes at the top third, window light in front of them), and that clip is both the host and the voice. With no host at all, the remix is built from kinetic type and screen recordings, and the sheet says so.

Done when every field in the template has a value or an explicit "none", and every file path in it exists.

## 2. The ticket (once per remix)

Read every `breakdown/<id>.md` and `remix/brand.md`, then write `remix/<slug>/TICKET.md`: one row per element of the reference look, with what it becomes.

| Theirs | Yours | Note |
|---|---|---|
| e.g. cream paper ground #F2F0EB | cobalt #0840D8 from brand.md | grid lines kept, recoloured white |
| e.g. their face, bottom half | your face-cam, bottom half | same framing |
| e.g. pixel mascot in costumes | your character, or kinetic type | keep the acting, not the character |

Cover ground, ink, accent, type, caption chips, host, characters, logo, music and voice. Follow `../../reference/not-a-copy.md`: their structure and devices may travel, their people, words, footage and characters may not.

Done when every element named in each breakdown's Packaging, Host and Motion sections has a row.
