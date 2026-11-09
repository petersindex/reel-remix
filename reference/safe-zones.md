# Safe zones for a 1080x1920 reel

The app draws over the video. Anything that must be read or seen goes inside the clear area.

| Zone | Pixels on 1080x1920 | What covers it |
|---|---|---|
| Top 14% | y 0 to 270 | Reels header, camera icon |
| Bottom 35% | y 1250 to 1920 | caption, @handle, audio row, Follow button |
| Right side, bottom 40% | x 960 to 1080, y 1150 to 1920 | like, comment, share, save rail |
| Sides 6% | 65 px each side | edge crop on some phones |

**Clear area:** x 65 to 1015, y 270 to 1250. Every word, the host's face and mouth, and every proof card sit inside it. The covered zones carry only ground, texture or decoration.

**Cover frame:** the profile grid crops every reel to 3:4 from the centre (y 240 to 1680), so the first frame's hook sits inside the clear area too.

These are Meta's published Reels percentages converted to pixels. TikTok and YouTube Shorts overlays are similar; check the platform when the reel is made for one of them.
