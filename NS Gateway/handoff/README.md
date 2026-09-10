# Nature Sacred — website design files

Nine finished pages. Each is a self-contained HTML file — no build step, no
dependencies to install.

## Pages

| File | Page |
|---|---|
| `final_Homepage.dc.html` | Homepage |
| `final_About.dc.html` | About |
| `final_Why Sacred Places.dc.html` | Why Sacred Places |
| `final_The Bench and Journal.dc.html` | The Bench and Journal |
| `final_The Network.dc.html` | The Firesoul Network |
| `final_Evidence.dc.html` | Evidence |
| `final_Our Team.dc.html` | Our Team |
| `final_Join the Movement.dc.html` | Join the Movement |
| `final_Donate.dc.html` | Donate |

Pages link to each other by filename, so keep them all in the same folder.

## Supporting files

- `support.js` — shared runtime; required by every page, must sit alongside the HTML
- `image-slot.js` — image placeholder component
- `.image-slots.state.json` — saved image crop/zoom positions (hidden file; include it)
- `assets/` — logos, marks, illustrations, photography

## Viewing locally

Serve the folder over HTTP — opening the files directly with `file://` will
break image loading:

```
python3 -m http.server 8000
```

then visit http://localhost:8000

## Brand notes

- Fonts: Nunito (sans, all UI and headlines), Lora (serif, journal entries and
  pull quotes), Caveat (handwriting, used sparingly). All loaded from Google Fonts.
- Primary green `#96c43d`, forest `#57a143`, bench taupe `#9d877a`,
  deep wood `#77441d`, coral `#ff4800`, journal yellow `#f5d06a`.
  Page background is warm paper `#fdfbf6`.
- Language: communities *create* Sacred Places; Nature Sacred guides the process.
  Avoid "we build." Firesoul carries a ™ on first use in body copy on each page.
  "Greenspace" is always one word.
