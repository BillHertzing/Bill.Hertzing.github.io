---
Title: How I setup this GitHub Pages Blog, Part 3
tags: Jekyll GitHubPages
description: Third steps in setting up a Jekyll generated blogging site hosted on GitHub Pages which uses any plugin, theme, Jekyll version or Ruby version.
category: technical
---

Welcome to the third part of this series detailing how I setup this blog site hosted on GitHub Pages. If you have not yet seen the first two post in the series [How I setup this GitHub Pages Blog Site Part 01]({{ '/technical/2021/2021-04-06-how-i-setup-this-github-pages-blog-site-part-01.html' | relative_url }}) and [How I setup this GitHub Pages Blog Site Part 02]({{ '/technical/2021/2021-04-17-how-i-setup-this-github-pages-blog-site-part-02.html' | relative_url }}) you should probably give them a quick review, to become familiar with how the site has been built up to this point.

The next steps will be to implement the features specified in [Milestone 0.03.0](https://github.com/BillHertzing/BillHertzing.github.io/milestone/3).  I've created Milestones for Release V0.03 and V0.04 already. I also have a lot of ideas for additional features in a Milestone *Release Far Future*.  I like to plan one or two milestones in advance of the current sprint. That gives me time to study the Internet for examples and guidelines for the specific new features coming in the next two releases. I also arrange the Milestone *Release Far Future* features in the rough order of prioritization I want, then when creating a new specific milestone, I move an appropriate number of features from Milestone *Release Far Future* into the new next Release milestone. I'll say this again, I've found that there is always "feature creep" in releases if I don't take the time to write down what is going into the next release. This helps me keep to the release cadence I want, and ensures these posts corresponding to each release don't get too big!

This release is all about moving to a better theme, adding navigation elements, and incorporating Disqus comments.

Lets move on!

## Create a new branch for developing the next Release

First step after doing a Release is to create a new branch for working on the features for the next Release.  

 1. Run `git checkout main` to switch to the just released Release. Hopefully, it is clean and there have been no changes since the last release tag was added.
 1. Run `git checkout -b SprintForRelease0.03.000` to create a branch for the work on the next release. Modify the branch name shown to reflect the number of the next release. For this post and the development of the next Release of this site, I'll keep coming back to the branch `SprintForRelease0.03.000` with the command `git checkout SprintForRelease0.03.000`.

## Work on bugs in parallel with new features

Every release brings new bugs. I always want to be working on exciting new features, not trying to figure out my past mistakes 😞. Gotta do it though, so it's best to get into a rhythm for working on both areas.

1. Use Github issues to record bugs found in the current release.
1. Create a branch to work on each bug issue.
1. Run `git checkout main` to switch back to the just released Release.
1. Run `git checkout -b BugFixIssue#9` to create a branch for the work on fixing the bug. Modify the branch name shown to reflect the Issue number.
1. If you have another issue that you want to work in parallel, fork another branch from `main`. Not too many though, because each time a bugfix branch is merged into `main`, the other bugfix branches will need to be rebased. Having just a couple bugfix branches existing and being worked on makes the process of merging and rebasing easier.

Once you have a few parallel branches setup, you can decide which branch you want to work on today. 😊

Later in this post I'll show how I merge the bug fix branches back into `main`, and then `git rebase -i` development sprint and bugfix branches onto the updated `main`.

## Update the git.commit.template

There is only one template for commits, and since I'm working primarily on Release V0.03.000, it's time to change the default template to reflect that.

1. Open the file `GitTemplates/git.commit.template.txt`
1. Find the line `See Milestone Release V0.02.00` and change it to `See Milestone Release V0.03.00`
1. Save the file. The new changed template should appear the next time the VSC SCM tool window is opened.

## Create a draft `... Part 03` post

1. Create the file `how-i-setup-this-github-pages-blog-site-part-03.md` under the `technical/_drafts` subdirectory (or under the `_drafts` subdirectory at the base of the repo if you are not using categories). Do not add the *YYYY-MM-DD* prefix to this file.
1. Add the following Front Matter text to the file. Modify it as appropriate for your site. *Note* There is no `date:` key in a draft post.

    ```markdown
    ---
    Title: How I setup this GitHub Pages Blog, Part 3
    tags: Jekyll GitHubPages
    description: third set of steps in setting up a Jekyll generated blogging site hosted on GitHub Pages which uses any plugin, theme, Jekyll version or Ruby version.
    ---

    Add text you want to see in your third post
    ```

1. Save the file.
1. Run `bundle exec jekyll serve --drafts` Jekyll will build the drafts with the current date so they will be easy to find at the top of your (chronologically sorted) post listings.
1. Validate the new post exists locally under the `technical` subdirectory, and a link to the `... Part 03` post appears at the top of the landing page.
1. Commit the file, sync with Github, and verify the GiHub repository now has the new branch `SprintForRelease0.03.000` and the new `... Part 03` file under `technical/_drafts`.

> **NOTE** During this period in the development of the site, Real Life interfered in the form of the passing of our dear dog Molly. Since one purpose of the site is to post updates regarding real-life happenings to friends and family, the features destined for release V0.03 were re-prioritized to support posting a Eulogy for Molly. This primarily involved doing the minimum needed to convert to the Minimal Mistakes theme, customizing the footer, customizing the Author information, customizing the favicon, and customizing the `gallery` component to support captions for the images in the gallery, using that modified component to create the picture gallery found in the eulogy post, creating a `favicon` and adding a Table Of Contents (TOC) to posts. The remainder of the features originally planed for V0.03 have slipped to V0.04.

## Change theme to Minimal Mistakes (MM)

Now we'll switch to a better theme. I decided to use [Minimal Mistakes](https://mmistakes.github.io/minimal-mistakes/). Installation details are in the [Quick-Start Guide](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/). What follows are the steps I took and the choices I made during installation.

### Add the `minimal-mistakes-jekyll` Gem-based theme to the `Gemfile`

1. Edit the `Gemfile` in the base of the repo.
1. Replace `gem "minima", "~> 2.5"` with this:

  ```yml
  gem "minimal-mistakes-jekyll"
  ```

1. Save the file.
1. Run `bundle` to fetch and update bundled gems.

### Finding the files that make up the theme

There are a number of theme files that will need to be overridden. When creating an override for a file, start with the theme's file. To locate theme files, run `bundle info minimal-mistakes-jekyll`. That will return the path of the Gem theme's installation directory. From that root path, all of the theme's files can be found.  Alternatively, the latest versions of all theme files can be found on the MM Github site, at [Minimal Mistakes](https://mmistakes.github.io/minimal-mistakes/). However, be careful that the version installed locally matches the version on the GitHub site.

### Merge MM default values of `_config.yml`

The MM theme has a default file for `_config.yml`. I compared the theme's default `_config.yml` file with the `_config.yml` file currently in use on my site, then merged the two, updating the resulting file with additional information specific to my site. There were a lot of setting in the new file with which I was unfamiliar. This post and subsequent posts will go into greater detail on the contents of this file and how it was modified.

1. Combine the latest version with the current version
    2. uncomment the `# theme` line
    2. update the `title:` key value
    2. update the `subtitle:` key value
    2. update the `name:` key value
    2. update the `description:` key value
    2. update the `url:` key value
    2. update the `repository:` key value
    2. update the `Author:` subkey values
      1. update the `name:` key value
      1. update the `bio:` key value
      1. update the `location:` key value
      1. update the `name:` key value
      1. update the `links:` subkey values
      1. uncomment and update the `url:` key values for any social media sites you want to appear under your Author information.
    > **NOTE** I do NOT recommend enabling email links unless you are willing to deal with a lot of spam in your inbox!
    1. update the `footer:links:` subkey values
    1. uncomment and update the `url:` key values for any social media sites you want to have links to appear in the footer.
    1. update the `timezone:` key value
    1. update the `plugins:` key. There are three additional plugins defined in the theme that are not present in the current version. Add all three
        - jekyll-paginate
        - jekyll-sitemap
        - jekyll-gist
    1. Save the file.

### Install additional GEMs

The MM theme references three additional plugins. Install them using the commands

1. Run `gem install jekyll-paginate`
1. Run `gem install jekyll-sitemap`
1. Run `gem install jekyll-gist`
1. Run `bundle update`

The results of running update will be a list of gems and their versions. Note the version numbers of the gems that match the plugins specified in the `_config.yml`

Update the `Gemfile`. The versions shown here are those that existed on April 23, 2021.

```yml
group :jekyll_plugins do
  gem "jekyll-paginate", "~> 1.1.0"
  gem "jekyll-sitemap", "~> 1.4.0"
  gem "jekyll-gist", "~> 1.5.0"
  gem "jekyll-feed", "~> 0.15.1"
  gem "jekyll-include-cache", "~> 0.2.1"
  gem "jekyll-timeago", "~> 0.14.0"
  gem "jekyll_version_plugin", "~> 2.0.0"
end
```

Save the Gemfile

Run `bundle exec jekyll serve --drafts`.

Oops, the site build did not finish and there are errors reported. Gotta work through the troubleshooting.

### Change `post` layout to `posts` layout

The `minima` theme had a layout named `post`, but MM uses a layout called `posts`. In all the posts for Release V0.01 and V0.02, each post had a Front Matter `layout:` key. Fix this by removing the `layout:` key from the Front Matter in all posts. The Default Front Matter in the `_config.yml` file will take care of defining the layout for all posts

1. Use VSC global search feature to find the string `layout: post`.
1. Go into each file and remove that line if it is within the files' Front Matter.

### Change `page` layout

The `minima` theme had a layout named `page`, but MM does not. Fix this by modifying the `layout:` key in the Front Matter in all pages, and use a layout specific to the page's intent.

1. Repeat the steps used to fix the `post` layout. Global search for `layout: page`, replace it as follows:

    1. in the `index.md` file (at the root of the repo), use `layout: home`
    1. in all other page files, remove the `layout:` key line completely.

1. Run `bundle exec jekyll serve --drafts`

Looks like this cleaned up all the warnings about missing the layout `post` and missing the layout `page`. Validate that the site builds and serves.

## Fix the `footer`

Eventually, I want the footer to look similar to the footer at GitHub Marketplace Action [Deploy to GitHub Pages](https://github.com/marketplace/actions/deploy-to-github-pages). However, for this release, I'll start with just the copyright, the License, Code of Conduct, and Contributing links, attributions for Jekyll and MM, and the current Release's Semantic Version number.  This is done by overriding the default `includes/footer.html` file .

1. Copy the file `_includes/footer.html` from the `minimal-mistakes-jekyll` theme's installation directory to the local repo's `_includes` subdirectory.
1. Edit the copyright line, replace the entire line with the following (and modify to fit your site):

    ```Liquid
    <div class="page__footer-copyright">&copy; William Hertzing 2020 - 2021. Licensed under the terms of the <a href={{ "/LICENSE/" | relative_url }}>MIT License.</a>
    <a href=https://github.com/BillHertzing/.github/blob/main/CODE_OF_CONDUCT.md>Code of Conduct</a>
    <a href=https://github.com/BillHertzing/.github/blob/main/CONTRIBUTING.md>CONTRIBUTING</a> 
    {{ site.data.ui-text[site.locale].powered_by | default: "Powered by" }} <a href="https://jekyllrb.com" rel="nofollow">Jekyll</a> &amp; <a href="https://mademistakes.com/work/minimal-mistakes-jekyll-theme/" rel="nofollow">Minimal Mistakes</a>.
    Site Release {{ "{%" }} capture long_tag_name %}{{ "{%" }} project_version  %}{{ "{%" }} endcapture %}{{ "{{" }} long_tag_name | remove: 'releases/' | split: '-' | first | prepend: "V" }}</div>
    ```

1. Run `bundle exec jekyll serve --drafts`

The site should build and display, and a decent looking footer should display on all pages and posts. We will address adding to the contents of the footer in later posts.

## Add a `favicon.ico`

I have a .jpg file with an image I'd like to use as the site's Favicon. The HTML needed to generate Favicon references for all kinds of browsers are usually found in each page's `<head>... </head>` section. The MM theme has a place to insert custom HTML for the head tag, `_includes/head/custom.html`. The MM theme's original custom head HTML file is `_includes/head/custom.html`, and in it there is a line the specifically mentions a place to insert html related to the Favicon. It also refers to [Favicon Generator. For real.](https://realfavicongenerator.net/), which lets you take a .jpg file and turn it into a series of .ico files for various browsers. If you don't have a picture you want to use yet, you can just try the Favicon Generator with a default image. The site returns a package of files to be installed into the root of the repo, and a block of HTML to be added to the `<head>... </head>` section of a page.

1. Create a new subdirectory and file `_includes/head/custom.html`.
1. Copy the contents of the MM original file into the local file above, although it is all comments.
1. Add the snippets generated by the [Favicon Generator. For real.](https://realfavicongenerator.net/) to the file.
1. Unpack the `.zip` package that was generated by Favicon Generator into the root of the repo.
1. Run `bundle exec jekyll serve --drafts`

Validate the tab in the browser now includes the favicon.

## Modify the MM `gallery` component to add a title under each picture

I needed to put all of Molly's pictures for her eulogy into a gallery, but I wanted captions under each picture. To do this, I used MM's `gallery` component with a simple modification.

1. Create a file `_includes/gallery`
1. Get the content of the theme's `_includes/gallery` file from the locally installed gem's location.
1. Edit the local file and paste the content from the theme's version of the file
1. Add `<span>{{ img.title }}</span>` just below the `<img ...>` tag.

To test this, a post and some pictures will be needed. In my site, the post was "Eulogy for Molly", and I added Front Matter specifying the gallery and the pictures.

## Add basic `TOC` to posts

MM theme comes with support for a basic Table of Contents (TOC) displayed to the right of each post. The TOC can be made sticky to the top of the page. This can be enabled in the Default Front Matter.

1. Edit `_config.yml`
1. Find the `defaults:` key
1. Under the `values:` subkey belonging to the `posts` scope, add the two lines

    ```yml
    toc: true
    toc_sticky: true
    ```

Run `bundle exec jekyll serve --drafts` and validate that the posts now have a TOC displayed on their right. The TOC should remain visible as the post is scrolled down. As the cursor moves to various sections of the post, the appropriate section of the TOC should highlight. Clicking on a section in the TOC should scroll the post to that section.

## Add Disqus comments to posts

There is a lot of opinions on the Internet related to "what is the best way to add a comments section to posts". I decided to use the Disqus approach, primarily because I did not want to have to spend time moderating comments to remove spam. Most people who weighed in on this topic agreed that Disqus had a very good track record in eliminating spam. As of this date, 2021-04-13, Disqus will provide the basic service (no ads) for free if I self-identify as a personal or OSS site. I registered on 2021-04-13, and received an email acknowledgement the next day. I will send a note to their support tomorrow. More on this later.

### Register for an account at Disqus

Go through the [Disqus](https://disqus.com/) registration procedure for a site. Make a note of the `shortname` you enter, it will be a key part of enabling comments below.

### Enable support for Disqus in the MM theme

The MM theme has built-in support for Disqus comments.

1. Edit the `_config.yml` file.
1. Find the `comments:` key.
1. Modify the `provider:` subkey to `provider: "disqus"`
1. Modify the `shortname:` subkey to `shortname: <Your Disqus Shortname>`>, the `shortname` you entered when registering for your Disqus account.
1. Save the file.

> Comments are only visible if the environment specifies an environment variable `JEKYLL_ENV` with a value of `production`. To enable comments, the command that is run to build and serve the site now becomes `$env:JEKYLL_ENV = 'production'; bundle exec jekyll serve` This will instruct PowerShell to create the Environment variable `JEKYLL_ENV` with a value of `production` whose scope is just for the building and serving of the site.

> The command `$env:JEKYLL_ENV = 'production'; bundle exec jekyll serve --drafts` also works, and will produce draft posts with comment sections. Avoid entering any comments while the post is still in draft, as the final name of the post will probably differ (in *YYY-MM-DD* part) from the published full name of the post.

Run `$env:JEKYLL_ENV = 'production'; bundle exec jekyll serve` and validate that the Disqus comments section now appears on the bottom of every post.

## Making the third release of the site

I'm happy now with the enhancements I've made to the blogging site. It's time to wrap up this release.

### Site Minor Release checklist

1. Ensure the `main` branch builds cleanly, without the `--drafts` option.
1. Review any `warnings` that appear in VSC's `problems`. pane. Clean up the underlying issue, or decide they are OK to live with for this release. Commit any changes made during this step to `main` and push to the remote.
1. Update the ChangeLog.md. I simply cleanup the Milestone text and add it to ChangeLog. Commit the ChangeLog.md and push it.
1. Publish the draft `How I setup this GitHub Pages Blog, Part 3` post into `_technical`
1. Publish the draft `Eulogy for Molly the Dog` post into `personal` subdirectory.
1. Run `$env:JEKYLL_ENV = 'production'; bundle exec jekyll serve` to ensure that `_site` has been built with no drafts and with Disqus enabled
1. Run `git pull rebase -i main` to pull any changes to `main` into the `SprintForReleaseXXX` branch. ToDo: add example git commands
1. Run through the *pre-release checklist - ToDo* of things to test in the Release Candidate.
1. If any item is deficient, fix the problem, update code and commit again until the *pre-release checklist* passes. Always ensure that  `$env:JEKYLL_ENV = 'production'; bundle exec jekyll serve` is run after the final Release Candidate code change is made, so that `_site` is up-to-date.
1. Run `git pull rebase -i main` to pull any last-minute changes to `main` into the `SprintForReleaseXXX` branch.
1. If there were any changes in `main` that were pulled into the feature branch, run the *pre-release checklist* again. Always ensure that  `$env:JEKYLL_ENV = 'production'; bundle exec jekyll serve` is run after the final Release Candidate code change is made, so that `_site` is up-to-date.

### Final soft reset and commit on the `SprintForReleaseXXX` branch

The purpose of the soft reset and commit is to clean up the commit messages and all the changes and make them ready for the ChangeLog. If the individual commit messages have been well written, the chore of making a good Feature Release commit message shouldn't be too hard.

1. Run `git log --pretty="format:%b" HEAD...$(git merge-base main $(git rev-parse --abbrev-ref HEAD)) > $env:TEMP/git_message_for_squash.md`
1. Run `code $env:TEMP/git_message_for_squash.md`
1. Edit the file and create the final commit message for the Feature Release.
1. Copy the final commit message into the `ChangeLog.md` file
1. Run `$env:JEKYLL_ENV = 'production'; bundle exec jekyll serve` and validate the ChangeLog looks as expected. Stop the local Jekyll server.
1. Run `git reset --soft $(git merge-base main $(git rev-parse --abbrev-ref HEAD))` to reset just the head of the feature branch to the head of `main`.
1. Run `git add .` to add the current state of the Feature branch to the next commit.
1. Run `git commit`. Title should be `FEAT Milestone V0.03.000` Paste the final commit message as the body. Close the editor.

### Merge the `SprintForReleaseXXX` branch with the `main` branch

Many organizations require a pull request to perform a merge. Thats a great idea as soon as your site has any collaborators, but its overkill for a solo developer.  I'll add instructions and templates for a Pull Request process in a later post. For now just merge the two branches.

1. Ensure the `SprintForReleaseXXX` branch is based at the head of `main`. ToDo: add examples git commands
1. Run `git checkout main` to change to the `main` branch.
1. Run `git merge SprintForReleaseXXX`  to perform the merge. If the pre-release checklist was followed, there should be no merge conflicts.
1. Commit all changes on `main`. Use `Chore Release Work for V0.03.000` as the commit title

### Add a Release tag

Now that the merge has been made, add a Release tag to `main`

1. Run `git tag -a releases/0.03.000 -m "Third release of Bill's Blog"` (modify the command as appropriate for your site)
1. Run `git tag` which will list all existing tags and verify the tag is there.

### Final build of production site

1. Run `$env:JEKYLL_ENV = 'production'; bundle exec jekyll serve`
1. Validate the final production build, including the Release Version in the footer, is correct. Stop the local Jekyll server.
1. Commit all changes on `main` (these should only be `_site` changes). Note the commit ID.
1. Run ToDo: insert git commands to move the tag forward one commit.
1. View the tag locally ensure it is present and associated with the correct commit ID (should be the very latest commit on `main`).
1. Run `git push --atomic origin main refs/tags/releases/0.03.000` to push both the final commit on `main` **AND** the associated release tag to GitHub.
1. Validate that the `Deploy` Github Action was invoked and ran successfully.  ToDo: reference the instructions back in `... part 01`
1. Validate the production site is up, with the new features, new published posts, and correct Release Version number

## Wrapping up

This concludes the third post in this series. I'm sure that there will be revisions to this post for typos, grammar, and general improvements. Future site revisions will support multiple editions of a post, with revision date and ChangeLog for the post. You will (eventually) be able to subscribe to the site's feed and get notifications when a revision is made.

This is the first release that supports Comments for posts. I'll provide feedback in the next `... Part 04` post as to how well that works (spam, comment author's ID, etc).

Thanks for staying to the end! 😊

Bill Hertzing, April 24, 2021

{% comment %}

I wanted to know if I created `_drafts` under the root subdirectory `technical`, and put a draft post there, would Jekyll find the file and build it into the correct subdirectory? The answer was yes!

1. Create the folder `_drafts` under the subdirectory `technical`.

{% endcomment %}
