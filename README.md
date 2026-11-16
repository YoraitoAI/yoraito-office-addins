# yoraito-office-addins

Shared templates for Yoraito tools that add a button to Excel or a menu to Google Sheets.

| | What it is | Where it runs |
|---|---|---|
| **Excel add-in** (`excel/`) | A ribbon button (Home tab, "Yoraito" group) that opens a task pane. The pane sends the open workbook to the tool on this computer and shows the result. | Excel on Windows and Mac. The tool serves the pane over HTTPS on localhost. |
| **Google Sheets launcher** (`sheets/`) | A menu item that shows a link to the tool on the user's computer. | Apps Script runs on Google's servers and can't reach the user's computer, so it only links. |

## Use it in a tool

1. Copy `excel/` (and `sheets/` if wanted) into the tool's `addins/` folder.
2. Replace the placeholders and drop the `.template` suffixes ([PLACEHOLDERS.md](PLACEHOLDERS.md)).
3. Have the tool serve `addins/excel/` over HTTPS and answer the health route and the action route ([PLACEHOLDERS.md](PLACEHOLDERS.md), "The tool's side").
4. Load the add-in in Excel ([docs/SIDELOADING.md](docs/SIDELOADING.md)).

The HTTPS requirement is Office's, and it applies on localhost too. How users' computers get a trusted certificate is a decision to make before a tool ships its add-in; [docs/SIDELOADING.md](docs/SIDELOADING.md) has the options.

## Which tools

An add-in helps where people already work in Excel: model-diff, the FP&A model, recon, reporting.

yoraito-sync doesn't need one. Its Excel workbooks refresh through Power Query with no add-in, Excel for the web gets pushes through Microsoft Graph, and it writes to Google Sheets through the Sheets API.

## Publishing

See [docs/PUBLISHING.md](docs/PUBLISHING.md). For firms, a Microsoft 365 admin can deploy the manifest centrally; AppSource needs a hosted version.

## License

MIT, see [LICENSE](LICENSE).
