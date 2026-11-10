---
name: director
description: Write the script and shot-by-shot storyboard for a reel built on a reference's structure, in the person's brand. Use when they want a reel scripted or storyboarded, or as step 4 of a remix, after the breakdown and brand sheet.
---

# The Director: storyboard

Turns the reference's grammar into a new reel about the person's own topic. Reads `breakdown/*.md`, `RANK.md`, `remix/brand.md` and `TICKET.md` (layout: `../../reference/project-layout.md`); writes `STORYBOARD.md` from `templates/storyboard.md`.

## Steps

1. **Pick the engine.** Lead with the top reel in `RANK.md`; borrow devices from the others only where they serve it. Say which engine you took from which reel.
2. **Write the script.** About 2.5 to 3 spoken words per second. Aim near the reference's length, but say only what the topic needs: a shorter reel is fine, padding is not. The opening line is a specific, true claim about this exact video or result, never a generic promise. The call to action names one keyword.
3. **Cut it into chips.** Two to five words per chip, following the voice word by word. The spoken line stays on screen as it builds (finished words stay up until the line ends), so the line, not each chip, carries the reading time. Shot times are estimates at 2.7 words a second; the Editor retimes them to the real voice.
4. **Give every chip a picture.** For each chip, write what the picture **does** with those words: a character acting it, a prop moving, a real UI moment. Then apply the grammar the Detective found, as far as the reference used it:
   - a **prop arc**: one object introduced early that changes and pays off at the end;
   - one **running example** carried through every proof card;
   - **world, then proof**: a playful scene, then a real card (numbers, UI, the actual output) over it;
   - the **host steps out** when a lineup or demo needs the full frame.

   **Scale:** each shot's hero (the character, the card, the UI) spans at least 760 px of the 1080 px width or 40% of the height. A small object in an empty frame reads as squashed on a phone. The accent colour appears in every shot, on the one thing that matters.
5. **List assets.** For every shot: what exists already in `brand.md`, and exactly what must be made (each pose, prop, recording). List separately anything that must be real before posting: links, the DM automation behind the keyword.
6. **Check** with the list in the template, including the transcript overlap rule in `../../reference/not-a-copy.md` (against every `transcript.json` that exists) and the layout planned in `../../reference/safe-zones.md`. Fix and re-check until every box is ticked; the Editor verifies the layout on real frames.
7. **Stop.** Show the script and the shot table, and wait for the person's go. Notes change only the shots they name.

Done when every box in Checks is ticked and the person has said go.
