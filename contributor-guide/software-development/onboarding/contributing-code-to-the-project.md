# Contributing Code to the Project

## Pick a Task

First off, thank you for your interest in contributing code to OpenBoxes!

We have plenty of [open issues on our github](https://github.com/openboxes/openboxes/issues?q=is%3Aissue%20state%3Aopen%20label%3A%22status%3A%20ready%20for%20work%22) that are ready to be worked on. If you're new to the project and don't know where to start, we encourage you to take a look at one of our [beginner friendly tasks](https://github.com/openboxes/openboxes/issues?q=is%3Aissue%20state%3Aopen%20label%3A%22flag%3A%20beginner%20friendly%22).

Of course, you're welcome to [open a new issue](https://github.com/openboxes/openboxes/issues/new) if you have a new feature or bug that you want to work on that isn't already documented.

## Fork the Repository

If you haven't already done so, you'll need to [create a fork](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/fork-a-repo) of the [openboxes repository](https://github.com/openboxes/openboxes) and then [clone your fork to your local machine](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository). We do this as a security measure to protect the project from rogue commits and to keep our branch structure clean.

We encourage you to regularly [sync the main repository to your fork](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/syncing-a-fork) so that you are always working against the latest code and so that you don't have to deal with merge conflicts when attempting to merge in your change.

If you're a full-time or trusted contributor to the project, you may be granted direct write access to the repository and so don't need to create a fork.

If you haven't done so yet, you'll want to [get OpenBoxes running on your local machine](https://openboxes.gitbook.io/contributor-guide/software-development/onboarding/running-openboxes-locally) so that you can test your change before committing it.

## Create a Branch

When implementing your code change, we suggest you [make your commits into a feature branch](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-and-deleting-branches-within-your-repository) so that your code and commit history stay clean.

We use a `<type_prefix>/<short_description>` naming scheme for our branches in OpenBoxes.

The type prefixes that we use are:

* `ft/*` for new features
* `bug/*`  for bug fixes that address unintended app behaviour
* `td/*`  for tech debt, non-feature code improvements and other general maintenance work

These prefixes help us categorize issues, and allow us to automatically apply matching labels to PRs.

After the prefix, we include a short description of the change. Don't worry too much about finding the perfect name. The goal is simply to allow us to easily find the branch in the future if needed.

For example, if your changes fixes a typo relating to the name field of products, you might name your branch `bug/product-name-typo` .

## Make a Pull Request

Once your code change is tested and ready to be submitted, you can [make a pull request from your fork](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request-from-a-fork) back into the `develop` branch of the openboxes repository.

Our pull request template will guide you in writing your pull request description, but please remember to provide enough context for reviewers to be able to understand the change and why it is necessary.

Once your pull request is created, we will review it as soon as possible. Thanks again for your contribution!
