# expense-tracker

## Platform-independent PIN + cloud backup setup

This app supports optional cloud sync to:
- **GitHub Gist** (primary)
- **Google Sheets (Apps Script Web App)** (backup)

If cloud is configured, PIN hash + data are synced so you can use **same PIN on laptop and mobile**.

## 1) Add runtime config in your deployed page

Add this before the app script runs:

```html
<script>
  window.MY_APP_TOKEN = 'github_pat_xxx';            // optional if using Gist
  window.GS_WEBAPP_URL = 'https://script.google.com/macros/s/XXX/exec'; // optional
  window.GS_SYNC_KEY = 'my-private-key';             // required for Sheets API lock
</script>
```

## 2) Google Sheets Apps Script (one-time setup)

1. Create a Google Sheet.
2. Extensions → **Apps Script**.
3. Paste this script:

```javascript
const SHEET_NAME = 'kharcha';
const PROP_KEY = 'KHARCHA_PAYLOAD';
const SECRET = 'my-private-key'; // same as window.GS_SYNC_KEY

function doPost(e) {
  try {
    const body = JSON.parse(e.postData.contents || '{}');
    if ((body.key || '') !== SECRET) return json({ ok:false, error:'unauthorized' }, 401);

    const props = PropertiesService.getScriptProperties();

    if (body.action === 'pull') {
      const raw = props.getProperty(PROP_KEY) || '{}';
      return json({ ok:true, data: JSON.parse(raw) });
    }

    if (body.action === 'push') {
      const payload = body.payload || {};
      props.setProperty(PROP_KEY, JSON.stringify(payload));
      writeSnapshotToSheet(payload);
      return json({ ok:true });
    }

    return json({ ok:false, error:'invalid action' }, 400);
  } catch (err) {
    return json({ ok:false, error:String(err) }, 500);
  }
}

function writeSnapshotToSheet(payload) {
  const ss = SpreadsheetApp.getActiveSpreadsheet();
  const sh = ss.getSheetByName(SHEET_NAME) || ss.insertSheet(SHEET_NAME);
  sh.clear();
  sh.getRange(1,1,1,8).setValues([['Date','Description','Amount','Tag','Payment','Cash','Online','Note']]);
  const rows = (payload.expenses || []).map(e => [
    e.date || '', e.desc || '', Number(e.amt||0), e.tag || '', e.payM || '', Number(e.ca||0), Number(e.oa||0), e.note || ''
  ]);
  if (rows.length) sh.getRange(2,1,rows.length,8).setValues(rows);
}

function json(obj, code) {
  return ContentService
    .createTextOutput(JSON.stringify(obj))
    .setMimeType(ContentService.MimeType.JSON);
}
```

4. Deploy → **New deployment** → type **Web app**:
   - Execute as: **Me**
   - Who has access: **Anyone**
5. Copy Web App URL and set it in `window.GS_WEBAPP_URL`.
6. Keep `SECRET` and `window.GS_SYNC_KEY` exactly same.

## 3) Verify cross-device behavior

1. Open on laptop, set PIN (e.g., `1234`), add 1 expense.
2. Press **Sync** once.
3. Open on mobile with same deployed URL.
4. Enter `1234`.
5. Data should load after sync.

## Notes
- App auto-syncs every ~2 minutes while unlocked + when tab becomes active/online.
- If cloud is unavailable, app still works in local cache mode.
