# Firebase staging audit — 2026-11-05

## Changes already committed to this branch
- Persistent Firebase Email/Password login gates: testphonecontroller.html, newlorestaffcontroller.html, controller.html, newloreplayercontroller.html.
- Draft rules: security/realtime-database.rules.DRAFT.json. DO NOT PUBLISH YET.
- Production/main branch and live Firebase rules unchanged.

## Actual tablet behavior verified from code
- Lore increment/decrement and reset: p1, p2.
- Game wins and reset: p1Games, p2Games.
- Player names: p1Name, p2Name.
- Ink choices: p1Ink/p2Ink and p1Inks/p2Inks.
- New tablet uses newlore/ prefix, older tablet uses root paths.
- Both tablets use multi-path update calls for ink selection; rules must allow all affected child paths.

## Additional Firebase consumers found in repository
- testlayout.html (OBS read), newloreoverlay.html (OBS read), scenetimer.html (OBS read), interviewoverlay.html (OBS read), interviewmotiontest.html (read), testingloretracker.html (inspect write paths before publishing), testlayout-trail-test.html (inspect), backups/testlayout-original-2026-10-23.html (archived).
- No code search matches for the same Firebase project in mrnonomango/TCG or mrnonomango/overlayhub; this is not a complete runtime audit.

## Current blocking items before deployment
1. Create a separate Firebase Authentication Email/Password user for the tablet (not the staff account). Never send passwords in chat.
2. Record staff and tablet UIDs from Firebase Console; insert them in the draft rules. UIDs are identifiers, not passwords, but do not publish them unnecessarily.
3. Check all remaining writer pages and confirm paths, especially testingloretracker.html and old test pages.
4. Run Firebase Realtime Database emulator/rules simulator: allow staff on approved paths, allow tablet only on approved paths, reject unauthenticated writes and tablet writes to timer/interview/records, and reject parent-level destructive writes.
5. Test sign-in persistence on actual phone and tablet and data updates/OBS reads. Confirm the hosted staging URLs really load the staging branch rather than main.
6. Improve data validation for lore range, game wins, names, and timer; decide whether public read-only overlay data is acceptable.
7. Deploy code only after testing; publish rules last and verify all live scenes, with rollback plan.

## Known caveat
The sign-in gate in the staged HTML is a UI change until security rules are deployed; it does not independently stop database writes by attackers. Browser sessions can expire or be cleared. Firebase client API keys are not passwords and must not be treated as authorization.
