# FGD Stage-I Dashboard – NTPC Sipat

Created by **Mridul Kanti Baruri · 109384 · Operation · NTPC Sipat**

Live website: `https://mridulkantibaruri98-hub.github.io/fgd-dashboard01/`

- **Everyone** opens the link and sees the dashboard. No login is needed.
- **Shift engineers** click **UPLOAD LOGBOOK** (bottom of the page), type their name and the **upload password** (asked every time, never saved), choose the logbook Excel and press **UPLOAD & PUBLISH**.
- **Every upload is kept for ever.** Each upload is saved as a new version in the GitHub repository (Commits), with who uploaded it and when. The bottom bar of the website shows the last upload.

## Files

| File | What it is |
|---|---|
| `index.html` | The dashboard (plant photo banner, big letters, touch-to-see values) and the upload button at the bottom |
| `setup.html` | Owner-only page to create or change the upload password |
| `access-keys.json` | Created by `setup.html`: the GitHub key, locked with the upload password (AES-256) |
| `data/dashboard-data.xlsx` | The latest logbook. Each upload replaces it; old versions stay in the history |
| `.nojekyll` | Tells GitHub Pages to publish the files as they are |

## One-time setup (owner)

1. **Put the files in the repository.** Open the repository `fgd-dashboard01` → **Add file → Upload files**, drag in `index.html`, `setup.html`, `.nojekyll`, `README.md` and the `data` folder, and press **Commit changes**. Old files with the same names are replaced.
2. **Make a new GitHub access key.** GitHub → your photo → **Settings → Developer settings → Personal access tokens → Fine-grained tokens → Generate new token**.
   - Repository access: **Only select repositories → fgd-dashboard01**
   - Permissions → Repository permissions → **Contents: Read and write**
   - Expiration: the longest offered (choose **No expiration** if your account shows it)
   - Copy the key (`github_pat_…`). Delete the old key you made earlier, because it was shown in a screenshot.
3. **Lock the key with the upload password.** Open `…/fgd-dashboard01/setup.html`, paste the key, type an upload password (10 or more characters) twice, and press **LOCK KEY & SAVE TO WEBSITE**.
4. Give the upload password to the shift engineers. Use **Test a password** on the setup page to check it.

## Everyday use (shift engineer)

1. Open the website → **UPLOAD LOGBOOK**.
2. Type your name, the upload password and choose the logbook Excel. The page checks the file first and shows “data up to …”.
3. Press **UPLOAD & PUBLISH**. Everyone sees the new data within 1–2 minutes.

## Changing or removing the password

Open `setup.html` again, paste a (new) GitHub key, type the new password and save with **Replace all existing passwords** ticked. The old password stops working at once.
To give a person their own password, untick that box. Each saved password then works separately.

If the GitHub key ever expires, uploads show “The upload key has expired”. Make a new key (step 2) and run `setup.html` again.

## How the figures are worked out

- **FGD availability** = FGD run h ÷ unit run h × 100. A blank unit run cell counts as 24 h.
- **SOx removal efficiency** = (inlet − outlet) ÷ inlet × 100, calculated daily. When FGD run h = 0 the unit shows **FGD NOT IN SERVICE**, and that day is left out of the SOx averages.
- **APC %** = FGD MU ÷ unit MU production × 100, shown to 4 decimals.
- **Periods:**
  - **Daily:** latest date; the trend shows that date − 7 days. A picked date shows ± 7 days.
  - **Monthly:** latest month; the trend shows every day of it. Month + date gives 1st of that month → that date.
  - **Yearly:** 01-Apr → date; the trend shows one bar per month.

## Security notes

- The GitHub key is stored only in locked form, so someone without the password cannot use it.
- Use a strong password, because `access-keys.json` is public in locked form.
- The key can only change this one repository.
