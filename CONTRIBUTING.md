# Contributing

Two different jobs land in this repository. Do not mix them.

| Who | Start here | Do not |
|---|---|---|
| Someone adding the package to an app | [App developers](https://docs.page/invertase/react-native-coverage/app-developers) | This file, root `AGENTS.md`, `okf-bundle/` |
| Someone changing this repository | This file, then root `AGENTS.md` | The README Quick Prompt. That prompt installs the package into a harness. It is not how you develop this repo. |

Questions: [Discord](https://invertase.link/discord).

Behaviour: [Invertase Code of Conduct](https://github.com/invertase/.github/blob/main/CODE_OF_CONDUCT.md). Report conduct issues to oss@invertase.io. The copy of `CODE_OF_CONDUCT.md` in this repository still has a placeholder contact. Use the org file.

## Report a bug

Open a [bug report](https://github.com/invertase/react-native-coverage/issues/new/choose). The template asks for the library version, `react-native info`, and the steps.

## Request a feature

Open an [issue](https://github.com/invertase/react-native-coverage/issues/new/choose). GitHub Discussions are off for this repository, so do not send people there.

For an API or behaviour change, open that issue before the pull request.

## Set up

Node.js `v24.13.0` (`.nvmrc`). This monorepo uses Yarn `4.11.0` (`packageManager` in `package.json`). Do not use npm to install the workspace.

```sh
yarn
yarn prepare
yarn test
yarn typecheck
yarn lint
node bin/rn-coverage.js --help
```

`yarn test` is the unit suite. Run an end-to-end cell when the change touches the harness, the native flusher, or the pull/assert path:

```sh
yarn e2e:ios:dynamic
yarn e2e:ios:static
yarn e2e:android
```

The example apps are `example/` (Expo, iOS static) and `example-dynamic/` (bare React Native, dynamic frameworks). How to open them is in `example/README.md` and `example-dynamic/README.md`. From the root, `yarn example start`, `yarn example android`, and `yarn example ios` drive the Expo example. Native edits need a rebuild of that app.

This package belongs in those harness apps, not in a shipping app. Autolinking reads dependencies, so `devDependencies` in a product app is not a safe place for it.

## Open a pull request

There is no pull request template in this repository yet. The title is the check.

- One change per pull request.
- Title is a [Conventional Commit](https://www.conventionalcommits.org/), lowercase subject. CI enforces this (`.github/workflows/pr-title.yml`). Squash merge so the title becomes the release commit.
- Check locally: `echo "feat: your subject" | yarn commitlint`

Examples:

- `feat: add ios summary JSON schema`
- `fix: exit 2 when fixture LCOV is empty`
- `docs: document Pattern C consumer checklist`
- `chore: bump Appium in e2e workspace`

## What else changes with the code

- Behaviour that a user follows: update the page under `docs/`. The site is that tree.
- Public install or the harness-only limit: update `README.md`.
- Tests: `yarn test` for the unit suite, and an e2e cell when the flush or assert path changes.
- Changelog: do not hand-edit `CHANGELOG.md`. semantic-release writes it from the squash-merged pull request title when someone runs the manual release workflow.

## Release

Maintainers only. Releases are manual (`workflow_dispatch`). Steps: [Releasing](https://docs.page/invertase/react-native-coverage/releasing). Do not publish from a laptop.

## Agents changing this repo

An agent with this repository open is a maintainer agent. Read root `AGENTS.md` after this file. `AGENTS.md` names the workspaces, the test commands, and `okf-bundle/` for how this repo is validated.

- Do not follow the README line that says `Read https://docs.page/invertase/react-native-coverage/app-developers`. That is for an agent inside someone else's app.
- Do not clone this guidance into an app, and do not add `react-native-coverage` to a product `package.json`.
- Do not open a pull request whose title is not a Conventional Commit. The title is the changelog entry.
- Do not edit `CHANGELOG.md` by hand.
- Do not dispatch a release unless the task is explicitly a release. Publishing is a human workflow.

If the task is "add coverage to an app", stop using this file and follow the app developers page instead.
