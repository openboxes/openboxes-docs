---
description: Contributing to the Playwright end-to-end test suite.
---

# End-to-End Tests

Our end-to-end (E2E) suite simulates real user behaviour against a running OpenBoxes instance. It lives in its own repository, [**openboxes/openboxes-e2e**](https://github.com/openboxes/openboxes-e2e), and is built with **Playwright** and **TypeScript**.

Increasing automated test coverage is a primary goal of the project — it gives us confidence the application works, and makes it safer to change. Writing tests is one of the most useful things you can contribute, and it doesn't require knowing the Grails backend.

{% hint style="info" %}
Looking for the unit and API tests that live alongside the application code? Those are in the main repository — see [Test Your Change](test-your-change.md).
{% endhint %}

## Before you start

E2E tests run against a live, deployed environment rather than a build of the source. You'll need an OpenBoxes instance to point them at — either one you [run locally](set-up-your-environment/running-openboxes-locally.md) or [in Docker](set-up-your-environment/running-with-docker.md), or one you already have access to.

## Getting set up

The [repository's README](https://github.com/openboxes/openboxes-e2e#readme) is the authoritative guide. In short, it expects Node 18.19.x and npm 9.2.0, then:

```
npm install
npx playwright install
```

Copy the example environment file and fill in the variables that point the suite at your instance, then:

```
npm run test                 # run the suite
npm run test -- --headed     # watch it drive a real browser
npm run lint                 # lint, with npm run lint-fix to autofix
```

The repository also carries its own documentation on authentication, fixtures, locators, test data setup, CI configuration and project structure — read that before writing your first test, since the suite has established patterns worth following.

## Picking something to test

If you'd like to write tests but aren't sure where to start, [reach out on Slack](http://slack-signup.openboxes.com/) and we'll help you pick a feature that needs coverage.
