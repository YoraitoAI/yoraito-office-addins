# Publishing

## Excel

**Firms (recommended):** a firm's Microsoft 365 admin deploys the manifest to its users from the admin center (Settings > Integrated apps). Nothing is published; the add-in still needs the tool running on each computer and the HTTPS setup in [SIDELOADING.md](SIDELOADING.md).

**Microsoft AppSource:** needs the add-in's pages on a public HTTPS host, a Microsoft Partner Center account, and an add-in that works for the reviewers. An add-in that only works with a program running on the user's computer has to say so clearly and may not pass review. To submit:

1. Host the `excel/` files on an HTTPS site and change every `https://localhost:<ADDIN_PORT>` URL in `manifest.xml` to that site.
2. Decide how the hosted page reaches the tool on the user's computer (CORS on the tool, and the browser's local-network rules), and test it.
3. Submit the manifest in Partner Center (https://partner.microsoft.com) as an Office add-in.

## Google Sheets

Publishing to the Google Workspace Marketplace needs a Google Cloud project, an OAuth consent screen and an Apps Script deployment of type "Add-on", followed by Google's review.

The script here is a launcher: a menu item that shows a link to the tool on the user's computer. Sharing the script with each firm (or pasting it per sheet, as in [SIDELOADING.md](SIDELOADING.md)) is enough until there's a reason to publish it.
