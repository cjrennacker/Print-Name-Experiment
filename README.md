# Print Title Search Task

A browser-based yes/no signal detection study for HSE 540. Participants read a print title, see one flashed
screenful of a gallery page (a 3 x 3 grid of cards modeled on a fine art prints page), and report whether a card
with that title was on it.

- **Manipulation:** title similarity (low vs high) within subjects. In *high*, five of the other titles share the target's
  first word (Desert Coral among Desert Garden, Desert Jewel, ...). In *low*, no other title shares a word with it.
- **Signal:** target present on half the trials, absent on half. This gives hits and false alarms per condition.
- **Measures:** `d'` (sensitivity) and `c` (criterion) per participant and similarity level, plus reaction time.
- **Design:** 2 x 2 within subjects, 160 trials (4 blocks of 40) after 16 practice trials, about 15 minutes.
- **Controls:** the same photographs appear in every condition and are randomly paired with titles on every trial; titles are
  matched on length; the "yes" key is counterbalanced across participants; no feedback outside practice.

## Files

```
index.html          the whole task (HTML, CSS, JavaScript)
apps-script/Code.gs Google Apps Script that writes rows to your sheet
SHEETS_SETUP.md     sheet setup and column dictionary
images/             44 Range & Focus photographs: print_01.jpg ... print_44.jpg
```

## Run it locally

Open `index.html` in a browser. Add `?quick=1` for a 2-minute test run, `?T=400` to change the display time.

## Publish on GitHub Pages

1. Push this folder to a GitHub repository.
2. In the repo, choose **Settings > Pages**, set the source to your main branch and the root folder, and save.
3. Your study is live at `https://YOUR-USERNAME.github.io/REPO-NAME/`.

## Before you collect data

- **Sheet:** follow `SHEETS_SETUP.md` and paste your Web App URL into `CONFIG.sheetWebAppUrl`.
- **Consent (required):** the first screen shows the ASU short-form consent with "I consent" and "I do not consent" buttons.
  Declining ends the session and sends no data. Open `CONFIG.consent` near the top of `index.html` and replace each
  `[BRACKETED]` placeholder (your name, advisor/PI, compensation or course credit, contact email) with the details in your
  approved IRB protocol. A red setup note shows on the consent screen until none remain; delete the `warn` line in
  `consentHTML()` if you want it gone for good. Set `includeDataSharing: false` if your protocol does not allow sharing
  de-identified data. Change `version` if you edit the wording so each row records which text was shown.
- **Photos:** 44 photographs from the Range & Focus website folder are in `images/` (square, white-matted, 480 px, about 1.2 MB).
  They are randomly re-paired with titles on every trial, so a photo never predicts a title. To swap them, keep the
  `print_NN.jpg` names and update `CONFIG.photoCount`.
- **Display time:** now 700 ms. Run a pilot and adjust `CONFIG.displayMs` (or use `?T=`) until `d'` sits around 1 to 2.5 in both conditions.
- **Titles:** ten target families of six titles each. 22 of the 60 are real catalog titles (Desert Garden, Emerald Bay, ...);
  the other 38 are invented siblings in the same style, because the real catalog has too few titles sharing a first word.
  Filler titles on each page are real catalog titles with place names removed. `target_source` and `n_invented_distractors`
  are logged so you can check whether invented titles behave differently.
