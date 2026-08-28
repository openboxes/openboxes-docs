---
description: Forking the repository and creating a well-named branch for your change.
---

# Forking and Branching

## Fork the repository

If you haven't already done so, you'll need to [create a fork](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/fork-a-repo) of the [openboxes repository](https://github.com/openboxes/openboxes) and then [clone your fork to your local machine](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository). We do this as a security measure to protect the project from rogue commits and to keep our branch structure clean.

We encourage you to regularly [sync the main repository to your fork](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/syncing-a-fork) so that you are always working against the latest code and so that you don't have to deal with merge conflicts when attempting to merge in your change.

If you're a full-time or trusted contributor to the project, you may be granted direct write access to the repository and so don't need to create a fork.

{% hint style="info" %}
If you haven't done so yet, [get OpenBoxes running on your local machine](../set-up-your-environment/running-openboxes-locally.md) so that you can test your change before committing it.
{% endhint %}

## Create a branch

When implementing your code change, we suggest you [make your commits into a feature branch](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-and-deleting-branches-within-your-repository) so that your code and commit history stay clean.

We use a `<type_prefix>/<short_description>` naming scheme for our branches in OpenBoxes.

The type prefixes that we use are:

* `ft/*` for new features
* `bug/*` for bug fixes that address unintended app behaviour
* `td/*` for tech debt, non-feature code improvements and other general maintenance work

These prefixes help us categorize issues, and allow us to automatically apply matching labels to PRs.

After the prefix, we include a short description of the change. Don't worry too much about finding the perfect name. The goal is simply to allow us to easily find the branch in the future if needed.

For example, if your change fixes a typo relating to the name field of products, you might name your branch `bug/product-name-typo`.

Branch off `develop`, which is where all of our latest changes live. See [Repositories and Branches](../../how-openboxes-works/repositories-and-branches.md) for how `develop`, `main` and release branches relate to each other.

**Next:** [Test your change](../test-your-change.md)
