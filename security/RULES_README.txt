DRAFT ONLY — DO NOT PUBLISH YET.

Current simplified plan: ONE Firebase Authentication Email/Password user on both staff phone and player tablet. Both have the same database write permissions. This preserves existing controls but does NOT isolate tablet actions from staff actions.

The draft JSON allows public reads to preserve unauthenticated OBS overlays, and allows writes only for auth.uid === REPLACE_WITH_OWNER_UID. Replace the placeholder with the exact UID shown in Firebase Authentication > Users. Never use an email address or password in rules. Do not send passwords in chat.

Before publishing: verify all active Firebase consumers; test persistent login on phone and tablet; test all reads/writes in the Realtime Database rules simulator/emulator, including denial for unauthenticated writes; verify timer, interview, names, inks, game wins and lore; check the root-level write rule is appropriate for this single-owner system; then deploy tested controller code and publish rules last. Keep rollback copies. No production deployment has happened.
