# Upgrading BrewStaffAI from 4.2.1 to 4.3.0

## 1. Put the new files in your project (VS Code)
1. Unzip `BrewStaffAI_v4.3.0.zip`.
2. Copy **everything inside** the unzipped `BrewStaffAI_v4.3.0` folder into your `brewstaffai` project folder and choose **Replace** when asked.
3. Do **not** delete your own `.streamlit/secrets.toml`. This zip does not contain one, so yours stays as it is.
4. Optional cleanup: delete the old `assets/storefront.jpg` (the login page now uses `assets/storefront_hd.jpg`).

## 2. Test on your laptop first (about 10 minutes)
```
python -m pip install -r requirements.txt
python test_forecaster.py
python -m streamlit run app.py
```
`test_forecaster.py` must end with **33 of 33 checks passed**. Then check the app:

| # | What to do | What you should see |
|---|---|---|
| 1 | Open the login page | The storefront photo is sharp and fills the left side |
| 2 | Log in as Staff, press **Log out** | A pop-up "Log out of BrewStaffAI?" Press **Stay logged in**: nothing happens. Press **Log out** again, then **Yes, log out**: you are logged out |
| 3 | Same test as Manager | Same pop-up |
| 4 | Manager → **Settings → Demand data** | Four cards, an import box, and a table "What the AI forecasts now" |
| 5 | Download the CSV template, change a few numbers, upload it | Green "Ready: n hours…" message and a preview. Press **Import** |
| 6 | **Staffing Planner → Plan the day** → open "Expected customers per hour" | A "Usual range" column and "Based on" text such as "AI forecast · medium confidence" |
| 7 | **Pilot Results → 3 · Demand forecast** | Needs counts from 2 or more days. Then you see the accuracy cards and charts |
| 8 | **Settings → Data & backup → Prepare backup** | The ZIP now contains `demand_history.csv` |

## 3. Push to GitHub
Source Control → type a message such as `v4.3.0: demand forecaster, logout confirmation, HD login photo` → **Commit** → **Sync Changes**.
Streamlit Community Cloud updates the app by itself in 1–3 minutes. No Secrets changes are needed.

## 4. Check the live app
Open your app link. If it shows the old version, press **Manage app → Reboot app**. The sidebar should show **v4.3.0** under the Log out button. The new database table is created automatically the first time the app opens.
