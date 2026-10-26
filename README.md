# Queens Solver router

A permanent address for **Queens Solver**, Joey Wilkes's Queens puzzle solver. It
redirects immediately to wherever the app is hosted, so links and QR codes keep
working when the host changes.

- Public address: https://joeywilkes12.github.io/queens-solver-router/
- Current destination: https://queens-solver-jw.vercel.app/ (Vercel Container Runtime)
- Rollback destination: https://queens-solver.replit.app/ (Replit Autoscale)
- Repository: https://github.com/JoeyWilkes12/queens-solver-router
- QR assets: `queens-solver-router-qr.png` (1176 × 1176 pixels, 300 DPI, black on
  white, high error correction) and `queens-solver-router-qr.svg`. Both encode the
  router address, not the destination.

Environment role: routes to the **Production** Queens Solver deployment on
Vercel. Agents: see [AGENTS.md](AGENTS.md).

Built from the [personal-website-router](https://github.com/JoeyWilkes12/personal-website-router)
template. See the [maintenance guide](MAINTENANCE.md) for changing or reverting
the destination, validation, commit/push commands, PR approval, and publication.

## Who links here

Link to the router address, not the host, anywhere the link should survive a
host change:

- The Portfolio page of Joey Wilkes's personal website.
- Printed or shared QR codes.

Changing the destination here updates every one of those without republishing
the personal website.

## Change the destination

Edit only the `redirect_url` value at the top of `index.html`:

```yaml
redirect_url: "https://queens-solver-jw.vercel.app/"
```

Commit and push a feature branch, then open a PR. After you approve and merge it
into `main`, GitHub Pages runs Jekyll automatically and replaces every
`page.redirect_url` reference with that value. This updates the JavaScript
redirect, HTML refresh, fallback link, canonical link, and structured metadata
together. Keep the URL in double quotes and use an absolute HTTPS address.

JavaScript uses `location.replace()` so the browser's Back button doesn't loop
through the router. The HTML refresh also works with JavaScript disabled. The
visible link provides a manual way to continue if automatic navigation is blocked.
This is a browser redirect served with HTTP 200, rather than an HTTP 301/302.

Keep the repository name and Pages address stable. Allow GitHub Pages a few
minutes to publish a push.

## Publishing and checks

GitHub Pages publishes the root of the `main` branch with its built-in Jekyll build.
Do not add `.nojekyll`: it would disable the URL substitutions. Opening the source
HTML directly also skips Jekyll; preview the generated site instead.

Run the automated hyperlink and generated-content regression check before a
release, supplying a rendered local preview URL, then verify the public deployment.
The maintenance guide includes a complete preview setup using
`scripts/render_preview.rb`:

```sh
python3 scripts/check_links.py --site-url http://127.0.0.1:4179/queens-solver-router/
python3 scripts/check_links.py
```

The checker follows HTTP redirects, fails on HTTP 4xx/5xx, and checks the published
redirect destinations, metadata, sitemap, robots file, and both QR files. Browser
regression coverage checks immediate navigation with and without JavaScript,
Back-button behavior, the fallback link, keyboard focus, and overflow at 390px
and 1440px. With Playwright CLI open on that localhost preview, run
`run-code --filename scripts/browser_check.js`. The test substitutes a local
destination so the browser does not visit external sites.

`robots.txt` allows public content. Because this is a GitHub project site, its file
is under the project path; domain-wide crawler rules belong to the account's root
site. The canonical URL points crawlers to the current destination.

## QR source

Regenerate the QR files with the QR Code Generator skill only if the stable
Pages address changes:

```sh
python3 ~/.claude/skills/qr-code-generator/scripts/generate_qr.py \
  "https://joeywilkes12.github.io/queens-solver-router/" \
  --name queens-solver-router-qr --formats png,svg --box-size 24 --output-dir .
```

The four-module white border is the required quiet zone; preserve it when
printing or placing the image.
