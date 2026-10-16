# Nafiya ♡ Anas — Anniversary Surprise Website

A private, cinematic anniversary story for Anju, in six stages:

1. **Intro** — "Nafiya ♡ Anas" written in golden calligraphy
2. **Wedding-date lock** — a golden padlock that opens with the right date
3. **Photo puzzle** — a real jigsaw (swap puzzle) made from your wedding photo
4. **Our Memories** — a gallery of about 10 photos with a full-screen viewer
5. **Love letter** — a sealed envelope that opens to Nafiya's own letter, with an optional music player
6. **Final reveal** — "HAPPY ANNIVERSARY · MY ANJU · Forever Yours, Nafiya ♡"

The visitor can only move forward one stage at a time through each stage's own button. There is no way to jump straight to the end.

Built with React, TypeScript, Vite, Tailwind CSS, Framer Motion and Lucide icons. No paid services or accounts are needed.

---

## 1. What you still need to add (the site works without them, using labelled placeholders)

| What | Where | Used for |
| --- | --- | --- |
| Wedding photo | `public/images/wedding.jpg` | The jigsaw puzzle |
| About 10 photos | `public/images/photo1.jpg` … `photo10.jpg` | The gallery |
| Final photo (optional) | `public/images/final.jpg` | Faint background of the last scene |
| Music (optional) | `public/audio/romantic-music.mp3` | The little music player |
| Nafiya's letter | `src/content/letter.ts` | The love letter |

Until the files exist the site shows clearly marked **Placeholder** tiles (nothing crashes). No AI-made photos are used anywhere.

---

## 2. Run it on your computer (first time)

1. Install **Node.js** (the "LTS" version) from <https://nodejs.org>.
2. Open a terminal inside this project folder.
3. Install the parts the site needs (only once):
   ```
   npm install
   ```
4. Start the website:
   ```
   npm run dev
   ```
5. Open the address it prints (usually <http://localhost:5173>). Edits you save appear instantly.

To check everything is healthy before publishing:

```
npm test         # unit tests for the date lock, puzzle logic and letter splitting
npm run build    # type-checks and creates the final site in the "dist" folder
npm run preview  # opens the built site locally
```

---

## 3. Personalise it

### Photos
- Copy your pictures into `public/images/`. Best: use the names in the table above. The site is forgiving, though: `Wedding.JPG`, `photo 3.jpeg`, `Photo_3.png` etc. are all matched automatically (case, extension and spaces are ignored). If a gallery slot has no matching name, photos left over in the folder (for example `IMG_2041.jpg`) are used to fill it, in file-name order. The puzzle and final photos always need `wedding` / `final` in the name.
- **iPhone photos:** `.HEIC` files can't be shown by browsers. Convert them to `.jpg` first (the terminal warns you about this when you run `npm run dev`).
- **Puzzle picture:** `public/images/wedding.jpg`. Pick one clear, well-lit photo; any shape works (the board matches the photo's shape).
- **Replace an image:** put a new file with the same name in the same folder (replace the old one). If the browser still shows the old one, refresh with Ctrl+Shift+R (Cmd+Shift+R on Mac).
- **Final photo:** save it as `public/images/final.jpg`. To use another file name, change `finalPhoto` in `src/content/siteConfig.ts`.
- Keep each photo under about 1.5 MB so the page is quick on phones.

### Gallery photos, order and captions
Open `src/content/photos.ts`. Each photo is one line:

```ts
{ src: 'images/photo1.jpg', alt: 'Nafiya and Anas together, photo 1', caption: '' },
```

- **Caption:** type text between the quotes after `caption:` (leave `''` for none).
- **Alt text:** a short description for screen readers.
- **Add / remove / reorder:** copy, delete or move lines.
- If your files are `.png` or `.webp`, change the extension in `src`.

### Wedding date (the lock)
Open `src/content/siteConfig.ts` and edit:

```ts
weddingDate: { day: 18, month: 10, year: 2025 },
```

Visitors can type it as `18-10-2025`, `18/10/2025`, `2025-10-18`, `18.10.2025` or `18102025`. The correct date is never shown on screen.

### Puzzle difficulty
In `src/content/siteConfig.ts`, change `gridSize` (default `3` = 9 pieces). `4` = 16 pieces, `5` = 25 pieces. Allowed: 2 to 6.

### The love letter
Open `src/content/letter.ts` and replace the text between the backticks ( ` ) with Nafiya's letter.
- A **blank line** starts a new paragraph.
- A single new line inside a paragraph is kept.
- Short or long letters both work (a long letter scrolls inside the paper).
- Don't type a backtick character inside the letter.

### Music
- Put the file at `public/audio/romantic-music.mp3` (or change `music.src` in `siteConfig.ts`).
- Use only music you have the right to use (your own recording, a commissioned piece, or a royalty-free track whose licence allows it).
- Music **never starts by itself**; the visitor presses the play button (shown on the letter and final pages). If the file is missing, the player says so politely.

### Names
`wifeName`, `husbandName` and `nickname` are in `src/content/siteConfig.ts`. The fixed greeting lines are in the component files in `src/components/`.

---

## 4. About the date lock (important, please read)

The lock is a **playful front-end lock, not real security.** The website is just files sent to the visitor's browser, so the date is inside those files; a technically skilled person who inspects the page source could find it. It is meant to feel like a lovely surprise gate, not to protect secrets. For genuine privacy, don't share the link with anyone except Anju, and see the privacy notes in section 6.

---

## 5. Publish it to a public HTTPS link

First run `npm run build`. This creates a **`dist`** folder: that folder *is* your website. Every option below gives you an `https://` address that you can send to Anju.

**Easiest — Netlify Drop (free):** go to <https://app.netlify.com/drop>, drag the `dist` folder onto the page, and you receive a link. Rename it under *Site settings → Change site name*.

**Vercel (free):** push this project to GitHub, import it at <https://vercel.com/new>. Framework: *Vite*, build command `npm run build`, output folder `dist`.

**Cloudflare Pages (free):** connect the GitHub repository, build command `npm run build`, output directory `dist`.

**GitHub Pages (free):** the site is built with relative paths (`base: './'`), so the contents of `dist` work from a repository sub-path. Upload the contents of `dist` to a `gh-pages` branch, or use any GitHub Pages workflow that publishes `dist`.

Remember to add your photos (and music) to `public/` **before** building so they are included.

---

## 6. Keeping the link private
- The page asks search engines not to index it (`noindex`), but anyone with the link can open it, so send the link only to Anju.
- Pick a hard-to-guess site name when you publish.
- For extra privacy, Netlify and Cloudflare offer optional password protection (some tiers are paid; it is not needed for the site to work).

---

## 7. Project map

```
public/
  images/        <- your photos go here (see images/README.txt)
  audio/         <- your music goes here (see audio/README.txt)
  favicon.svg
src/
  content/       <- THE FILES YOU EDIT
    siteConfig.ts   names, wedding date, puzzle photo + difficulty, music
    photos.ts       gallery list and captions
    letter.ts       anniversaryLetter (the love letter text)
  components/    <- the six stages and shared pieces
    Intro.tsx  DateLock.tsx  Puzzle.tsx  Gallery.tsx  Lightbox.tsx
    Letter.tsx  Finale.tsx  AudioPlayer.tsx
    NamesLogo.tsx  GoldButton.tsx  ParticleBackground.tsx
    Celebration.tsx  SafeImage.tsx  HeartMark.tsx  ProgressDots.tsx
  utils/         date parsing, puzzle logic, letter splitting, asset paths, forgiving photo-name matching
  hooks/         image loading helper
  App.tsx        stage order, transitions, progress
tests/           unit tests (npm test)
```

## 8. How the puzzle works
The picture is cut into `n × n` pieces by positioning one copy of the photo behind each piece (no distortion). Pieces are shuffled with a random permutation, and a move is always a **swap of two pieces**, so every shuffle is solvable. The puzzle is complete only when every board position holds the piece that belongs there; the game checks the actual arrangement after every move and never relies on a button press.

Ways to play: drag a piece onto another (mouse, finger or pen), tap two pieces, or use the keyboard (arrow keys to move, Enter or Space to select and swap). A dropped piece that lands outside the board simply stays where it was.

## 9. Troubleshooting
- **A photo shows "Placeholder"** — the file isn't in `public/images/`, has no matching name (see above), or is a `.heic`/other format browsers can't show. Run `npm run dev` and read the `[images]` lines in the terminal, and the `[photos]` warnings in the browser console (F12), which list exactly which files were found.
- **Added photos while the site was running** — the page reloads by itself; if not, refresh once.
- **The lock doesn't open** — make sure the date in `siteConfig.ts` is what you expect, then type it as DD-MM-YYYY.
- **No music** — add `public/audio/romantic-music.mp3`, and press play (it never autoplays).
- **I want to see the last page right away while editing** — the site remembers progress for the current browser tab. Press the "Relive Our Story" button, or open the page in a new tab, to start from the beginning. (During testing you can also temporarily change the starting stage in `src/App.tsx`.)
"# wedding-surprise" 
