# Home Assistant Add-ons

Personal fork of the official [hassio-addons/addon-tailscale](https://github.com/hassio-addons/addon-tailscale)
add-on, with a GitHub Action that checks daily for new Tailscale releases and
bumps the bundled version automatically — so updates show up in Home Assistant
within ~24 hours instead of waiting on the upstream maintainers.

## Installation

1. In Home Assistant: **Settings → Add-ons → Add-on Store → ⋮ (top right) → Repositories**
2. Add: `https://github.com/YOUR_USERNAME/ha-addons`
3. Install **Tailscale** from this repository (it will show up as a separate
   add-on from the official one — uninstall the official one first if you
   want to avoid confusion, and reconfigure this one with the same options).

## How the auto-update works

`.github/workflows/update-tailscale.yml` runs daily:

1. Checks the latest release at `tailscale/tailscale` on GitHub.
2. Compares it to the version currently pinned in `tailscale/Dockerfile`.
3. If newer, updates the `Dockerfile` and bumps `tailscale/config.yaml`'s
   `version:` to match, then commits and pushes.
4. Home Assistant picks up the new commit as a normal add-on update — click
   **Update** like any other add-on.

## Maintenance

This is a personal fork, not an actively maintained community project. If the
upstream `hassio-addons/addon-tailscale` repo changes its file layout, the
workflow's `sed`/`grep` patterns may need updating. Check
`.github/workflows/update-tailscale.yml` runs are succeeding under the
**Actions** tab periodically.
