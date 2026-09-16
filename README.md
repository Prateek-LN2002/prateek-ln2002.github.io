# Prateek L N — portfolio site

A single-page, self-contained portfolio. No build step, no dependencies.

```
index.html                 the whole site (HTML + CSS + JS in one file)
assets/media/<project>/    drop gameplay videos and screenshots here
```

---

## 1. Put it online (GitHub Pages)

You already have a GitHub account: **Prateek-LN2002**.

```bash
# from inside this folder
git init
git add .
git commit -m "portfolio site"
git branch -M main
git remote add origin https://github.com/Prateek-LN2002/portfolio.git
git push -u origin main
```

Create the empty `portfolio` repo on GitHub first (github.com/new, public, no README).

Then: **repo → Settings → Pages → Source: Deploy from a branch → Branch: `main` / `root` → Save.**

Live in about a minute at:

```
https://prateek-ln2002.github.io/portfolio/
```

That is the link to put on your resume, LinkedIn and job applications.

---

## 2. Add your gameplay videos and screenshots

Put the files in the right folder:

```
assets/media/sharp-shooter/gameplay.mp4
assets/media/sharp-shooter/poster.jpg
assets/media/learning-program/01.jpg
assets/media/room-tone/01.jpg
```

Then open `index.html`, find the **MEDIA CONFIG** block near the bottom, and fill in the entry:

```js
const MEDIA = {
  "sharp-shooter": {
    video: "assets/media/sharp-shooter/gameplay.mp4",
    poster: "assets/media/sharp-shooter/poster.jpg",
    caption: "Wave 7 — sniper loadout"
  },
  "learning-program": {
    shots: [
      "assets/media/learning-program/01.jpg",
      "assets/media/learning-program/02.jpg",
      "assets/media/learning-program/03.jpg"
    ],
    caption: "Four titles from Set 5"
  },
  "room-tone": {},

  // animation & rendering section — same shape, shows a small 16:9 panel
  "reel-titan":  { video: "assets/media/reel/titan.mp4" },
  "reel-kids":   {},
  "reel-unreal": {},
  "reel-test":   { video: "assets/media/reel/creature-test.mp4" }
};
```

- `video:` shows one player. `shots:` shows one big image with a clickable thumbnail strip underneath.
- Any entry left as `{}` keeps its placeholder panel (or, in the reel section, shows nothing at all), so the page never looks broken.
- **Run For The Time** needs no video — it already links to your live playable build, which is stronger than a clip.
- Then `git add . && git commit -m "add media" && git push`.

### Video tips
- **Keep each clip under ~20 MB.** GitHub Pages has a 1 GB repo limit and big files make the page slow.
- MP4 / H.264, 1280×720, 30 fps, 20–40 seconds is plenty. Show the best 20 seconds, not the whole level.
- Compress with:
  ```bash
  ffmpeg -i raw.mp4 -vf scale=1280:-2 -c:v libx264 -crf 26 -preset slow -an gameplay.mp4
  ```
  (`-an` drops audio, which usually halves the size. Keep audio for Room Tone.)
- Grab a poster frame:
  ```bash
  ffmpeg -i gameplay.mp4 -ss 3 -vframes 1 poster.jpg
  ```
