# 🐻 Google Sheets RSVP Setup Guide

Follow these step-by-step instructions to connect your baby shower website to a Google Sheet so every RSVP is automatically saved. No coding experience required!

---

## Step 1 — Create the Google Sheet

1. Go to [sheets.google.com](https://sheets.google.com) and sign in with your Google account.
2. Click the **+** button (or "Blank spreadsheet") to create a new sheet.
3. Name it **Baby Shower RSVPs** by clicking "Untitled spreadsheet" at the top and typing the new name.
4. In the very first row, type these column headers exactly (one per cell, starting at A1):

   | A | B | C | D | E | F | G |
   |---|---|---|---|---|---|---|
   | Timestamp | Name | Email | Guests | Attending | Dietary | Message |

5. Your sheet is ready. Leave it open in this tab.

---

## Step 2 — Open the Apps Script Editor

1. In your Google Sheet, click the top menu: **Extensions → Apps Script**
2. A new tab will open with a code editor. You'll see a default `function myFunction() { }` — delete it completely.
3. Paste the following code into the editor:

```javascript
function doPost(e) {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  var data = JSON.parse(e.postData.contents);
  sheet.appendRow([
    new Date(),
    data.name,
    data.email,
    data.guests,
    data.attending,
    data.dietary,
    data.message
  ]);
  return ContentService
    .createTextOutput(JSON.stringify({result: 'success'}))
    .setMimeType(ContentService.MimeType.JSON);
}
```

4. Click the **floppy disk icon** (or press Ctrl+S / Cmd+S) to save. Name your project **"Baby Shower RSVP"** when prompted.

---

## Step 3 — Deploy as a Web App

1. In the Apps Script editor, click the blue **"Deploy"** button (top right).
2. Choose **"New deployment"** from the dropdown.
3. Click the gear icon ⚙️ next to "Select type" and choose **Web app**.
4. Fill in the settings:
   - **Description:** Baby Shower RSVP Handler
   - **Execute as:** Me _(your Google account)_
   - **Who has access:** Anyone
5. Click **"Deploy"**.
6. Google will ask you to **authorize** the app — click "Authorize access", choose your Google account, and click "Allow" on the permissions screen.
7. After deploying, you'll see a screen that says **"Web app URL"** — copy that URL. It looks like:
   ```
   https://script.google.com/macros/s/AKfycb.../exec
   ```

---

## Step 4 — Add the URL to Your Website

1. Open `index.html` in any text editor (Notepad, VS Code, etc.).
2. Find this line near the top of the `<script>` section (search for `GOOGLE_SCRIPT_URL`):
   ```javascript
   const GOOGLE_SCRIPT_URL = 'YOUR_GOOGLE_APPS_SCRIPT_URL_HERE';
   ```
3. Replace `YOUR_GOOGLE_APPS_SCRIPT_URL_HERE` with the URL you copied in Step 3, keeping the single quotes:
   ```javascript
   const GOOGLE_SCRIPT_URL = 'https://script.google.com/macros/s/AKfycb.../exec';
   ```
4. Save the file.

---

## Step 5 — Test It

1. Open the website in your browser (or visit the GitHub Pages URL).
2. Fill out the RSVP form and click **Send My RSVP**.
3. Go back to your Google Sheet — within a few seconds you should see a new row with the RSVP data!

---

## Viewing RSVPs

Simply open your **Baby Shower RSVPs** Google Sheet at any time to see all submitted RSVPs. Each row is:

| Timestamp | Name | Email | Guests | Attending | Dietary | Message |
|-----------|------|-------|--------|-----------|---------|---------|
| Aug 1, 9:14 AM | Jane Smith | jane@… | 2 | Yes | None | Can't wait! |

You can also use Google Sheets features like:
- **Filter** by "Attending = Yes" to get a headcount
- **Sum** the Guests column for total attendees
- **Download as Excel** to share with your caterer

---

## Troubleshooting

**RSVPs aren't appearing in the sheet:**
- Make sure you deployed with **"Who has access: Anyone"** (not "Anyone with Google account")
- Re-deploy: in Apps Script, click Deploy → Manage deployments → Edit → create a New version → Deploy

**Getting an error on the website:**
- Double-check the URL in `index.html` — it should end in `/exec`
- Make sure you didn't accidentally remove the surrounding single quotes

**"Authorization required" error:**
- Run the `doPost` function manually once from the Apps Script editor (click ▶ Run) to trigger the authorization prompt, then re-deploy.

---

*Need help? Have a tech-savvy friend look at this guide — it only takes about 10 minutes to set up!*
