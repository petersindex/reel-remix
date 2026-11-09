# Project layout

Every Reel Remix skill reads and writes inside the person's working directory, never inside the plugin folder.

```
remix/
├── brand.md                    the person's brand sheet, reused across remixes (brand-cop)
└── <slug>/                     one remix, slug from the person's topic, e.g. remix/morning-routine
    ├── links.txt               the reel URLs, one per line
    ├── RANK.md                 engagement ranking (high-roller)
    ├── refs/<id>.mp4           downloaded references, plus <id>.info.json
    ├── breakdown/<id>/         measure output, sheets/, transcript.json
    ├── breakdown/<id>.md       the written breakdown (detective)
    ├── TICKET.md               what changes from their reel to yours (brand-cop)
    ├── STORYBOARD.md           script and shot table (director)
    ├── video/                  the HyperFrames project (editor)
    └── <slug>.mp4              the final render (editor)
```

A step is done when its file exists and meets that skill's completion criterion. A later skill reads the earlier files rather than asking again.
