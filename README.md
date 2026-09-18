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

## Still outstanding

Two placeholders remain in the file, both marked in square brackets so they are
impossible to miss on the page:

- **`[FORM ENDPOINT]`** — the contact form's `action`. Until it points at a real
  handler (Formspree, Basin, a GoDaddy PHP script, anything), submitting shows a
  notice instead of sending. The form is currently the only way to reach RAS
  from the site, so this is the important one.
- **`[HERO PHOTOGRAPHY / RENDER]`** — the hero's building is still a hand-drawn
  SVG stand-in, marked in a comment above it. The Approach section now uses the
  real artwork; the hero does not.
