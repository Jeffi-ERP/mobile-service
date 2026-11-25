<!-- Managed from AloysJehwin/Jeffi_Stores (oss/templates); edits here are overwritten by the next export. -->
<p align="center"><a href="https://github.com/Jeffi-ERP"><img src="https://raw.githubusercontent.com/Jeffi-ERP/.github/main/assets/jeffi-erp-logo.svg" width="64" alt="Jeffi ERP"></a></p>

# mobile-service

Mobile backend API and the Expo (React Native) shopping app.

Part of [Jeffi ERP](https://github.com/Jeffi-ERP), where the Jeffi Stores commerce platform is developed in the open. In the workspace this repo is `mobile-service/`. It builds and tests inside the assembled workspace, not on its own.

## Set up

```bash
git clone https://github.com/Jeffi-ERP/workspace.git jeffi-erp
cd jeffi-erp
node oss/assemble.mjs                  # clones every Jeffi ERP repo into its folder
ONNXRUNTIME_NODE_INSTALL=skip npm ci
```

Then follow [Set up the workspace](https://github.com/Jeffi-ERP/.github/blob/main/CONTRIBUTING.md#set-up-the-workspace) for the database, `.env.local` and a local admin. You never need Jeffi Stores' own keys. To change this repo, fork it and add your fork as a remote inside `mobile-service/`.

## How a change gets in

1. Open a pull request against `main`. Nothing runs yet.
2. A maintainer reads it and adds the `ok-to-test` label. That runs **PR checks** and **Guard**. A new push removes the label until a maintainer looks again.
3. When both pass, a maintainer squash-merges it. The merge runs pre-build and build, then waits for a maintainer to approve the promotion.
4. After approval the change is opened as a pull request on [AloysJehwin/Jeffi_Stores](https://github.com/AloysJehwin/Jeffi_Stores) and ships with a later release. The export from that release brings it back here.

`.github/` and `LICENSE` (and `oss/` in workspace) come from AloysJehwin/Jeffi_Stores, and Guard rejects pull requests that change them. Open an issue for those instead.

## Checks

| Stage | Check | Command (from the workspace root) |
|---|---|---|
| PR checks (after `ok-to-test`) | Lint | `npx eslint --no-eslintrc -c .eslintrc.services.cjs --ext .ts mobile-service/src` |
| PR checks (after `ok-to-test`) | Type check | `npm --prefix mobile-service run typecheck` |
| PR checks (after `ok-to-test`) | Unit tests | `npm --prefix mobile-service test -- --passWithNoTests` |
| PR checks (after `ok-to-test`) | App type check | `npm --prefix mobile-service/client ci && npm --prefix mobile-service/client run typecheck` |
| Pre-build (after merge) | Lint | `npx eslint --no-eslintrc -c .eslintrc.services.cjs --ext .ts mobile-service/src` |
| Pre-build (after merge) | Type check | `npm --prefix mobile-service run typecheck` |
| Pre-build (after merge) | App type check | `npm --prefix mobile-service/client ci && npm --prefix mobile-service/client run typecheck` |
| Build (after merge) | Unit tests | `npm --prefix mobile-service test -- --passWithNoTests` |

Run a stage locally from the workspace root: `node oss/checks.mjs mobile-service pr`.

## Licence

[GNU Affero General Public License v3.0](../LICENSE) (`AGPL-3.0-only`). You may use, modify and redistribute this code, including in production. If you distribute a modified version, or run one as a service that people use over a network, you must make its source available to those users under the same licence. Jeffi Stores also offers a commercial licence for use without those conditions. Contributions are accepted on the terms in [CONTRIBUTING](https://github.com/Jeffi-ERP/.github/blob/main/CONTRIBUTING.md).
