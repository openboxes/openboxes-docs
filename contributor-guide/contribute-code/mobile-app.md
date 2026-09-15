---
description: Contributing to the OpenBoxes React Native app.
---

# Mobile App

The OpenBoxes mobile app is a cross-platform iOS and Android client for inventory and warehouse management. It lives in its own repository, [**openboxes/openboxes-mobile**](https://github.com/openboxes/openboxes-mobile), and is built with **React Native** and **TypeScript** — a separate codebase and toolchain from [the web application](./).

## Before you start

The app talks to a running OpenBoxes server, so you'll need one to point it at. You can [run the web application locally](set-up-your-environment/running-openboxes-locally.md), [run it in Docker](set-up-your-environment/running-with-docker.md), or use an instance you already have access to. Set `API_BASE_URL` in an `EnvironmentActual.ts` file to tell the app where the server is.

## Getting set up

The [repository's README](https://github.com/openboxes/openboxes-mobile#readme) is the authoritative setup guide and covers this in full. In short:

```
yarn install
yarn pod install   # iOS only
```

Then `yarn start` to run Metro, and `yarn ios` or `yarn android` to build and launch. Both build commands lint before they run.

## Coding standards

The project follows the TypeScript Standard style, enforced by ESLint with the Airbnb configuration and React plugins. Husky blocks commits containing lint errors, and **linting cannot be disabled inline without a reviewer's explicit approval** — if a rule is genuinely wrong for your case, raise it in review rather than silencing it.

## Contributing

Issues, branches and pull requests work as they do everywhere else in the project — see [Find Something To Work On](find-something-to-work-on.md) and [Open a Pull Request](open-a-pull-request.md). Note that the branch naming scheme described in [Forking and Branching](write-your-change/forking-and-branching.md) and the `develop` target branch are conventions of the web application repository; check the mobile repository's recent history for what it uses.

{% hint style="info" %}
Not sure whether something belongs in the mobile app or the server? [Ask on Slack](http://slack-signup.openboxes.com/) — see [Community & Getting Help](../start-here/community-and-getting-help.md).
{% endhint %}
