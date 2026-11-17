# ZionCore 2nd

ZionCore 2nd is the full standalone research laboratory source preserved from
the `zioncore-2nd/full-implementation` worktree. Its web application is
`artifacts/zioncore-frequency-lab`; its API is `artifacts/api-server`; shared
contracts and services are in `lib/`. This repository does not depend on the
main ZionCore application's source or API.

## Included experience

The full web application includes Live Lab, exploration, missions, astronomy,
bioacoustics, Voice V2, access guidance, messages, device tools, signal cards,
history, wallet, premium and owner routes. The API contains authenticated
Firebase identity checks, research and AI routes, wallet and credit-ledger
operations, Stripe webhook/fulfilment code, owner diagnostics and health
endpoints. Financial and owner actions remain server-authorized.

The original Genesis Seed is preserved byte-for-byte at
`governance/genesis/GENESIS_SEED.original.txt`. Its SHA-256 is
`f87c324da247443bcf6ac4c6b799241e871abc3dec8aaa69c921cd123943f95e`.
`ZIONCORE_GENESIS_SEED_INTEGRATION.md` maps its bounded, versioned operational
context to the API prompt pipeline; the immutable source is not rewritten.

## Install and run

Use Node.js 22 or newer and pnpm 10:

```sh
pnpm install --frozen-lockfile
pnpm --filter @workspace/zioncore-frequency-lab run dev
pnpm --filter @workspace/api-server run dev
```

The artifact manifests contain the Replit preview routing configuration.
For local development, configure the public Firebase values documented in
`artifacts/zioncore-frequency-lab/.env.example` and keep the API service
credential in a server-side secret store as documented in
`artifacts/api-server/.env.example`. Never commit credential values.

## Validation

```sh
pnpm run typecheck
pnpm --filter @workspace/zioncore-frequency-lab run test:unit
pnpm --filter @workspace/api-server run test:unit
PORT=3000 BASE_PATH=/ pnpm --filter @workspace/zioncore-frequency-lab run build
pnpm --filter @workspace/api-server run build
```

Authentication, Firestore rules and wallet integration tests use the Firebase
emulators; see the `test:auth`, `test:rules` and `test:wallet` scripts in the
package manifests. Emulator passes do not establish live-project readiness.
GitHub Actions runs the unit, type, emulator and build checks on proposed
changes. It does not deploy production.

## Firebase status

The independent project is `zioncore-2nd-production` (`225578874852`). Its
default Firestore database is Native mode in `europe-west2`; reviewed rules are
deployed. Read-only Admin access succeeded using the project-specific service
identity. Development and production App Check token exchange have both been
verified, with distinct web app IDs and hostname-restricted reCAPTCHA keys.
App Check enforcement remains disabled pending authenticated-flow verification.

Firebase Authentication is not initialized: the provider configuration lookup
returned `404 CONFIGURATION_NOT_FOUND`, and initialization returned
`400 FAILED_PRECONDITION: BILLING_NOT_ENABLED`. No billing was enabled and no
customer accounts were created. Consequently, cloud history, authenticated AI,
and account journeys are not launch-ready. See
`artifacts/zioncore-frequency-lab/FIREBASE_SETUP_ZIONCORE_2ND.md` for evidence
and the exact remaining setup requirement.

## Release boundary

This source is buildable, but it is **not yet a complete business launch**.
Firebase Authentication, live AI provider availability/quota, production
payment configuration, an independently deployed API runtime, and final
mobile-browser verification remain outstanding. The original ZionCore
production project and its Firebase resources were not modified.
