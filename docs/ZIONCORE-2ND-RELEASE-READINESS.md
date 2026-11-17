# ZionCore 2nd Release Readiness

## Verified

- The complete standalone preview source is preserved in the private GitHub
  repository `https://github.com/tariromasawi/zioncore-2nd`, branch `main`.
  The verified source commit before this report update is
  `9958dc821028c34188c08a3e5d76482eefaab1ce`.
- The repository contains 605 tracked files. `SOURCE_INVENTORY.sha256` has
  604 file checksums, all of which verified; the manifest does not hash itself.
- The Phase 1 source baseline and file-comparison findings are recorded in
  `docs/ZIONCORE-2ND-PHASE-1-SOURCE-BASELINE.md`.
- The repository's GitHub Actions validation workflow passed on the verified
  source commit: typecheck, web and API tests, Firebase emulator checks, and
  web/API production builds. Run:
  `https://github.com/tariromasawi/zioncore-2nd/actions/runs/44001360145`.
- A clean production-mode build after deferring optional lab visuals measured
  196,474 gzip bytes for the initial JavaScript, below the 200,000-byte budget.
- The complete preview application source is present in
  `artifacts/zioncore-frequency-lab`, with the API in `artifacts/api-server`
  and shared packages in `lib/`.
- The original Genesis Seed is preserved byte-for-byte; SHA-256:
  `f87c324da247443bcf6ac4c6b799241e871abc3dec8aaa69c921cd123943f95e`.
- Firebase project identity and server service-account project were verified
  as `zioncore-2nd-production` (`225578874852`).
- A real read-only Admin SDK request completed against the live default
  Firestore database in `europe-west2`.
- Reviewed Firestore rules are deployed to the independent project. Rules
  emulator tests passed 14/14.
- Development and production App Check token exchanges succeeded against
  their respective Firebase App IDs and allowed hostnames. Enforcement remains
  disabled.
- Local checks passed: web unit tests 425/425; API unit tests 108/108; web and
  API typechecks; web and API production builds; wallet/ledger/Stripe emulator
  integration tests 20/20.
- Firebase Authentication emulator tests passed 3/3 for registration,
  sign-out, sign-in, invalid-password handling, duplicate email rejection and
  server-side token verification. This does not prove the live project's Auth
  service is initialized.
- Local route checks returned 200 for `/`, `/missions`, `/astronomy`,
  `/bioacoustics`, `/voice-v2`, `/access`, `/dashboard`, and `/messages`.
  Unauthenticated wallet and owner endpoints returned 401 as intended.
- Source uses the ZionCore 2nd Firebase project in runtime configuration; no
  main-project ID or main-project service-account variable was found in the
  selected runtime source.
- The main ZionCore Firebase project and production application were not
  changed.

## Hosting safeguard

A legacy GitHub Pages configuration on `main` at the repository root was
already enabled and published a README/Jekyll page at
`https://tariromasawi.github.io/zioncore-2nd/`; this was not the application.
The Pages configuration has been removed, the repository is private, and the
old deployment records are marked inactive. The URL returned HTTP 200 during
propagation but returned HTTP 404 at the final check.

During this session, GitHub reported the repository as public; it was restored
to private. A source scan found no common service-account, private-key,
Stripe/GitHub-token or Firebase-key patterns. The period of public visibility
cannot be precisely established, and changing visibility cannot revoke copies
made while source was public.

## Blocking launch items

1. **Firebase Authentication and history:** Email/Password is enabled and live
   sign-up/sign-in passed using one disposable synthetic account, which was
   deleted afterward. A valid own observation create/read passed; cross-account
   read and wallet write were denied. No customer data or persistent test
   account remains. Google sign-in needs an owner-selected OAuth support email;
   Apple sign-in needs Apple Developer configuration. App Check enforcement and
   owner access remain unverified.
2. **Cloud AI:** application requests remain gated until live authenticated
   flows and project/provider cost and quota settings are verified. One minimal
   text-only `gemini-3.8-flash` reachability check succeeded (7 prompt, 1 output,
   118 thought tokens; no customer data); this did not verify the app's
   authenticated AI route or quota enforcement.
3. **Business payments:** code and emulator tests exist, but live Stripe
   catalogue, independent price IDs, webhook delivery, and customer checkout
   were not tested or changed.
4. **Independent production API:** the source builds and the Replit preview
   API responds locally; no independent production backend was deployed.
5. **Live customer and owner journeys:** the temporary customer auth/history
   path passed, but the browser's persistent-session journey and owner access
  have not been verified. A read-only Auth listing found zero users after test
  cleanup, so no owner account or claim is available; none was assigned.
6. **Mobile browser:** final iPhone Safari end-to-end verification remains
   outstanding.
7. **Dependency advisories:** the standalone production dependency audit
   reported two moderate advisories; GitHub Dependabot reports three moderate
   alerts. No high or critical production dependency findings were reported.

## Deployment boundary

The independent Firestore rules and App Check provider registrations are
configured, but no app deployment, App Check enforcement, billing activation,
production Stripe operation, or change to the original ZionCore project was
performed. Do not describe the system as launch-ready until the blockers above
are resolved and the resulting live journeys are verified.
