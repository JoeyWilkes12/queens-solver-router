# Queens Solver router: agent instructions

This repository is the stable public address (and QR code) for **Queens
Solver**, Joey Wilkes's Queens puzzle solver. GitHub Pages renders `index.html`,
which redirects visitors to wherever the app is hosted. The personal website's
Portfolio links here, not to the app host.

## Environments

| Environment | Address | Role here |
| --- | --- | --- |
| Dev | Local Liquid preview, also shared on the owner's tailnet | Render and check changes before a PR |
| Production destination | https://queens-solver.replit.app/ (Replit Autoscale) | The destination on `main` |

The personal website's own Dev, Test, Staging, and Production environments all
link to this router. The full environment reference lives in the owner's
private source repository.

## Rules

- Change only `redirect_url` at the top of `index.html`; keep it an absolute
  HTTPS URL in double quotes. The QR files never change.
- Work on a feature branch or worktree and open a PR. Merge, or push to `main`,
  only with the owner's explicit approval for that specific change: `main` is
  what GitHub Pages publishes.
- Before a PR, render the preview and run `scripts/check_links.py` and
  `scripts/browser_check.js` as described in [MAINTENANCE.md](MAINTENANCE.md).
- Share any local preview on the owner's tailnet
  (`Tailscale serve --bg --http=<port> <port>`) so it can be reviewed from a
  phone.
