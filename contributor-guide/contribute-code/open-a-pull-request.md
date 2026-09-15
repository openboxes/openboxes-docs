---
description: Submitting your change and getting it through review.
---

# Open a Pull Request

Once your code change is tested and ready to be submitted, you can [make a pull request from your fork](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request-from-a-fork) back into the `develop` branch of the openboxes repository.

Our pull request template will guide you in writing your pull request description, but please remember to provide enough context for reviewers to be able to understand the change and why it is necessary. A good description covers:

* What the change does, and which issue it addresses
* Why it's needed, if that isn't obvious from the issue
* How you tested it, including anything a reviewer should check by hand
* Screenshots or a short recording, for anything that changes the UI

## What happens next

Once your pull request is created, we will review it as soon as possible. A reviewer may ask questions or request changes — this is normal and is not a judgement on the work. Push follow-up commits to the same branch and the pull request will update automatically.

If your pull request goes quiet for a while, give us a nudge on [Slack](http://slack-signup.openboxes.com/). We'd rather be reminded than leave your work sitting.

Once approved, a maintainer will merge your change into `develop`. It will ship to users in the next release — see [Cut a Release](/maintainers/cut-a-release) for how that works.

Thanks again for your contribution!
