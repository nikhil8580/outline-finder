# Outline Finder

Single-page tool (`index.html`) that scans your Google Drive for course outlines and moves the ones you
confirm into the Content Repository's Outlines folder.

## Setup
1. In Google Cloud Console, create an OAuth client of type **Web application** and enable the **Drive API**.
2. Add the origin you serve the page from (e.g. `http://localhost:8000`) to *Authorized JavaScript origins*.
3. Set `CONFIG.clientId` in `index.html`.
4. Serve the folder (`python3 -m http.server 8000`) and open it.

## How it works
- Searches Docs and PDFs for 5 keywords in parallel; keeps files matching >= 3.
- Google Docs are verified by reading their text: keywords must appear as headings/labels. PDFs are marked *unverified*.
- Files already in the Outlines / KB Articles folders (or their subfolders) are skipped.
- Selected files are moved with the Drive API; failures are shown per file and can be retried.
- Uses the full `drive` scope because moving files you did not create requires it.
