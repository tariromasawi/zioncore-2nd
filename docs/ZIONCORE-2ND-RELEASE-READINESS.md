# ZionCore 2nd Release Readiness

## Verified

- The preserved standalone source snapshot is in the private GitHub repository
  `https://github.com/tariromasawi/zioncore-2nd`, branch
  `zioncore-2nd/firebase-integrity-reviewed`, based on
  `zioncore-2nd/phase2-genesis-foundation`. Original-workspace byte-for-byte
  parity remains unverified.
- The repository contains 607 tracked files. `SOURCE_INVENTORY.sha256` records
  606 tracked-file checksums; CI verifies the manifest after every push.
- The Phase 1 source baseline and file-comparison findings are recorded in
  `docs/ZIONCORE-2ND-PHASE-1-SOURCE-BASELINE.md`.
- The GitHub Actions validation workflow runs typecheck, web and API tests,
  Firebase emulator checks, source-inventory verification, and web/API
  production builds. The latest branch commit passed run
  `44321869186`.
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
- Firestore App Check enforcement is enabled. The standalone browser SDK passed
  authenticated own-record write/read with a valid development App Check token;
  a matching authenticated REST read without App Check was rejected. The test
  account and record were deleted. Identity Toolkit enforcement remains off.
- Local checks passed: web unit tests 426/426; API unit tests 108/108; web and
  API typechecks; web and API production builds; wallet/ledger/Stripe emulator
  integration tests 20/20.
- Firebase Authentication emulator tests passed 3/3 for registration,
  sign-out, sign-in, invalid-password handling, duplicate email rejection and
  server-side token verification. Live Email/Password sign-up/sign-in and
  session restoration after reload also passed with a disposable account.
- The standalone browser rendered content at `/`, `/missions`, `/astronomy`,
  `/bioacoustics`, `/voice-v2`, `/access`, `/dashboard`, `/history`, and
  `/messages` in a simulated 402×874 viewport without horizontal overflow.
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
   Apple sign-in needs Apple Developer configuration. Firestore App Check
   enforcement is verified; owner access remains unverified.
2. **Cloud AI:** application requests remain gated until live authenticated
   flows and project/provider cost and quota settings are verified. One minimal
   text-only `gemini-3.8-flash` reachability check succeeded (7 prompt, 1 output,
   118 thought tokens; no customer data); this did not verify the app's
   authenticated AI route or quota enforcement.
3. **Business payments:** a read-only live Stripe catalog check confirmed active
   GBP prices for the app's current supported credit packs (250, 500, 1,050,
   2,750 and 5,750 credits) and £1/month Premium. Active legacy 50/200/1,000
   credit products also exist, but the app classifies them as legacy and does
   not expose them for new checkout. No checkout, webhook fulfillment, or
   charge was performed. Production checkout remains disabled until separate
   ZionCore 2nd Stripe credentials, the exact offer set, approved host, and
   environment gates are configured.
4. **Independent production API:** the source builds and the Replit preview
   API responds locally; no independent production backend was deployed.
5. **Live customer and owner journeys:** Email/Password sign-in, persistent
   session after reload, and temporary customer history access passed. Owner
   access remains unverified. A read-only Auth listing found zero users after
   cleanup, so no owner account or claim is available; none was assigned. The
   supplied Replit preview resolves to the main Firebase project, not this app,
   so it cannot validate the standalone Firebase client.
6. **Mobile browser:** the nine key routes rendered at 402×874 Chromium
   mobile-emulation width without horizontal overflow; final iPhone Safari
   end-to-end verification remains outstanding.
7. **Dependency advisories:** the scoped full dependency audit reports one high
   and one moderate development-tool advisory, plus two moderate production
   transitive advisories (`glob` and `minimatch`). The high `picomatch` advisory
   currently has no patched release in the registry result. The Firebase CLI
   was updated to 15.36.0; the advisory remains open. Do not claim a clean
   dependency audit.

## Deployment boundary

The independent Firestore rules and App Check enforcement are configured, but
no app deployment, billing activation, production Stripe operation, or change
to the original ZionCore project was performed. Do not describe the system as
launch-ready until the blockers above are resolved and the resulting live
journeys are verified.
