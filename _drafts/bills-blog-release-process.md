---
title: Bill's Blog Release Process
Description: ordered steps to take to produce a new Release of the blog site
category: technical
tags: [Release Process, Process]
---

Detailed steps to finalize a Feature/Bugfix/Post branch, merge it with `main`, and release a new version of the site.

## Assumptions

This process document assumes that there is no development work directly on `main`. All changes are done in separate branches. There are currently three kinds of development branches.

- Feature branches - these branches are where new features to the site are developed and tested. They may include Bugfix work when the bug is minor and can fixing it can be rolled into new feature effort. A Feature Release can also incorporate new Post work when a Release milestone calls for a new post, e.g. the posts in the ongoing series "How I setup this Github Pages blog site" are part of each version's feature effort, and one such post is released with each feature Release. When a Feature branch is merged into `main`, the Major or Minor numbers of the Semantic Version will be incremented.
- Bugfix branches - these branches are created to fix bugs that have been recorded in the repository's Issues list. These are typically short lived branches with very limited changes, aimed at addresses specific deficiencies in the site. They are typically developed in parallel with Feature branches. When a Bugfix branch is merged into `main`, the Patch number (third part of the Semantic Version) will be incremented.
- Post branches - a new branch created for the purpose of releasing a new published post, or significant editorial reworking of an existing published post. These branches are typically very short-lived, and are used to move a draft post to a published post. When a Post branch is merged into `main`, the patch number of the site's Version is incremented.

The criteria and steps to create new branches is discussed in [TBD](). This document assumes that there are "more than one" active branches that have been created to track development work, and that all development work is being tracked in a branch. This document is focused on the steps needed to release one active development branch into `main`, and update the production site with the new stuff.

The branch being released will be referred to as the Release Candidate in this document.

## Ensure the <Feat/Bug/Post-Branch>  meets release criteria and is built atop the latest `main`

- The development work on the branch meets the criteria set out in the [Bill's Blog Pre-Release Checklist](bills-blog-pre-release-checklist.md). This ensures the new work meets the standards expected for a release.
- The `main` branch has no changes to it since the last Release tag was applied. The `main` branch builds and serves cleanly, without the `--drafts` option.

1. Ensure the `main` branch builds cleanly, without the `--drafts` option.
1. Checkout the <Feat/Bug/Post-Branch> ( the Release Candidate) with Visual Studio Code (VSC).
1. Publish all draft posts that are part of this release.
1. Run `$env:JEKYLL_ENV = 'production'; bundle exec jekyll serve` to ensure that `_site` has been built with no drafts and with Disqus enabled.
1. Run `git pull rebase -i main` to pull any prior release changes to `main` into the Release Candidate branch. Following the [Pre-Release Checklist](bills-blog-pre-release-checklist.md) should ensure that this step has already been done, but redoing this step here ensures that no recent updates to `main` are missed. If there are no recent updates, this step takes very little time / effort.
1. If there are any recent updates to `main`, then recheck the Release Candidate branch with [Bill's Blog Pre-Release Checklist](bills-blog-pre-release-checklist.md) to ensure the changes didn't break anything, and restart this release process.
1. Always ensure that `$env:JEKYLL_ENV = 'production'; bundle exec jekyll serve` is run after the final Release Candidate code change is made, so that `_site` is up-to-date.

## Final soft reset and commit on the <Feat/Bug/Post-Branch>

The purpose of the soft reset and commit is to clean up the commit messages and make them ready for the ChangeLog, and to cleanup all the changes and eliminate dross in the change list. If the individual commit messages have been well written, the chore of making a good <Feat/Bug/Post-Branch> release commit message shouldn't be too hard.

1. Run `git log --pretty="format:%b" HEAD...$(git merge-base main $(git rev-parse --abbrev-ref HEAD)) > $env:TEMP/git_message_for_squash.md`
1. Run `code $env:TEMP/git_message_for_squash.md`
1. Edit the file and create the final commit message for the release.
1. Copy the final commit message into the `ChangeLog.md` file
1. Run `$env:JEKYLL_ENV = 'production'; bundle exec jekyll serve` and validate the `ChangeLog` looks as expected. Stop the local Jekyll server.
1. Run `git reset --soft $(git merge-base main $(git rev-parse --abbrev-ref HEAD))` to reset the head of the Release Candidate branch to the head of `main`.
1. Run `git add .` to add the current state of the Release Candidate branch to the next commit.
1. Run `git commit`. Title should be `FEAT Milestone VX.XX.XXX`, or `BugFix Issue #XX`, or `Post "<ShortTitle>"` Paste the final commit message as the body of the commit. Close the editor.
1. Sync the local `<Feat/Bug/Post-Branch>` with the remote.

At this point the Release Candidate should be complete. If you discover additional issues to be addressed, fix them and then repeat the steps in this section.

### Merge the `<Feat/Bug/Post-Branch>` branch with the `main` branch

Many organizations require a pull request to perform a merge. That's a great idea as soon as your site has any collaborators, but its overkill for a solo developer.  I'll add instructions and templates for a Pull Request process in a later update to this post. For now just merge the two branches.

1. Run `git checkout main` to change to the `main` branch.
1. Run `git merge <Feat/Bug/Post-Branch>` to perform the merge. If the [Bill's Blog Pre-Release Checklist](bills-blog-pre-release-checklist.md) was followed, there should be no merge conflicts.
1. Commit all changes on `main`. Use `Chore Release Work for <Feat/Bug/Post-Branch>` as the commit title

### Add a Release tag

Now that the merge has been made, add a Release tag to `main`

1. Run `git tag -a releases/X.XX.XXX -m "Third release of Bill's Blog"` Modify the command as appropriate for the specific release being made
1. Run `git tag` (which will list all existing tags) and verify the new tag is there.

### Final build of production site

1. Run `$env:JEKYLL_ENV = 'production'; bundle exec jekyll serve`
1. Validate the final production build, including the Release Version in the footer, is correct.
1. Commit all changes on `main` (these should only be `_site` changes). Note the commit ID.
1. Run `git tag -f releases/X.XX.XXX`  should result `Updated tag 'releases/X.XX.XXX' (was c7f1fab)` and the commit number will always be different from this example. This will move the tag forward to the most recent commit.
1. View the tag locally ensure it is present and associated with the correct commit ID (should be the very latest commit on `main`).
1. Run `git push --atomic origin main refs/tags/releases/X.XX.XXX` to push both the final commit on `main` **AND** the associated release tag to GitHub.
1. Validate that the `Deploy` Github Action was invoked and ran successfully.  ToDo: reference the instructions back in `... part 01`
1. Validate the production site is up, with the new features, new published posts, and correct Release Version number.



Written for "Visual Studio Code" with both GitLens and GitGraph plugins

The VCS SCM tool should not be illuminated with a number.

Review the commit log. If there are a number of commits in the bugfix branch, squash them together, and edit the comments to be a clean edited description of the changes.

## Create a new branch for the update

Run `git checkout -b <Post/Bug/Feat-BranchName>` (or use VSC)

Review the commit log. If there are a number of commits in the bugfix branch, squash them together, and edit the comments to be a clean edited description of the changes.

`git checkout main`

git merge *BugFixBranchName*

sync main with remote

build locally and validate bug has been fixed.

git tag -a releases/0.02.001 -m "Bill's Blog, Fix Issue #9"

git tag

$env:JEKYLL_ENV = 'production'; bundle exec jekyll serve

git tag -f releases/0.02.001  should result `Updated tag 'releases/0.02.001' (was c7f1fab)` and the commit number will always be different from this example.

commit the _site changes on main


Switch to the Feature branch `SprintForRelease0.03.000`

Run `git pull --rebase` to bring the bugfix patch into the feature development branch. 

sync the feature branch with the remote

Do the same for any / all other branches being worked.

## Release post, merge into `main` and update site version.

1. Commit the staged and unstaged changes.
1. Follow the [Site Minor Release checklist](TBD - anchor in another document?, `..Part 03`)
 - Correction to pull. Don't use git pull rebase -i main just use git rebase -i --onto main. If the post branch's base is still pointing at the same commit as the HEAD of main, there will be a message that there are no commits. Abort the rebase and move on. 
1. As often as necessary, commit changes, using `Chore commit Production build` .
  ***Note: if publishing runs over midnight, "nnndays ago" used in multiple places, gets updated, and multiple files may get changed.
1. Squash the post's branch's commits, see [Final soft reset and commit on the `Post<insert name>` branch](ToDo: link) .
1. Copy the commit message to the top of the `ChangeLog.md` .
1. Rebuild and validate the `_site's` `ChangeLog.md` the looks correct. Repeat as necessary.
1. final commit using `Chore commit Production build` 
1. Put the final version of the text for this release's ChangeLog into the copy buffer.
1. Run git reset --soft $(git merge-base main $(git rev-parse --abbrev-ref HEAD))
1. Run `git add .` to stage the cumulative changes.
1. Run `git commit` .

### Merge the `postXXX` branch with the `main` branch

1. Ensure the Post branch has been rebased on the latest `main`.  Run `git rebase -i main` to pull any last-minute changes to `main` into the `<Post/Bug/Feat-BranchName>` branch. If there are no changes to `main`, then there should be just one commit in the commit list, and `pick` is the operation selected for it. Hit `Start Rebase` (from GitLens Interactive Rebase). You should see the message `Successfully rebased and updated refs/heads/`<Post/Bug/Feat-BranchName>` .
1. Switch to main branch, either with `git checkout main`, or using VSC.
1. Run `git merge <Post/Bug/Feat-BranchName>` to perform the merge. If the pre-release checklist was followed, there should be no merge conflicts.
1. Commit all changes on `main`. Use `Chore Release Work for <NextReleaseVersion>` as the commit title.

### Add a Release tag

Now that the merge has been made, add a Release tag to `main`

1. Run `git tag -a releases/<NextReleaseVersion> -m "<message appropriate for release>"` (modify the command as appropriate for your site)
1. Run `git tag` which will list all existing tags and verify the tag is there.

### Final build of production site

1. Run `$env:JEKYLL_ENV = 'production'; bundle exec jekyll serve`
1. Validate the final production build, including the Release Version in the footer, is correct. Stop the local Jekyll server.
1. Commit all changes on `main` (these should only be `_site` changes). Note the commit ID.
1. Run `git tag -fa releases/<NextReleaseVersion>` -m "<message appropriate for release>". It will open an editor window in VSC, simply close it as we should not need to make any changes to the tag message.

1. View the tag locally ensure it is present and associated with the correct commit ID (should be the very latest commit on `main`).
1. If you are correcting a mistake in a prior loop, and have already pushed the tag to the remote, it has to be removed from the remote. In this case, run `git push origin :refs/tags/releases/<NextReleaseVersion>` to push an empty tag to the remote
1. Run `git push --atomic origin main refs/tags/releases/<NextReleaseVersion>` to push both the final commit on `main` **AND** the associated release tag to GitHub.
1. Validate that the `Deploy` Github Action was invoked and ran successfully.  ToDo: reference the instructions back in `... part 01`
1. Validate the production site is up, with the new features, new published posts, and correct Release Version number.

### Remove the `<Post/Bug/Feat-BranchName>` branch

#### Use VSC Git 

1. Switch to `main` branch.
1. Expand the `Branches` window
1. right-click the `<Post/Bug/Feat-BranchName>` branch to be removed
1. Select `Delete...`
1. Chose to delete both the local and the remote tracking branch.
1. Confirm...
1. View the `Git Graph` and validate the <Post/Bug/Feat-BranchName>` branch has been removed both locally and remotely. ToDo: insert jpg

#### Use command line Git

1. ToDo: Add list of CLI git commands

### Rebase any Feature or Bug branches onto the latest `main`

1. Switch to the <Post/Bug/Feat-BranchName> to be rebased.



## Create new branch for work on new post

Run git checkout -b <NameOfBranchForPost> (or use VSC)

## Create the new draft post

Run `bundle exec jekyll draft "Name Of Your Draft`

Edit the draft until you are ready to publish it.
