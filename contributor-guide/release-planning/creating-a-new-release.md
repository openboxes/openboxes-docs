# Creating A New Release

The following outlines the steps required in order to create a new release of OpenBoxes.

It is the responsibility of the release manager to not only perform the release, but to determine if the application is in a stable enough state for us to be deemed as "release-ready".

### 1. Merge the 'develop' branch into 'main'

We do our development work in the 'develop' branch. This branch has all of our latest changes, and so is not stable to release from. To start the release process, merge develop into main (which is our stable branch).

&#x20;

### 2. Bump the application version

{% hint style="info" %}
We typically give ourselves a one week "Regression Sprint" after merging develop into main but before bumping the app version. This sprint acts as a buffer period as it allows us to test the release to confirm its stability. At this time we "freeze" the develop and main branches, only allowing changes to be merged in that are essential to the release.

If testing unconvers any bugs, we submit the bugfix to the develop branch and then merge the change down to main.

We only proceed with bumping the app version and creating the release branch once we've completed our full testing plan and all discovered issues have been resolved.
{% endhint %}

Our releases follow the [Semantic Versioning (semver) pattern](https://semver.org/). In short:

> Given a version number MAJOR.MINOR.PATCH, increment the:
>
> 1. MAJOR version when you make incompatible API changes
> 2. MINOR version when you add functionality in a backward compatible manner
> 3. PATCH version when you make backward compatible bug fixes

For example, if we're currently on v1.4.3 and need to create a new release:

* if we're only making a bug fix -> v1.4.4
* if we're adding new functionality -> v1.5.0
* if we're making backwards incompatible change -> v2.0.0



Once you've determined the version that we need to upgrade to, change the version number in the `gradle.properties` file:

```
version=x.y.z
```

Where `x.y.z` is the new version. Make sure to remove `-SNAPSHOT` from the end of the version number.

The commit message for this change should be `"bumped app version to x.y.z"` (where `x.y.z` is the new version).



### 3. Create a new release branch off of 'main'

Now that we're ready to release, we can create a branch off of the final commit of the release (bumping the app version). We do this so that we can easly merge and release patch fixes to existing releases.

The release branch should be named: `release/<release_version>`  where `release_version` is the semver number of the upcoming release.

For example, if the application is being bumped to `v0.9.8`, the branch should be named `release/0.9.8`



### 4. Tag the release commit

We need to tag the commit from step 2 so that we can create the actual release from it. First, find the commit number.

<figure><img src=".gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

Then create the tag and push it to the repository:

```console
git tag -a vx.y.z -m 'Release x.y.z'
git push --tags
```

Where `x.y.z` is the semver number of the upcoming release. For example:

```
git tag -a v1.2.3 -m 'Release 1.2.3'
```



### 5. Update the release notes

Once you complete step 4 and push the new tag, [a GitHub Action that we created](https://github.com/openboxes/openboxes/actions/workflows/do-github-release.yml) will be triggered, automatically creating [the GitHub release](https://github.com/openboxes/openboxes/releases) for you.

The generated release notes will be populated with a "What's Changed" section, hilighting all the commits from the release. It will also automatically contain an openboxes.war file containing the application distribution for the release.

All you should need to do is confirm everything looks as expected and add any additional notes that are required for the release. If the release contains backwards incompatible changes, these should be pointed out clearly in the release notes and be paired with instructions on how to upgrade to the new version.



### 6. Merge back up to develop

Now that the release is completed, we need to merge main back up to develop so that the develop is up to date with any new commits from main.

As a part of the merge, bump the patch version in the `gradle.properties` file, adding SNAPSHOT to the end (signifying this new version is unreleased):

```
version=x.y.z-SNAPSHOT
```

For example, if the version was `1.2.3`, it should now be `1.2.4-SNAPSHOT` .

_(As a side note, we should probably be bumping the minor version instead of the patch version, but we can re-evaluate our approach later.)_



### 7. Publishing to the community

Create a new announcement post on [the community forums](https://community.openboxes.com/c/announcements/12) so that we can announce the release to the wider community!

Make sure to clearly point out any backwards incompatible changes so that the community is aware of them, and if possible add instructions (or link to instructions) on what users need to do to upgrade to the new version.

Go back to the release notes from step 5 and edit the notes, adding a link to the community release post that you just created.
