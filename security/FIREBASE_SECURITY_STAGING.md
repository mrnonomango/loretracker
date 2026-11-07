# Firebase security staging (NOT DEPLOYED)

Project: lore-counter-4e654

This branch is isolated from main. The live database currently permits public reads and writes. Do not publish restrictive rules before testing all existing pages.

## Verified code findings
- testphonecontroller.html, newlorestaffcontroller.html, newloreplayercontroller.html connect to Realtime Database without Firebase Authentication.
- newloreoverlay.html subscribes to database values without Authentication.
- Existing data includes both root keys (p1, p2, etc.) and newlore/*; interview/* is also used.

## Implementation requirements
1. Add persistent Firebase Email/Password sign-in to staff phone, with no repeated login under normal conditions. Never embed credentials in HTML.
2. Add persistent authorized tablet session; tablet UI must remain unchanged and only write lore fields. Tablet possession alone is not a Firebase security boundary.
3. Preserve OBS read access without a manual login, either with carefully scoped public read-only paths or a separately authenticated read-only session; avoid public reads if the data is sensitive.
4. Update every legacy page and any other repositories sharing the database before locking down writes.
5. Rules must restrict staff writes by explicit auth.uid allowlist / custom claims, tablet writes by explicit per-device authorization and narrow paths; do not allow all authenticated or anonymous users to write.
6. Validate data types/ranges and use the Realtime Database rules simulator/emulator to test allowed and denied operations.
7. Test phone, tablet, OBS, timers, score, interview, and older overlays; then publish rules with a rollback plan.

No database rules or production files were changed by this staging note.
