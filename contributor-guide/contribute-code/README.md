---
description: The path from picking a task to getting your pull request merged.
---

# Your First Contribution

Thank you for your interest in contributing code to OpenBoxes!

## Which codebase?

| Codebase | Built with | Where to go |
| --- | --- | --- |
| **Web application** — the main OpenBoxes app | Grails (Groovy) and React | The five steps below |
| **Mobile app** | React Native and TypeScript | [Mobile App](mobile-app.md) |
| **End-to-end tests** | Playwright and TypeScript | [End-to-End Tests](end-to-end-tests.md) |

## Contributing to the web application

The steps below cover [openboxes/openboxes](https://github.com/openboxes/openboxes), the main web application. Read them start to finish if you're new — each step assumes you've done the one before it.

### 1. [Set up your environment](set-up-your-environment/running-openboxes-locally.md)

Get OpenBoxes building and running on your machine, and get your debugger attached. This is the longest step, and you only do it once.

### 2. [Find something to work on](find-something-to-work-on.md)

Pick an existing issue or open a new one. We flag beginner-friendly tasks specifically for people making a first contribution.

### 3. [Write your change](write-your-change/forking-and-branching.md)

Fork the repository, create a branch following our naming scheme, and make your change.

### 4. [Test your change](test-your-change.md)

Run the frontend and backend test suites, and add tests covering what you changed.

### 5. [Open a pull request](open-a-pull-request.md)

Submit your change back to the `develop` branch and work with a reviewer to get it merged.

## Other codebases

* [Mobile App](mobile-app.md) — the React Native app, in [openboxes-mobile](https://github.com/openboxes/openboxes-mobile)
* [End-to-End Tests](end-to-end-tests.md) — the Playwright suite, in [openboxes-e2e](https://github.com/openboxes/openboxes-e2e)

***

Stuck at any point? [Ask on Slack](http://slack-signup.openboxes.com/) — see [Community & Getting Help](../start-here/community-and-getting-help.md). If you hit unfamiliar jargon, the [Glossary](../start-here/glossary.md) covers both warehouse and codebase terms, and [How OpenBoxes Works](../how-openboxes-works/) explains the architecture.
