# expense-tracker

## Cloud setup (cross-device + backup)

This app now supports two optional cloud sync targets:

- **GitHub Gist** (primary sync)
- **Google Sheets via Apps Script Web App** (backup sync)

Add these globals before loading the app script (or in a small `<script>` tag in `index.html` head):

```html
<script>
  window.MY_APP_TOKEN = 'github_pat_xxx';
  window.GS_WEBAPP_URL = 'https://script.google.com/macros/s/xxx/exec';
  window.GS_SYNC_KEY = 'your-shared-secret';
</script>
```

### Notes
- If a local PIN is missing, app tries cloud payload and reuses `pinHash` so login works across devices.
- Google Sheets sync expects Apps Script endpoint to support JSON POST:
  - `{ action: 'pull', key }` -> returns `{ data: { expenses, tags, pinHash, updatedAt } }`
  - `{ action: 'push', key, payload }` -> returns HTTP 200 on success.
- If cloud is unavailable, app continues in local-cache mode.
