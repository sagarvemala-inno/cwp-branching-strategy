# CWP 2.0 Release Engineering Standard

The branching and release standard for Mobile, Backend, Frontend and AI, as a single self-contained web page. No build step, no dependencies, no framework.

Live at https://branching-strategy-cwp.vercel.app/ and embedded in Google Sites at
https://sites.google.com/innovapptive.com/pni-standards/branching-strategy

## Contents

| File | Purpose |
|---|---|
| `index.html` | The entire page. CSS, JavaScript, the Innovapptive logo and all seven diagrams are inline. |
| `favicon.png` | Square Innovapptive mark. Also embedded in `index.html`, so this file is optional. |
| `vercel.json` | Sends `noindex` and two standard security headers. |
| `.gitignore` | OS and editor noise only. |

## Putting it on GitHub

```bash
cd cwp-branching-standard
git init
git add .
git commit -m "CWP 2.0 release engineering standard"
git branch -M main
git remote add origin git@github.com:<org>/<repo>.git
git push -u origin main
```

## Connecting it to the existing Vercel project

**Connect the repository to the project that already exists.** Do not create a new
Vercel project from the repository.

The Google Site frames `https://branching-strategy-cwp.vercel.app/` by URL. A new
Vercel project gets a different `.vercel.app` address, which would leave the
Google Site pointing at a dead URL until someone edits the embed.

1. Vercel dashboard, open the existing **branching-strategy-cwp** project.
2. **Settings → Git → Connect Git Repository**, and pick the repository you just pushed.
3. Framework preset **Other**. Leave build command and output directory empty; the
   repository root is served as static files.
4. Production branch **main**.

From then on every push to `main` redeploys, the URL does not change, and the
Google Sites page picks up the new version with no edit in Sites.

If the project has to be recreated for any reason, the domain
`branching-strategy-cwp.vercel.app` can be moved to the new project under
**Settings → Domains**, and the Google Site keeps working.

## Editing the content

Open `index.html` and search for the section heading. The CSS custom properties at
the top of the `<style>` block control the whole palette, so a colour change is one
line. Diagrams are hand-written inline SVG inside `<figure class="fig">` blocks with
ids `figA` through `figG`.

## Notes

- The only external request the page makes is to Google Fonts for Poppins, Barlow and
  IBM Plex Mono. Everything else is embedded. If the network blocks Google Fonts the
  page falls back to system fonts and stays fully readable.
- Diagrams animate on scroll and each has a Replay control. They respect
  `prefers-reduced-motion` and render complete when JavaScript is unavailable.
- A print stylesheet is included. Ctrl+P produces the A4 landscape PDF with every
  diagram frozen in its finished state and no figure split across a page.
- The page is an internal engineering standard, so `vercel.json` asks search engines
  not to index it. That is a request to crawlers, not access control. To restrict who
  can read it, use Vercel Authentication under Settings → Deployment Protection.
