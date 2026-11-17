# ZionCore 2nd Release Readiness

## Verified

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
- Local route checks returned 200 for `/`, `/missions`, `/astronomy`,
  `/bioacoustics`, `/voice-v2`, `/access`, `/dashboard`, and `/messages`.
  Unauthenticated wallet and owner endpoints returned 401 as intended.
- Source uses the ZionCore 2nd Firebase project in runtime configuration; no
  main-project ID or main-project service-account variable was found in the
  selected runtime source.

## Blocking launch items

1. **Firebase Authentication:** the project has no Identity Toolkit config.
   Read returned `404 NOT_FOUND: CONFIGURATION_NOT_FOUND`; initialization
   returned `400 FAILED_PRECONDITION: BILLING_NOT_ENABLED`; a direct provider
   configuration update also returned `404 CONFIGURATION_NOT_FOUND`. No
   billing was activated. Email/password, Google, and Apple sign-in therefore
   cannot be verified in this Firebase project.
2. **Cloud AI:** authenticated AI calls are gated until Firebase Auth is
   available and the project/provider cost and quota settings are explicitly
   configured. No paid model request was made.
3. **Business payments:** code and emulator tests exist, but live Stripe
   catalogue, independent price IDs, webhook delivery, and customer checkout
   were not tested or changed.
4. **Independent production API:** the source builds and the Replit preview
   API responds locally; no independent production backend was deployed.
5. **Live customer and owner journeys:** not testable without configured
   Authentication. No owner account or customer record was created.
6. **Mobile browser:** final iPhone Safari end-to-end verification remains
   outstanding.

## Deployment boundary

The independent Firestore rules and App Check provider registrations are
configured, but no app deployment, App Check enforcement, billing activation,
production Stripe operation, or change to the original ZionCore project was
performed. Do not describe the system as launch-ready until the blockers above
are resolved and the resulting live journeys are verified.
