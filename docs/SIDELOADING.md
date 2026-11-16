# Sideloading

## Excel (Office.js add-in)

### What it needs

- **Excel on Windows or Mac** (Microsoft 365, or Excel 2016 and later). Excel on the web can't reach a program on the user's computer, so this add-in is desktop only.
- **The tool serving the add-in over HTTPS.** Office loads add-in pages over HTTPS only, including on localhost. The tool serves `excel/` (with `assets/`) at `https://localhost:<ADDIN_PORT>/addins/excel/` and answers its API on the same origin.
- **A certificate for `localhost` that the computer trusts.** For development, Microsoft's tool makes one:

  ```
  npx office-addin-dev-certs install
  ```

  It creates `localhost.crt` and `localhost.key` in `%USERPROFILE%\.office-addin-dev-certs\` and installs a development certificate authority in your user's trusted root store (Windows asks first). The certificate lasts 30 days; run the command again to renew it. The tool then serves HTTPS with those files, for example uvicorn's `--ssl-certfile` and `--ssl-keyfile`.

**Before shipping to users:** installing a certificate authority on every user's computer is a security decision, not a packaging detail. Decide it before a tool ships an add-in. The alternative is to host the add-in pages on a public HTTPS site and have them call the tool on localhost; that needs CORS on the tool and has to be tested against the browser's local-network rules.

### Load it in Excel

**Windows** (Microsoft's method for desktop Excel is a trusted shared-folder catalog):

1. Put `manifest.xml` in a folder and share it (right-click > Properties > Sharing > Share). Note the network path, e.g. `\\YOUR-PC\addins`.
2. Excel > File > Options > Trust Center > Trust Center Settings > Trusted Add-in Catalogs: enter the network path, **Add catalog**, tick **Show in Menu**, OK, and restart Excel.
3. Home > Add-ins > More Add-ins > **SHARED FOLDER**, choose the add-in, **Add**.

**Mac:** copy `manifest.xml` to `~/Library/Containers/com.microsoft.Excel/Data/Documents/wef/` (create `wef` if it's missing) and restart Excel. The add-in is under Home > Add-ins.

**Then:** start the tool, and click the tool's button in the **Yoraito** group on the Home tab. The task pane says "Ready." when it can reach the tool.

**Organisations** can deploy the manifest to their users from the Microsoft 365 admin center (Settings > Integrated apps) instead of sideloading.

### Remove it

Windows: remove the catalog in the Trust Center and restart Excel. Mac: delete the manifest from the `wef` folder.

## Google Sheets (Apps Script)

1. Open the Google Sheet, then Extensions > Apps Script.
2. Paste the contents of `Code.gs`, save, and reload the sheet.
3. Use the menu **<tool name> > Open <tool name>**. It shows a link that opens the tool in your browser.

Apps Script runs on Google's servers and can't reach your computer, so the script never calls the tool; it only shows the link. To use the sheet's data in the tool, download it first (File > Download > Microsoft Excel (.xlsx)) and open it there.
