# Safe zones for a 1080x1920 reel

Instagram scales a reel to fill the screen above its tab bar, so a 9:16 video is cropped at the edges, then draws its UI on top. The rule: **the picture fills the whole frame, the words stay clear of the crop and the UI.**

## Measured on an iPhone (1320x2868 screen, Reels viewer)

The reel is scaled 1.42x. In the reel's own 1080x1920 pixels:

| What | Where | Effect |
|---|---|---|
| Visible area | x 74 to 1003, y 28 to 1879 | about 75 px is cropped off each side |
| Clock, back arrow, + | y up to 134 | covers the top |
| Like, comment, share, save rail | x 904 to 975, y 1012 to 1807 | covers the right edge in the lower half |
| Handle and caption | y 1716 to 1821, with a dark fade from about 1650 | covers the bottom |

## The layout that clears all of it

| Zone | Pixels | Holds |
|---|---|---|
| Headline | x 110 to 970, y 240 to 390 | the words; also inside the profile grid's 3:4 cover crop (y 240 to 1680) |
| Stage | x 110 to 970, y 420 to 940 | characters, props, the world |
| Lower cards | x 110 to 880, y 970 to 1560 | anything readable below y 1000 stays left of the rail |
| Below 1600 | full width | picture only: ground, texture, the bottom of a scene |

Characters and grounds may bleed past these lines; words, numbers, a host's mouth and anything a viewer must read may not.

## Keep blocks apart

- At least 40 px between any two blocks (cards, characters, the headline).
- A character stands beside a card, not on it. A perch may overlap a card's corner, never its text.
- An element that moves to point at something lands beside its target, never over it.

Other phones and TikTok or YouTube Shorts crop a little differently; the margins above leave room for that. For a new device, record the reel playing in the app and measure where its grid lines land, as above.
