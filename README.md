# SKG Football AR Penalty V1.4 — Local MediaPipe + Keeper Fix

## Apa yang dibaiki
- MediaPipe JavaScript dan WASM **dipasang semasa build Vercel** melalui npm dan dihidang dari domain game sendiri (`/vendor/`). Tiada import jsDelivr / unpkg untuk AR.
- Skrip build cuba muat turun model pose `.task` ke `/vendor/` semasa deployment. Jika tidak berjaya, model masih memerlukan Google Storage pada masa bermain dan mesej ralat akan dipaparkan.
- Kamera game didekatkan, penjaga gol berada lebih hampir dan stadium di belakang gawang dijauhkan supaya muka, badan dan sarung tangan lebih kelihatan.
- `config.js` mengekalkan URL Google Apps Script lama.

## KEMAS KINI GITHUB & VERCEL (PENTING)
1. Extract ZIP. Buka repo GitHub lama (branch deploy, biasanya `main`). Upload **semua fail dan folder** daripada ZIP: `index.html`, `game.js`, `style.css`, `config.js`, `Code.gs`, `vercel.json`, `package.json`, `README.md`, dan folder `scripts/` dengan `build.mjs`. **Jangan upload ZIP sahaja**.
2. Tekan `Commit changes`. Pastikan folder `scripts/build.mjs` ada di root repo.
3. Vercel → Project → Settings → Build and Deployment: Framework Preset **Other**; Build Command `npm run build` (atau ikut `vercel.json`), Output Directory `dist`; Root Directory kosong jika fail ada di root.
4. Vercel → Deployments → buka deployment terbaru; `npm install` harus memasang `@mediapipe/tasks-vision` dan log build patut menyebut `Built dist with MediaPipe JS + WASM`.
5. Buka website HTTPS, hard refresh `Ctrl+Shift+R`, mulakan FOOT AR, beri akses kamera. Pastikan seluruh badan termasuk kedua-dua kaki terlihat dan lampu terang.
6. Jika Vercel gagal build, ambil screenshot **build logs**. Jika AR masih gagal, buka browser Console (F12) dan ambil mesej ralat. Periksa `https://YOUR-APP.vercel.app/vendor/vision_bundle.mjs` boleh dibuka.

## Penting
- ZIP ini ialah **source project** yang memerlukan `npm install` dan `npm run build` di Vercel. Ia tidak mengandungi binari MediaPipe kerana dependency tersebut dipasang oleh Vercel. Penjanaan bundle tidak dapat diuji dalam persekitaran ini tanpa akses npm; semak Vercel build logs.
- Three.js masih diimport melalui jsDelivr kerana stadium sudah berfungsi pada screenshot. Jika CDN Three.js turut disekat, ia perlu dilokalkan juga.
- Ini AR melalui kamera inset: pose estimates 2D, bukan fizikal sebenar bola. Touch mode masih boleh digunakan.
- Sheets dikendalikan oleh `Code.gs` sama seperti versi dahulu. Periksa helaian untuk pengesahan rekod; submit form silang domain tidak memberi acknowledgement yang boleh dipercayai.
