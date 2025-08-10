
# Nowify — GitHub Pages Edition (Single File)

A self-contained HTML page that shows your Spotify **Now Playing** with album art and an adaptive background. Uses **Authorization Code with PKCE** entirely in the browser (no server).

## Quick Deploy on GitHub Pages

1. **Create a new public repo** on GitHub, e.g. `nowify-pages`.
2. Add this file as `index.html` to the repo and commit to `main`.
3. In the repo: **Settings → Pages → Build and deployment → Source: Deploy from branch**.  
   - Branch: `main`  
   - Folder: `/ (root)`  
   - Save. Wait 30–90 seconds for the first deploy.
4. Your site will appear at:  
   `https://USERNAME.github.io/REPO/`  
   (Example: `https://wouterstomp.github.io/nowify-pages/`)
5. In **Spotify Developer Dashboard → Your App → Edit Settings → Redirect URIs**, add the **exact** Pages URL from step 4. Include the trailing slash.
6. Visit your Pages URL. In the app UI:
   - Paste your **Spotify Client ID**.
   - Ensure the **Redirect URI** shown matches the Pages URL from step 4 (it auto-fills).
   - Click **Save**, then **Log in with Spotify** and authorize.

## Notes
- Tokens are stored in your browser's **localStorage** on this device only.
- To move devices or browsers, repeat the login.
- If you change the domain (e.g., add a custom domain), add the new **exact** HTTPS URL in Spotify → Redirect URIs as well.

## Troubleshooting
- **INVALID_CLIENT / redirect_uri_mismatch**: The Redirect URI in Spotify must match **exactly** (including trailing slash) what the page shows in the Redirect URI input.
- **Blank screen after login**: Check the browser console for errors; make sure the app ID is correct and scopes are set. Try force-refresh (Ctrl/Cmd+Shift+R).
- **Nothing playing**: Spotify returns 204 when no active playback. Start a track on any device and wait a few seconds.
