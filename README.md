# RAS Development — marketing site

Single-page site for RAS Development, a commercial and residential builder in
Austin, Texas.

Two files, and both are needed:

- **`index.html`** — the whole site. Inline CSS, vanilla JS, inline SVG. No
  framework, no build step, nothing to install.
- **`building.jpg`** — the RAS mark's own render, cropped to the building. The
  Approach section dissolves into it.

The only external request is the Google Fonts stylesheet for Jost and
Source Sans 3.

### About the Approach animation

As you scroll that section, a gold wireframe draws itself, then the real render
fades up through it — dark shell first, then lit. The wireframe is SVG whose
coordinates were **measured off `building.jpg`** (roof arris, soffit edge, base
line and each mullion), so the lines land on the real building.

That means the two are coupled: **if `building.jpg` is ever replaced or
re-cropped, the wireframe has to be re-traced**, or the lines will drift off the
photo. The wireframe lives in the `<svg class="wireL">` block in `index.html`.

---

## Deploying

The file is named `index.html`, which is what every web host looks for by
default, so there is nothing to configure — whatever directory it sits in
becomes that page.

### GoDaddy (cPanel / Web Hosting)

1. Log in to GoDaddy → **My Products** → your hosting plan → **cPanel Admin**.
2. Open **File Manager**.
3. Go to **`public_html`** (this is the web root — the folder the domain serves).
4. **Upload both `index.html` and `building.jpg`** into it, side by side.
5. Visit your domain. That's it.

Both files must sit in the same folder. If only `index.html` is uploaded, the
page loads but the Approach section stays as a bare wireframe.

If `public_html` already contains a GoDaddy placeholder `index.html`, delete or
rename it first, or your file will not be the one served.

If the domain is on **GoDaddy Website Builder** rather than cPanel hosting, you
cannot upload a raw HTML file — Website Builder only serves pages it generates.
You would need to switch the domain to a hosting plan (or point it at another
host, see below).

### Pushing updates

GoDaddy does not pull from GitHub automatically. After changing a file,
re-upload it through File Manager, or set up FTP/SFTP with the credentials in
cPanel and overwrite it there.

### Alternatives worth considering

Because this is a single static file, any of these will host it free, and each
deploys straight from this repository on every push — no manual upload:

- **Netlify** or **Vercel** — connect the repo, no build command, publish
  directory `.`. Point the GoDaddy domain at them with a DNS record.
- **Cloudflare Pages** — same idea.
- **GitHub Pages** — simplest, but this repository is **private**, and Pages
  from a private repository requires a paid GitHub plan. Making the repository
  public would let it work on the free tier.

---

## The contact form

Submissions are emailed to **hello@villavistahomes.com** through
[FormSubmit](https://formsubmit.co), which needs no account and no server —
useful here, because the site is a static file.

The page posts to FormSubmit's AJAX endpoint with `fetch`, so the visitor never
leaves: on success the form dissolves and a confirmation — check mark, "we'll get
back to you within one business day" — eases up in its place. If JavaScript is off,
the plain `<form action>` still posts and FormSubmit shows its own thank-you
page.

### One-time activation — required before any mail arrives

FormSubmit will not forward to an address until that address is confirmed.

1. Open the live site and send a test request through the form.
2. FormSubmit emails **hello@villavistahomes.com** with an activation link.
   Click it.
3. Send one more test. That one lands in the inbox, and every one after it.

Until step 2 is done, the page still shows the confirmation but no mail is
delivered — so do this before pointing anyone at the site.

### Changing the address

It appears twice in `index.html`, and **both have to change together**:

- the `action` on `<form id="contactForm">` — the no-JS fallback
- `var ENDPOINT` in the form script — the `/ajax/` variant

A new address needs its own activation round.

### Hiding the address from scrapers

The address is deliberately **not displayed anywhere on the page** — not in the
contact panel, not in the post-submit confirmation, not in the send-failure
notice. The form is the only route in.

It does still sit in the page source in plain text, in the two spots above,
because FormSubmit addresses its delivery by it. After activating, FormSubmit
gives you a random alias for that address; swapping the alias into both spots
keeps the form working and takes the mailbox out of the HTML entirely. That is
the remaining step if you want it gone from view-source too.

### Project types

The dropdown offers Commercial, Residential, Spec Home and Investment
Partnership. Field
names are capitalized (`Name`, `Project Type`, …) because FormSubmit prints them
verbatim as the labels in the email it sends.

---

## Still outstanding

One placeholder remains, marked in square brackets so it is impossible to miss
on the page:

- **`[HERO PHOTOGRAPHY / RENDER]`** — the hero's building is still a hand-drawn
  SVG stand-in, marked in a comment above it. The Approach section now uses the
  real artwork; the hero does not.
