# VÉLORA Eyewear: Luxury Sunglasses Website

A multi-page static website for the sunglasses brand VÉLORA Eyewear, built with HTML5, CSS3 and a little vanilla JavaScript. There is no framework, build step, backend or checkout.

**Pages:** Home (full-width photo slideshow, featured frames, brand story, editorial feature), Shop (10 sunglasses with clickable color swatches), Product page (one dedicated page per frame), About (brand story, philosophy), Contact (front-end demo form).

## 1. Run it locally

- **Simplest:** double-click `index.html`.
- **VS Code:** install *Live Server*, right-click `index.html`, choose **Open with Live Server**.
- **Node.js:** `npx serve .` in this folder. **Python:** `python3 -m http.server`, then open http://localhost:8000.

Photos and fonts load from the internet, so you need a connection. If a photo cannot load, a neutral VÉLORA placeholder appears instead of a broken-image icon.

## 2. Project structure

```
velora-eyewear/
├── index.html  shop.html  about.html  contact.html
├── product.html             ONE reusable product page (opens any frame)
├── css/style.css            One shared stylesheet
├── js/
│   ├── products.js          Product data used by the product page (names, prices, colors, photos)
│   ├── product.js           Draws the product page and handles its color swatches
│   ├── shop.js              Color swatches on the shop and home product cards
│   ├── slideshow.js         Hero slideshow behavior (you normally never edit this)
│   ├── main.js              Mobile menu + contact form validation
│   └── images.js            Fallback if a remote photo fails to load
├── images/
│   ├── slideshow/           PUT YOUR OWN HOMEPAGE SLIDESHOW PHOTOS HERE
│   └── fallback.svg         Neutral picture shown only if a photo fails to load
├── tools/check-images.mjs   **Slideshow images supplied by the site owner.** `images/slideshow/tortoise-orange-backdrop.webp`, `four-frames-editorial.jpg` and `gold-shield-portrait.webp` (slides 4 to 6) were provided by the site owner and are stored in the project. They are not from Unsplash and are not covered by the license above: they appear to be professional editorial photographs, so make sure you have the right to publish them on this site, or replace them with images you own.

Run `node tools/check-images.mjs` to test every photo URL
└── README.md
```

## 3. Product pages

Clicking a product card (its image, its name or **View Details**) opens `product.html?id=VL-001`, a dedicated page with a large image, the name, price, description, selectable color swatches, an **Add to Cart** button and a **Back to Collection** link (top of the page) to `shop.html`. Selecting a color changes the large image, and the address also gets the color (`product.html?id=VL-001&color=Silver`) so the page can be reloaded or shared in that color. If a visitor picks a color on a shop card first, the card's links open the product page in that color.

There is no list of details under the shop grid any more.

**Cart.** *Add to Cart* adds the selected frame **in the selected color** to a simple cart. The number of items shows on the bag icon in the header on every page, and the items are kept in the visitor's browser (`localStorage`, key `velora-cart`; the code is in `js/main.js`). Adding the same frame in the same color again raises its quantity. There is no cart page, checkout or payment: the bag icon still links to the shop.

**To change a product:** edit its entry in `js/products.js` **and** its card in `shop.html` (and `index.html` if it is featured there).
**To add a product:** add an entry in `js/products.js` with a new unique `id` (for example `VL-011`) and copy an existing card in `shop.html`, changing the `id` in its three `product.html?id=...` links, its `data-` attributes and its swatches.
Every color needs **its own photo**, so the large image always matches the selected color.

If an address has an unknown `id`, the page shows a friendly "We couldn't find that frame" message with a link back to the collection.

## 4. Managing the homepage slideshow yourself

- **Slides live in:** `index.html`, in the section `<section class="hero" ...>`. Look for the comment *"HOMEPAGE SLIDESHOW: HOW TO ADD, REPLACE, REORDER OR REMOVE IMAGES"*; the slides are right below it.
- **Image paths are the `src="..."` inside each `<div class="hero__slide">`.**
- **Your own pictures go in:** `images/slideshow/` (see the `README.txt` in that folder). Use a path like `src="images/slideshow/summer-campaign.jpg"`.
- **To add a slide:** find the *SLIDE TEMPLATE* at the end of the slides. Delete the two lines that contain only `<!--` and `-->`, then set your file name, `alt` text and headline.
- **To replace:** change the `src` (and `alt`). **To remove:** delete the whole `<div class="hero__slide"> ... </div>`. **To reorder:** move whole blocks; the order in the file is the order on the site.
- Dots are created automatically. `js/slideshow.js` and `css/style.css` need no changes.
- Recommended pictures: landscape, 2000 × 1250 px, JPG or WebP, under about 400 KB, with the subject near the middle.

## 5. Contact form

The form (Full name, Email address, Subject, Message) has labels, HTML validation, inline error messages and a character counter. It is a **front-end demonstration**: the page says so, and after a valid submission it states that the message has not been sent or saved. No email address, phone number or social account is listed, because none exist for this project.

To receive real messages you would need a backend or a form service (for example Formspree or Netlify Forms). Once one is configured, point the form's `action` at it, change the submit handler in `js/main.js`, and update the demo note in `contact.html`.

## 6. Photos and license records

Except for three slideshow images (see below), all photographs come from the free [Unsplash](https://unsplash.com) library (`images.unsplash.com`, not Unsplash+) and are loaded directly from there; no copies are stored in the project.

**License check.** Under the [Unsplash License](https://unsplash.com/license) the photos may be used for commercial and non-commercial purposes, and **credit is not required** (it is only "appreciated"). The license forbids compiling Unsplash photos to replicate a similar or competing service. It does not address model releases or trademarks, so if VÉLORA ever becomes a real business, replace these stock photos with your own photography. For that reason no photographer names, credits or source links appear on the public pages. This table is the license record; keep it up to date when you change photos.

| Where it is used | Photographer | Unsplash page |
|---|---|---|
| About: Our Story | Peri Stojnic | https://unsplash.com/photos/Q7y7GVH4mtI |
| About: Timeless Eyewear; Shop: Solène, Black | Kiran CK | https://unsplash.com/photos/lSl94SZHRgA |
| Home: brand story | Ben Iwara | https://unsplash.com/photos/z8-Fu0KudgA |
| Home: editorial feature | Ben Iwara | https://unsplash.com/photos/z8-Fu0KudgA |
| Home: slideshow, slide 1 | YASU SHOTS | https://unsplash.com/photos/_y6hMz1pJC0 |
| Home: slideshow, slide 2; Shop: Meridian, Gold | Daniel Schludi | https://unsplash.com/photos/tzA2MfnYSb0 |
| Home: slideshow, slide 3 | K Studios | https://unsplash.com/photos/INlbQFDQnJ4 |
| Home: slideshow, slide 4; Shop: Ondine, Black | Lucas George Wendt | https://unsplash.com/photos/3xtCeUhqZWE |
| Shop: Alpine, Black | Alex Perez | https://unsplash.com/photos/4AtyEKK36DI |
| Shop: Alpine, White | Annie Williams | https://unsplash.com/photos/FlP6C5pkMKs |
| Shop: Atlas, Black | Daniel Schludi | https://unsplash.com/photos/7J-ro9TbEp0 |
| Shop: Atlas, Tortoise | Apostolos Vamvouras | https://unsplash.com/photos/Pp_nVOuJMTU |
| Shop: Atlas, White | GianCarlo Greco | https://unsplash.com/photos/nAdZH0_SRx0 |
| Shop: Capri, Red | Thayná Gandra | https://unsplash.com/photos/NEFEAFqUnJw |
| Shop: Capri, White | Sebastian Coman Travel | https://unsplash.com/photos/dtOTQYmTEs0 |
| Shop: Cognac, Brown | Natalie Kinnear | https://unsplash.com/photos/OP342zvseUs |
| Shop: Cognac, Tortoise | Nick Hillier | https://unsplash.com/photos/QsBTYwxjzUU |
| Shop: Heritage, Black | Joseph Greve | https://unsplash.com/photos/dPw0N01onxE |
| Shop: Heritage, Brown | Orion | https://unsplash.com/photos/m_T5fWmYSWw |
| Shop: Lumière, Black | omid armin | https://unsplash.com/photos/Zt99Ho5Hq3s |
| Shop: Lumière, Silver | Adam Thomas | https://unsplash.com/photos/3Npd9GJEKrE |
| Shop: Meridian, Black | Andres Hernandez | https://unsplash.com/photos/ouAyz-zRMTw |
| Shop: Meridian, Silver | Laura Chouette | https://unsplash.com/photos/VgVvWHYwl3c |
| Shop: Ondine, Silver | Rainy Wong | https://unsplash.com/photos/_thycCxUAEo |
| Shop: Sable, Green | Laura Chouette | https://unsplash.com/photos/k3xpBOMzJnc |
| Shop: Sable, Teal | Daniel Lincoln | https://unsplash.com/photos/SttmdhoyRlk |
| Shop: Solène, Black & Brown | Charlota Blunarova | https://unsplash.com/photos/V4pktt_0_mI |

Run `node tools/check-images.mjs` once with an internet connection. It requests every photo URL used by the site and reports any that fail to return an image.

**Colors.** Each swatch has its own photograph, named by the photographer's description of it. No photo is used for two colors. Stock photography rarely shows one exact frame in several colors, so the frame shape can vary slightly between colors of the same model; replace them with your own product photos (one per color) when you have them.

## 7. Other content

- **Colours and fonts:** CSS variables at the top of `css/style.css`: `--beige #E8DCCB`, `--espresso #49372B`, `--cream #FAF7F2`, `--caramel #B79A78`, `--gold #D6C09A`. Fonts: [Cormorant Garamond](https://fonts.google.com/specimen/Cormorant+Garamond) and [Jost](https://fonts.google.com/specimen/Jost) (SIL Open Font License) via Google Fonts.
- **Footer:** the same three lines on every page (`footer.site-footer`).

## 8. Simple Static Website requirements

Multiple linked pages; a shared navigation bar (with mobile menu); images with `alt` text; a footer on every page; responsive layouts (CSS Grid, Flexbox, media queries at 1024, 820 and 560 px); semantic HTML; HTML, CSS and JavaScript in separate files.

## 9. Future virtual try-on

Nothing camera-related exists: no permissions, no face tracking. The structure is ready: every product has an `id`, color changes fire a `velora:colorchange` event, and a future `js/tryon.js` can be added separately. Try-on overlays would need transparent product images; photos with backgrounds will not work for that.

## 10. What changed in this update

- **Slideshow:** three new slides (4 to 6) added to `index.html` after the existing ones, with their images in `images/slideshow/`. All existing slides are unchanged; only the screen-reader numbers (`1 of 6` ...) were updated.
- **Add to Cart:** on `product.html` the button that said *Back to Collection* is now *Add to Cart* (`js/product.js`). The bag icon shows a count (`js/main.js`, `css/style.css`). The *Back to Collection* link at the top of the product page remains.
- **Added:** `images/slideshow/tortoise-orange-backdrop.webp`, `images/slideshow/four-frames-editorial.jpg`, `images/slideshow/gold-shield-portrait.webp`.
- **Modified:** `index.html`, `js/main.js`, `js/product.js`, `css/style.css`, `README.md`.

## 11. Testing checklist

**Desktop:** all nav links work; every product card opens the right product page from its image, name and View Details; every swatch on the product page changes the large image and label; Back to Collection returns to the shop; slideshow arrows, dots and autoplay work; form validation appears; no console errors (F12); `node tools/check-images.mjs` reports no failures.

**Mobile / tablet (DevTools device mode at 360, 390, 768, 1024 px):** no horizontal scroll; menu opens and closes; product page stacks image above details; swatches are easy to tap; hero text, arrows and dots are readable.

**Accessibility:** Tab reaches everything with a visible focus ring; with "reduce motion" on, the slideshow does not auto-advance.
