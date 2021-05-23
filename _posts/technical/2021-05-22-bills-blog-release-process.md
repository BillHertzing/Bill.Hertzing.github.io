---
title: Bill's Blog Release Process
Description: ordered steps to take to produce a new Release of the blog site
category: technical
tags: ["Release Process", Process]
---

Detailed steps to finalize a Feature/Bugfix/Post branch, merge it with `main`, and release a new version of the site.

## Assumptions

This process document was written assuming the developer is using Visual Studio Code (VSC) with both GitLens and GitGraph plugins. Instructions in this document may refer to either interactions with the VSC plugins, or may be provided as Git commands to be run in a CLI.

This process document assumes that there is no development work directly on `main`. All changes are done in separate branches. There are currently three kinds of development branches.

- Feature branches - these branches are where new features to the site are developed and tested. They may include Bugfix work when the bug is minor and fixing it can be rolled into new feature effort. A Feature release can also incorporate new Post(s) work when a Release milestone calls for a new post, e.g. the posts in the ongoing series "How I setup this Github Pages blog site" are part of each version's Feature effort, and one such post is released with each Feature release. When a Feature branch is merged into `main`, the Major or Minor numbers of the site's Semantic Version will be incremented.
- Bugfix branches - these branches are created to fix bugs that have been recorded in the repository's Issues list. These are typically short lived branches with very limited changes, aimed at addressing specific deficiencies in the site. They are typically developed in parallel with Feature branches. When a Bugfix branch is merged into `main`, the Patch number (third part of the Semantic Version) will be incremented.
- Post branches - a new branch created for the purpose of releasing a new published post, or significant editorial reworking of an existing published post. These branches are typically very short-lived, and are used to move a post from the draft state to a published state. When a Post branch is merged into `main`, the patch number of the site's Version will be incremented.

Git branches are lightweight and easy to create. This document assumes that there are "more than one" active branches, and that all development work is being tracked in a branch. This document is focused on the steps needed to release / merge one active development branch into `main`, and update the production site with the work done on the development branch.

The branch being released will be referred to as the Release Candidate in this document.

## Ensure the <Feat/Bug/Post-Branch> meets release criteria and is built atop the latest `main`

Prerequisites:

- The development work on the branch meets the criteria set out in the [Bill's Blog Pre-Release Checklist]({{ '/technical/2021/2021-05-22-bills-blog-pre-release-checklist.html' | relative_url }}). This ensures the new work meets the standards expected for a release.
- The `main` branch has no changes to it since the last Release tag was applied. The `main` branch builds and serves cleanly, with the value of the environment variable `JEKYLL_ENV` set to 'production' and without the `--drafts` option.

Steps:

1. Ensure the `main` branch builds cleanly, without the `--drafts` option.
1. Checkout the <Feat/Bug/Post-Branch> (the Release Candidate).
1. [Publish all draft posts]({{ '/technical/2021/2021-05-22-bills-blog-pre-release-checklist.html#steps-to-publish-a-draft-post' | relative_url }}) that are part of this release.
1. Run `$env:JEKYLL_ENV = 'production'; bundle exec jekyll serve` to ensure that `_site` is built with no drafts and with comments enabled.
1. Run `git rebase -i main` to pull any prior release changes to `main` into the Release Candidate branch. Following the [Bill's Blog Pre-Release Checklist]({{ '/technical/2021/2021-05-22-bills-blog-pre-release-checklist.html' | relative_url }}) should ensure that this step has already been done, but redoing this step here ensures that no recent updates to `main` are missed. If there are no recent updates, this step takes very little time / effort.
1. If there are any recent updates to `main`, then rebase the Release Candidate branch onto `main`, and recheck the Release Candidate branch with [Bill's Blog Pre-Release Checklist]({{ '/technical/2021/2021-05-22-bills-blog-pre-release-checklist.html' | relative_url }}) to ensure the changes didn't break anything, and restart this release process.
1. Always ensure that `$env:JEKYLL_ENV = 'production'; bundle exec jekyll serve` is run after the final Release Candidate code change is made, so that `_site` is up-to-date.

## Final soft reset and commit on the <Feat/Bug/Post-Branch>

The purpose of the soft reset and commit is to clean up the commit messages and make them ready for the ChangeLog, and to cleanup all the changes and eliminate dross in the change list. If the individual commit messages have been well written, the chore of making a good <Feat/Bug/Post-Branch> release commit message shouldn't be too hard.

### Create the summary commit message from the commits made on the Release Candidate branch

1. Run

    ```text
    git log --pretty="format:%b" HEAD...$(git merge-base main $(git rev-parse --abbrev-ref HEAD)) > $env:TEMP/git_message_for_squash.md
    ```

1. Run

    ```text
    code $env:TEMP/git_message_for_squash.md
    ```

1. Edit the file and create the summary commit message for the release.
1. Copy the summary commit message into the `ChangeLog.md` file.
1. Run `$env:JEKYLL_ENV = 'production'; bundle exec jekyll serve` and validate the `ChangeLog` page looks as expected. Stop the local Jekyll server.

### Soft-reset the Release Candidate branch to eliminate mis-steps in the branch development

1. Run the following to reset the head of the Release Candidate branch to the head of `main`.

    ```text
    git reset --soft $(git merge-base main $(git rev-parse --abbrev-ref HEAD))
    ```

1. Run `git add .` to add the current state of the Release Candidate branch to the next commit.
1. Run `git commit`. Title should be `FEAT Milestone VX.XX.XXX`, or `BugFix Issue #XX`, or `Post "<ShortTitle>"` Paste the final commit message as the body of the commit. Close the editor.

At this point the Release Candidate should be complete. If you discover additional issues to be addressed, fix them and then repeat the steps in this section.

## Merge the Release Candidate branch with the `main` branch

Many organizations require a pull request to perform a merge. That's a great idea as soon as your site has any collaborators, but its overkill for a solo developer.  I'll add instructions and templates for a Pull Request process in a later update to this post. For now just merge the two branches.

1. Run `git checkout main` to change to the `main` branch.
1. Run `git merge <Feat/Bug/Post-Branch>` to perform the merge. If the [Bill's Blog Pre-Release Checklist]({{ '/technical/2021/2021-05-22-bills-blog-pre-release-checklist.html' | relative_url }}) was followed, there should be no merge conflicts.
1. Commit all changes on `main`. Use `Chore Release Work for <Feat/Bug/Post-Branch>` as the commit title

## Add a Release tag

Now that the merge has been made, add a Release tag to `main` .

1. Run `git tag -a releases/X.XX.XXX -m "Fourth release of Bill's Blog"` Modify the command as appropriate for the specific release being made
1. Run `git tag` (which will list all existing tags) and verify the new tag is there.

## Final build of production site

1. Run `$env:JEKYLL_ENV = 'production'; bundle exec jekyll serve`
1. Validate the final production build, including the Release Version in the footer, is correct.
1. Commit all changes on `main` (these should only be `_site` changes). Note the commit ID.
1. Run `git tag -f releases/X.XX.XXX`  which should produce the result `Updated tag 'releases/X.XX.XXX' (was c7f1fab)` (the commit number will always be different from this example). This will move the tag forward to the most recent commit.
1. View the tag locally to ensure it is present and associated with the correct commit ID (should be the very latest commit on `main`).
1. Run `git push --atomic origin main refs/tags/releases/X.XX.XXX` to push both the final commit on `main` **AND** the associated release tag to GitHub.
1. Validate that the `Deploy` Github Action was invoked and ran successfully. See [Review the workflow run]({{ '/technical/2021/2021-04-06-how-i-setup-this-github-pages-blog-site-part-01.html#review-the-workflow-run' | relative_url}}) for details
1. Validate the production site is up, with the new features, new published posts, and correct Release Version number.

## Rebase all active branches onto the new HEAD of `main`

Now that the Release Candidate branch has been merged into `main` and the official release to production has ocurred, all/any active branches should be rebased onto the new HEAD of the `main` branch.

Repeat the following steps for all active `Feat/Bug/Post-Branch` branches

1. Checkout `Feat/Bug/Post-Branch`
1. Run `git rebase -i main`
1. Resolve any merge conflicts

Review the commit log. If there are a number of commits in the bugfix branch, squash them together, and edit the comments to be a clean edited description of the changes.
