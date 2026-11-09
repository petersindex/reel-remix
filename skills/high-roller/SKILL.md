---
name: high-roller
description: Rank reels or short videos by engagement to pick which format to remix. Use when the person pastes several Instagram, TikTok or YouTube Shorts links and asks which performed best, or as step 1 of a remix.
---

# The High Roller: find

Bets on the reels pulling the most comments, the signal "comment KEYWORD" reels live on. Free: the numbers come from yt-dlp, with no API key.

## Steps

1. Read the links from `remix/<slug>/links.txt` (layout: `../../reference/project-layout.md`), or take them from the message and write that file.
2. Fetch the public numbers for all links in one call:

   ```bash
   yt-dlp --skip-download --ignore-errors --print "%(id)s	%(uploader)s	%(like_count)s	%(comment_count)s	%(view_count)s	%(upload_date)s	%(webpage_url)s" <link> <link> ...
   ```

   If a link fails with a login or rate-limit error, retry that link once with `--cookies-from-browser chrome` (or the person's browser), and say that their browser's Instagram session was used.
3. For each reel compute:
   - **Comment pull** = comments / likes. The headline number: it shows how hard the reel drives people to comment.
   - **Comments per day** = comments / days since `upload_date`, so a fresh reel is not punished for being young.
   - **Views** only when present. Instagram returns `NA` for views through yt-dlp; say so instead of estimating.
   Likes can be hidden by the creator and come back missing or implausibly low. Mark those rows and rank them on comments per day alone.
4. Write `RANK.md`: a table sorted by comment pull, the raw numbers beside each ratio, then two or three sentences naming the top reel's engine (the call to action, the hook, the promise) as a hypothesis for the Detective to confirm.

Done when every link has a row in `RANK.md` (a failed fetch gets a row saying why) and the top pick is named.

## Searching a niche

Finding reels by keyword needs a paid social data API; yt-dlp only reads links it is given. When the person has one connected (for example the treg MCP's Instagram reel search), use it to collect candidates and their comment and like counts, tell them the cost per search before running it, then rank as above. Without one, ask them for links: their own saved reels and the creators they watch are the best source anyway.
