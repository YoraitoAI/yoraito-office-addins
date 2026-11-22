# The local contract an add-in expects

This repository is a template for Excel (Office.js) and Google Sheets (Apps Script). It contains no
Python, and it should not gain any. The tool on the user's machine provides the contract.

## Excel

The pane is served over HTTPS by the tool on 127.0.0.1. The tool should provide:

- `GET /health` returns `200` with `{"ok": true, "tool": "<id>", "version": "<version>"}`.
- `POST /action` accepts the pane's JSON and returns JSON.

Guard every request with `yoraito_core.localapi` and `yoraito_core.installkey`:

- Host allowlist for `127.0.0.1` and `localhost`.
- Origin allowlist for the pane.
- `X-Yoraito-Key` with the per-install key for non-browser clients, and the session cookie for the
  pane the tool serves itself.
- No CORS.

HTTPS on localhost needs a trusted certificate. Decide the story before shipping: a local CA the
installer trusts, or a loopback certificate the tool manages. Put it in the tool's install guide.

Store tool data with `yoraito_core.paths.app_dir("<tool>")`.

## Google Sheets

Apps Script runs on Google's servers and cannot reach 127.0.0.1. The Sheets launcher only links to
the tool. Do not imply that it calls the local daemon.

## Why there is no core code here

This template is copied into every tool. A second copy of the guard, key handling or paths would
drift from core. The template states the contract; the tool implements it with core.

## Checklist

- [ ] HTTPS on localhost with a trusted certificate.
- [ ] `GET /health` and `POST /action`.
- [ ] Host and Origin allowlist.
- [ ] `X-Yoraito-Key` from `installkey`, and the session cookie for the pane.
- [ ] Data under `paths.app_dir("<tool>")`.
- [ ] The Sheets launcher only links.
