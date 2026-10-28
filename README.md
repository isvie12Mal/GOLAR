# SKG FOOTBALL AR PENALTY KICK V1

3D procedural stadium with Three.js, MediaPipe Pose Landmarker foot motion recognition, AR video inset, 5 penalties, keeper saves, sound effects and Google Sheets leaderboard.

## Deploy on Vercel
1. Extract this ZIP. Open https://vercel.com/new and import the folder via GitHub, **or** install Vercel CLI and run `npx vercel --prod` inside this folder.
2. Framework preset: **Other**. No build command. Output directory: project root (leave blank).
3. Open HTTPS URL, provide camera permission, ensure the entire body including ankles is visible.
4. For development run `python -m http.server 8080` and open http://localhost:8080; localhost camera permission works in supported browsers. Do NOT double-click index.html using file:// due to module restrictions.

## Set up Google Sheets + Apps Script
1. Create a Google Sheet named `SKG FOOTBALL AR LEADERBOARD`.
2. Open **Extensions > Apps Script** from that spreadsheet.
3. Replace Code.gs with the supplied `Code.gs` file contents; save.
4. Choose function **setup** then **Run**, approve permissions; the `LEADERBOARD` sheet is created.
5. Choose **Deploy > New deployment > Web app**; Execute as: **Me**; Who has access: **Anyone** (if school admin allows). Click Deploy and copy `/exec` URL.
6. Open `config.js`, paste the URL in `GAS_URL = 'https://script.google.com/macros/s/.../exec'`.
7. Redeploy Vercel (new project deployment). Shoot 5 times and check Google Sheet for a new row; leaderboard automatically reads latest Top 10.
8. For backend modifications, use Deploy > Manage deployments > Edit > New version > Deploy; retain the /exec URL.

## Controls
- Foot AR: select **PLAY WITH FOOT AR**, stand 2–3m from a stable camera with legs visible. Move a leg sideways to aim; raise/swing one ankle upward sharply to trigger a kick. MediaPipe estimates 2D leg motion; depth of a real foot kick is **not precisely measurable** with one camera. For smaller children, touch mode is more reliable.
- Touch: click/tap on the stadium to adjust direction, press KICK.
- Keyboard: left/right arrows and SPACE.
- If model download/GPU fails, app attempts CPU; if permissions/model fail, touch/keyboard mode remains available.

## Notes and limitations
- Video processing occurs in browser. The app does not upload videos, photos or skeletal tracking data.
- MediaPipe/Three.js/fonts are CDN-loaded and require internet. The AR model is downloaded from Google CDN.
- Shot outcomes incorporate random keeper behaviour by difficulty. It is a **game**, not a measurement of real kick accuracy.
- GAS handles public score submissions by cross-origin HTML form POST and fetches leaderboard by JSONP GET. A successful POST cannot be confirmed by the game using this transport; check spreadsheet to verify. Users can view or spoof submitted scores; do not use as trusted exam or competition data without authenticated backend and anti-cheat protection.
- Publishing an Apps Script web app as **Anyone** makes its endpoint public. This may be blocked by Workspace administrative policy. Avoid students' full names if data minimization is needed; use nicknames/ID. Do not share the Sheet's edit link with students.
- For high traffic or competition-grade ranking, replace the public GAS endpoint with an authenticated server or trusted write proxy.


## V1.1 — URL leaderboard disambungkan
`config.js` telah dimasukkan URL Web App pengguna. Jika Web App organisasi memerlukan akaun moe-dl.edu.my, akses leaderboard daripada pemain luar organisasi mungkin gagal. Uji simpan rekod dan leaderboard selepas deployment.

## V1.2 — pembetulan gagal import MediaPipe
- Import lama `@mediapipe/tasks-vision@0.10.22/+esm` diganti dengan pakej `vision_bundle.mjs`.
- Cuba **jsDelivr**, kemudian **unpkg** jika gagal, termasuk fail WASM daripada hos yang sepadan.
- Jika GPU gagal, cuba CPU; butang kamera menjadi `RETRY AR` jika gagal.
- Jika kedua-dua CDN disekat (contohnya Wi-Fi sekolah), tukar rangkaian atau hoskan aset MediaPipe secara setempat. Versi ini masih memerlukan internet bagi model dan library Three.js.
- Sambungan Apps Script dalam `config.js` dikekalkan.
- Selepas deploy, buat hard refresh **Ctrl+Shift+R** agar kod baharu dimuatkan.


### V1.3 — Keeper Visible
- Keeper is moved forward, scaled 1.42x and gets visible eyes, eyebrows, nose, mouth, hair, ear, neon gloves, raised ready arms and chest badge.
- Updated camera aim. Existing Google Apps Script URL remains in `config.js`.
- To update GitHub: extract ZIP, visit the same repository, choose Add file > Upload files, drag the seven files (not the ZIP), then Commit changes to main. If Vercel is connected it redeploys automatically.
