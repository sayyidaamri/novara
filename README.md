# NOVARA — native HTML site (no hosting needed)

![NOVARA homepage preview](docs/preview/homepage.gif)

An original site for a fictional studio, **NOVARA**. All copy, logo, project
names, client names, shaders and code are original. Photos come from Unsplash, video, music and sound
effects from Mixkit, and everything is stored locally.

## Running it

Open `site/index.html` in Chrome, Edge or Firefox by double-clicking it. It needs no server and no internet
connection, because fonts, three.js, images, video and audio are all in `site/assets/`.
Sound starts on your first click (browser autoplay rule). Turn it off with the round wave button in the header.

## Pages (22)

| File                   | Content                                                                                                                                                                                                                                                                                                  |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `index.html`           | Preloader, 3D hero (procedural glossy jacks pushed by the cursor), reel that grows into a full-width frame + video modal, Featured Work (12), "Where Creative Ideas…" tablet that zooms into a GLSL tunnel journey, end section with stickers, footer, scroll-nav → About                                |
| `about.html`           | Particle cloud + giant wordmark → "We are NOVARA…", text reveal, pinned TEAM viewer (7 people, glitch + scramble, pixel initial, ▶ button / swipe), brand marquees, awards/articles/talks, blue "Area of Expertise" card deck that deals out and flips, blue dot-wave end section, scroll-nav → Projects |
| `projects.html`        | "PROJECTS 19 ↘" + 2-column grid of all 19 projects, scroll-nav → About                                                                                                                                                                                                                                   |
| `projects/*.html` (19) | Themed detail page (accent colour per project), BACK pill, meta + services/links, horizontal media rail driven by vertical scroll, "Next project" panel (over-scroll navigates)                                                                                                                          |

## States and interactions

- **Preloader** (first visit per session): rolling 000→100 digits and a bar that turns into the logo glyph.
- **Menu**: dropdown cards (links / newsletter / labs) with stagger and blur. On mobile it is a full-screen blue panel. Close it with the button, Esc or a click outside.
- **Header hovers**: Let's talk (blue + arrow), Menu (white, dots rotate), Sound (blue).
- **Video modal**: click the reel to open it. It has Play/Pause, a seek bar and Mute, a custom "Close" cursor, and closes with Esc or a click.
- **Grid cards**: they enter narrower with a bowed top edge and flatten into the grid; on hover the image does a focus pull (blur + zoom, then sharp) with a faint grid flash, the arrow slides in and the title letters roll.
- **Newsletter** (menu + footer): demo validation only (error / success message). **Nothing is sent.**
- **Scroll-nav / next project**: keep scrolling at the bottom to fill the green bar and the site opens the next page.
- **Page transitions**: a colour wipe between pages.
- **Scroll reveals**: hero/paragraph words rise with a 15° tilt (staggered). Project cards slide up and scale in with the scroll (image first), then the tags and title letters roll in. The footer text slides up line by line and the input background wipes in from the left.
- **Gestures**: hero, press = burst and drag = stir the 3D pieces. Team, the blue button is the cursor and follows the pointer; click anywhere (or swipe on mobile) for the next person. Expertise cards tilt toward the pointer. Project detail, drag the media rail with the mouse.
- **Page fluid** (`fluid.js`): moving the cursor anywhere leaves a milky white smear with iridescent rims behind every light section; it scrolls with the page and slowly fades. Inside the hero frame the same motion drags the 3D image.
- **Snake lines**: a blue tube (reel) and a cyan tube (goal) of fixed length slide along their path with the scroll and coil around the thumbnail and title.
- **Reel**: line 1 "Bold Ideas," glides into its indent; the thumbnail warps like fabric (curved edges, video drawn in strips on a 2D canvas) from blue duotone to full colour; the PLAY/REEL words rise on their own and the play button pops in at the end.
- **Goal journey (3D, own procedural astronaut)**: tablet showing the astronaut above earth → fills the screen → text spreads and grows → astronaut recedes into a rainbow ring → wireframe scaffold tunnel (white → red/cyan → green/yellow) → pink crystal → white flash → blue room → monitor zoom-out, the glass shatters and the astronaut flies out → the astronaut stands in the end section while the stickers burst out around it.
- **Page transition**: diagonal black shutters → pixel "L" → "LOADING" types out → the new page enters as a rotated grey card that straightens. On About the wordmark letters enter in a wave, then fly off one by one on scroll.
- `prefers-reduced-motion` is respected.

## Sound map (Mixkit, `site/assets/audio/`)

| Trigger                                            | File                      |
| -------------------------------------------------- | ------------------------- |
| Background loop after first interaction            | `music.mp3` ("Vastness")  |
| Hover on any button / link / card (`data-sfx`)     | `hover.mp3`               |
| Click on buttons / links                           | `click.mp3`               |
| Menu open / close, closing the video               | `menu.mp3`                |
| Focus on an email input, validation error          | `focus.mp3`               |
| Page transition                                    | `page.mp3`                |
| Entering the tunnel / crystal phase (home)         | `tunnel.mp3`, `glass.mp3` |
| Preloader done, newsletter OK, scroll-nav complete | `chime.mp3`               |
| Team member change, card deal, project rail item   | `slide.mp3`               |

## Editing copy

All text, projects, team, clients and awards are in `tools/data.mjs`. After editing it, regenerate the pages:

```
node tools/build.mjs
```

Styles are in `site/assets/css/main.css` and behaviour is in `site/assets/js/` (`core.js` shared; `hero.js`,
`home.js`, `end.js`, `about.js`, `project.js` page-specific; `astronaut.js` = the procedural astronaut model).

## Placeholders to replace

Brand name/logo (`NOVARA`, CSS wordmark + SVG glyph), emails `hello@novara.studio` / `studio@novara.studio`,
the Lisbon address, social links (point to generic domains), the "Labs" link (example.com), the project
"Launch project" / link buttons (dead links on purpose), all 19 projects, 7 team members, 16 client
names and the awards list (all fictional). Photos and videos are stock media.

## Technical notes

- **Font**: Inter Tight (free) for UI text, with IBM Plex Mono for monospaced labels.
- **3D content**: procedural three.js/GLSL scenes, original SVG stickers and CSS-treated photos.
- WebGL cannot read local images or video when a page is opened from `file://`, so photos and videos stay as
  DOM elements (with CSS parallax) instead of being drawn on the GPU.
- Native page scroll with custom smooth wheel scrolling and sticky sections, so keyboard, scrollbar and touch
  work normally.
