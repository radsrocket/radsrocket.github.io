# Nowify (Kiosk, GitHub Pages)

A single-file, GitHub Pages–friendly **Now Playing** display for Spotify that’s optimized for a Raspberry Pi kiosk.

- Auth: **Authorization Code with PKCE** (client-side only; no server).
- Storage: **localStorage** (`nowify_cfg`) on your GitHub Pages origin.
- Display: album art (left), big title + artist (right), **smooth** progress bar.
- Behavior: **screen goes black** when paused or nothing is playing; subtle network notice on outages.

## Quick start

1. Create (or open) a **public** GitHub repo for Pages.
2. Put this `index.html` at repo root and commit to the default branch.
3. In repo **Settings → Pages**, pick **Deploy from branch**, `main`, folder **/**.
4. Visit your Pages URL (e.g. `https://USERNAME.github.io/REPO/`).

## Spotify app setup

1. Go to the [Spotify Developer Dashboard](https://developer.spotify.com/dashboard/).
2. Create an app (or open your existing one).
3. **Edit Settings → Redirect URIs** → add your exact Pages URL, including trailing slash  
   e.g. `https://USERNAME.github.io/REPO/`
4. Copy the **Client ID**.

## First run

- Open your Pages URL.
- Press **`s`** to open **Settings**.
- Paste **Client ID** and confirm **Redirect URI** (it auto-fills to your current page).
- Click **Log in with Spotify** and finish the flow.
- After success, the small gear hides; press **`s`** anytime to reopen Settings.

## Tokens & privacy

- **Access token**: short-lived (~1 hour) and refreshed automatically.
- **Refresh token**: stored only in your browser’s localStorage on your Pages origin.
- Nothing is sent to any server other than Spotify’s APIs.

If you clear site data, switch browsers, or change Profiles, you’ll need to log in again.

## Display behavior

- **Paused / Nothing playing** → full **black screen** (great for TV/OLED).
- **Network issues** → after ~15s of consecutive failures, a centered grey notice appears; it hides automatically upon recovery.
- **Progress bar** → thinner (18px), the **remaining part is solid light grey**; fill animates smoothly between polls.
- **Text fitting** → title can use up to **3 lines**, artist up to **2 lines**; it shrinks font size before truncating.

## Raspberry Pi tips

Chromium kiosk launch (replace URL):
```bash
chromium-browser --kiosk --disable-infobars --check-for-update-interval=31536000 \
  --noerrdialogs --disable-session-crashed-bubble --autoplay-policy=no-user-gesture-required \
  https://USERNAME.github.io/REPO/
```

Optional auto-start (LXDE autostart):
```
sudo nano /etc/xdg/lxsession/LXDE-pi/autostart
```
Add:
```
@chromium-browser --kiosk https://USERNAME.github.io/REPO/
```

## Troubleshooting

- **“Invalid redirect URI”** → the URL in Spotify settings must match your Pages URL exactly (including trailing slash).
- **Stuck after login** → open **Settings (s)** and confirm Client ID + Redirect URI; try a hard refresh.
- **Looks cached** → hard reload (Ctrl/Cmd+Shift+R) or clear site data.
- **Blank screen** → you might be paused or nothing is playing; press **s** to bring up Settings.
- **Network notice won’t go away** → check connectivity; it clears on the next successful poll.

## Development

Everything is in `index.html`. No build step. If you want to iterate locally, run a simple file server and open it with a file URL or `http://localhost` (remember: your Spotify **Redirect URI** must include that local URL if you test the login flow locally).

---

MIT-style use. Attribution appreciated.
