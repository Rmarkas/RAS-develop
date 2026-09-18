# RAS Development — marketing site

Single-page site for RAS Development, a commercial and residential builder in
Austin, Texas.

Everything is in **`index.html`**. One file: inline CSS, vanilla JS, inline SVG
artwork. No framework, no build step, no dependencies to install. Open it in a
browser and it works.

The only external request is the Google Fonts stylesheet for Jost and
Source Sans 3.

---

## Deploying

The file is named `index.html`, which is what every web host looks for by
default, so there is nothing to configure — whatever directory it sits in
becomes that page.

### GoDaddy (cPanel / Web Hosting)

1. Log in to GoDaddy → **My Products** → your hosting plan → **cPanel Admin**.
2. Open **File Manager**.
3. Go to **`public_html`** (this is the web root — the folder the domain serves).
4. **Upload** `index.html` into it.
5. Visit your domain. That's it.

If `public_html` already contains a GoDaddy placeholder `index.html`, delete or
rename it first, or your file will not be the one served.

If the domain is on **GoDaddy Website Builder** rather than cPanel hosting, you
cannot upload a raw HTML file — Website Builder only serves pages it generates.
You would need to switch the domain to a hosting plan (or point it at another
host, see below).

### Pushing updates

GoDaddy does not pull from GitHub automatically. After changing `index.html`,
re-upload it through File Manager, or set up FTP/SFTP with the credentials in
cPanel and overwrite the file there.

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
- **`[HERO PHOTOGRAPHY / RENDER]`** — the hero's building artwork is a
  hand-drawn SVG stand-in, marked in a comment above it.

The mid-page building render is also hand-authored SVG. To reach true parity
with the logo it should be replaced with the actual logo artwork, cropped to the
building, with the existing SVG wireframe traced over it.
