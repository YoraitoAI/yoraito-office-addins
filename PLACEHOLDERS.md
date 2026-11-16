# Placeholders

Replace these in every `.template` file, then drop the `.template` suffix.

| Placeholder | Meaning | Example (model-diff) | Example (recon) |
|---|---|---|---|
| `__TOOL_NAME__` | Display name | `Yoraito Model Diff` | `Yoraito Recon` |
| `__TOOL_ID__` | Lowercase and hyphenated, as in the tool's repository name | `yoraito-model-diff` | `yoraito-recon` |
| `__TOOL_DESCRIPTION__` | One short sentence, without a full stop (the task pane adds one) | `Compare this workbook with another version` | `Reconcile this workbook against a statement` |
| `__PORT__` | The tool's local web app (http), for the Google Sheets link | `17842` | `17843` |
| `__ADDIN_PORT__` | The HTTPS port where the tool serves the Excel add-in and its API | `17852` | `17853` |
| `__API_ENDPOINT__` | The route the task pane POSTs to: the workbook as `workbook`, and a picked file as `file` | `/api/diff` | `/api/match` |
| `__ACTION_LABEL__` | The task pane's button | `Compare with another file` | `Run reconciliation` |
| `__NEEDS_FILE__` | `true` if the action also needs a file the user picks, else `false` | `true` | `true` |
| `__FILE_ACCEPT__` | File types for that picker | `.xlsx` | `.csv,.xlsx,.pdf` |
| `__ADDIN_ID__` | A new GUID for the add-in, e.g. from PowerShell `[guid]::NewGuid()` | (generate) | (generate) |

## Files

| Template | Becomes | Served at |
|---|---|---|
| `excel/manifest.xml.template` | `manifest.xml` | not served: it's what Excel loads (see [docs/SIDELOADING.md](docs/SIDELOADING.md)) |
| `excel/taskpane.html.template` | `taskpane.html` | `https://localhost:__ADDIN_PORT__/addins/excel/taskpane.html` |
| `excel/commands.html.template` | `commands.html` | `https://localhost:__ADDIN_PORT__/addins/excel/commands.html` |
| `excel/assets/icon-*.png` | as they are, or the tool's own icons in the same sizes | `https://localhost:__ADDIN_PORT__/addins/excel/assets/` |
| `sheets/Code.gs.template` | `Code.gs` | pasted into the sheet's Apps Script |

## The tool's side

- **Answer `GET /api/health`** on the add-in origin; the task pane checks it.
- **Answer `__API_ENDPOINT__`** with JSON. `message` is shown to the user; `url` (optional, relative) is where the "Open" link points; `detail` is shown on errors.
- **If the API needs yoraito-core's install key**, serve `taskpane.html` with the key in its `yoraito-key` meta tag. The page sends it as `X-Yoraito-Key`.
