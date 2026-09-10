# natsac

Design files for the Nature Sacred website.

Each page is a self-contained HTML file that opens directly in a browser —
no build step, no dependencies to install.

## Pages

| File | Page |
|---|---|
| `Homepage-V2.dc.html` | Homepage (current) |
| `About.dc.html` | About |
| `Why Sacred Places.dc.html` | Why Sacred Places |
| `The Bench and Journal.dc.html` | The Bench and Journal |
| `Our Design Process.dc.html` | Our Design Process |
| `Our History.dc.html` | Our History |
| `Our Team.dc.html` | Our Team |
| `The Firesoul Network.dc.html` | The Firesoul Network |
| `Evidence.dc.html` | Evidence |
| `News and Stories.dc.html` | News and Stories |
| `Join the Movement.dc.html` | Join the Movement |

Files beginning with `*` or containing `copy` / a trailing number are earlier
drafts and alternates, kept for reference.

## Supporting files

- `support.js` — shared runtime required by every page
- `image-slot.js` — drag-and-drop image placeholder component
- `assets/` — logos, marks, photography
- `CLAUDE.md` — writing and language rules for the site

## Viewing locally

Open any `.dc.html` file in a browser, or serve the folder:

```
python3 -m http.server 8000
```

then visit http://localhost:8000
