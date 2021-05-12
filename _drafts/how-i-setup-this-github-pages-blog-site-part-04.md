---
Title: How I setup this GitHub Pages Blog, Part 4
tags: Jekyll GitHubPages
description: Fourth group of steps in setting up a Jekyll generated blogging site hosted on GitHub Pages which uses any plugin, theme, Jekyll version or Ruby version.
category: technical
---

Welcome to the fourth part of this series detailing how I setup this blog site hosted on GitHub Pages. If you have not yet seen the first posts in the series [How I setup this GitHub Pages Blog Site Part 01]({% link technical/_posts/2021-04-06-how-i-setup-this-github-pages-blog-site-part-01.md %}), [How I setup this GitHub Pages Blog Site Part 02]({% link technical/_posts/2021-04-17-how-i-setup-this-github-pages-blog-site-part-02.md %}), and [How I setup this GitHub Pages Blog Site Part 03]({% link technical/_posts/2021-04-24-how-i-setup-this-github-pages-blog-site-part-03.md %}) you should probably give them a quick review, to become familiar with how the site has been built up to this point.

The next steps will be to implement the features specified in [Milestone 0.04.0](https://github.com/BillHertzing/BillHertzing.github.io/milestone/4). I've already created Milestones for Release V0.05, [Milestone 0.05.0](https://github.com/BillHertzing/BillHertzing.github.io/milestone/5) as well and updated the Milestone *Release Far Future* to reflect whats planned for later. Release V0.05 calls for creation of a  Github project for tracking future features,So at that point hopefully, there will be a single point for tracking and reporting on planned and requested features.

## Add a new branch `SprintForRelease0.04.000`

- Run `git branch create SprintForRelease0.04.000`

## Add jekyll-compose

jekyll-compose adds commands that help streamline the creation and publishing of posts. Installation instructions and details can be found in [jekyll-compose](https://github.com/jekyll/jekyll-compose). What follows are th steps I took and choices I made for this site.

1. Edit the Gemfile in the root of the repo.
1. Add `gem 'jekyll-compose', group: [:jekyll_plugins]` just above the `plugins:` key.
1. Run `bundle`

Refer to detailed instructions in [jekyll-compose](https://github.com/jekyll/jekyll-compose) for using the new commands. This post was drafted and published using the commands added by this tool, and it made the process much much easier. I created the draft of this post using the command `bundle exec jekyll draft "how-i-setup-this-github-pages-blog-site-part-04"`, which placed a file containing just Front Matter in the `_drafts` directory.

## Update the commit template

- Edit `GitTemplates/git.commit.template.txt` and change `03` to `04`

## First commit on the sprint branch

Commit the changes and use VSC to synchronize changes with the remote, then inspect the Github repository to ensure the branch and first commit exist on the repo. I like using Git Lens along with Git Graph. ToDo: insert jpg You can see the site development history clearly.

To show what a feature development branch looks like with more than one commit, I'll make a small one now.

Afterwards, this is what it looks like ToDo: insert jpg.

And a third: ToDo: insert jpg

## Add jekyll-minifier

 Minification is the process of rewriting the stream of data sent from the server to the browser to make the stream as small as possible.Minification of your site is something that all good digital properties should do. It's just manners. But this has consequences if a developer is trying to read the data stream and debug problems.

As with any optimization, it is important to measure the baseline, and then the improvement. ToDo: A short tutorial on Fiddler 4. ToDo: Find online site that can quantify the number of bytes. Or see if Fiddler 4 has that capability.

This minifier allows fine control over minification of HTML, JavaScript, CSS, and Json, as well as many more minification options.

Detailed instructions are here at [jekyll-minifier](https://github.com/digitalsparky/jekyll-minifier)

1. Run `gem install jekyll-minifier` Make a note of the version installed, mine was 0.1.10
1. Run `bundle update`
1. Edit `Gemfile` at the root of the repo, and add `gem "jekyll-minifier", "~> 0.1.10"` into the `group :jekyll_plugins do` section.
1. Edit `_config.yml` and add `jekyll-minifier` to the `plugins`: key

  ```yml
  plugins:
    - jekyll-minifier
  ```

1. Further down the `_config.yml` add lines that control the minifier's settings. Add the entire list now, and later we will work through each setting and decide if this site will need it.

  ```yml
  jekyll-minifier:
    preserve_php: true                # Default: false
    remove_spaces_inside_tags: true   # Default: true
    remove_multi_spaces: true         # Default: true
    remove_comments: true             # Default: true
    remove_intertag_spaces: true      # Default: false
    remove_quotes: false              # Default: false
    compress_css: true                # Default: true
    compress_javascript: true         # Default: true
    compress_json: true               # Default: true
    simple_doctype: false             # Default: false
    remove_script_attributes: false   # Default: false
    remove_style_attributes: false    # Default: false
    remove_link_attributes: false     # Default: false
    remove_form_attributes: false     # Default: false
    remove_input_attributes: false    # Default: false
    remove_javascript_protocol: false # Default: false
    remove_http_protocol: false       # Default: false
    remove_https_protocol: false      # Default: false
    preserve_line_breaks: false       # Default: false
    simple_boolean_attributes: false  # Default: false
    compress_js_templates: false      # Default: false
    preserve_patterns:                # Default: (empty)
    uglifier_args:                    # Default: (empty)
    
  ```

> ***es6 support is experimental.***  If your site is using es6 scripts, see the [jekyll-minifier](https://github.com/digitalsparky/jekyll-minifier) documentation for possible issues.

Run `bundle exec jekyll serve --drafts` and ensure the site looks like it should. The re-run the tests that measure the size of the data stream.

## Setup masthead navigation

The MM theme has built-in support for masthead navigation. These are the links that appear across the top of every page, and which collapse down into the navigation hamburger on narrow screens. There is a direct relationship between the files in the `_pages` subdirectory and the navigation links in the `_data/navigation.yml`

## Setup archive pages

The MM theme has two kinds of archive support built in, either a Liquid approach or a `jekyll-archives` approach. I chose to use the `jekyll-archives` plugin.

### Add the `jekyll-archives` gem

1. Run `gem install jekyll-archives`. Mine came back as version 2.2.1.
1. Edit the `Gemfile` in the root of  the repo. Add `gem "jekyll-archives", "~> 2.2.1"` into the `group :jekyll_plugins do` group.
1. Run `bundle update`
1. Run `bundle exec jekyll build` and ensure the site builds correctly.

### Modify `_config.yml` for `jekyll-archives`

1. Edit `_config.yml`, and find the `jekyll-archives` section. Uncomment the settings that appear in MM's default. Mine looks like this:

   ```yml
   jekyll-archives:
    enabled:
      - categories
      - tags
    layouts:
      category: archive-taxonomy
      tag: archive-taxonomy
    permalinks:
      category: /categories/:name/
      tag: /tags/:name/
   ```

### Create override for `_pages/category-archive.md`

There needs to be an `index.html` in the generated sites `/categories/` directory.

1. Add a new subdirectory and file `_pages/category-archive.md` at the root of the repo.
1. Add the following Front Matter to the file. Nothing else is needed.

   ```yml
    ---
    title: "Posts by Category"
    layout: categories
    permalink: /categories/
    author_profile: true
    ---
    ```

1. Run `bundle exec jekyll serve` and ensure the site builds correctly
1. Navigate to `http://localhost:4000/categories/` and validate there is a page listing all current posts organized by category.

### Create override for `_pages/year-archive.md`

There needs to be an `index.html` in the generated `_sites` `/year-archive/` subdirectory.

1. Add a new file `_pages/year-archive.md` at the root of the repo.
1. Add the following Front Matter to the file. Nothing else is needed.

   ```yml
    ---
    title: "Posts by Date"
    layout: archive
    permalink: /years-archive/
    author_profile: true
    ---
    ```

1. Run `bundle exec jekyll serve` and ensure the site builds correctly
1. Navigate to `http://localhost:4000/tags/` and validate there is a page listing all current posts organized by Date.

### Create override for `_pages/tags-archive.md`

There needs to be an `index.html` in the generated sites `/tags/` directory.

1. Add a new file `_pages/tags-archive.md` at the root of the repo.
1. Add the following Front Matter to the file. Nothing else is needed.

   ```yml
    ---
    title: "Posts by Tags"
    layout: Tags
    permalink: /tags/
    author_profile: true
    ---
    ```

1. Run `bundle exec jekyll serve` and ensure the site builds correctly
1. Navigate to `http://localhost:4000/tags/` and validate there is a page listing all current posts organized by tag.

### Modify the look of the `tags-archive` page

I found an archive page layout for tags that I like better than the MM default. To implement this alternative,

ToDo: implement https://justin.kelly.org.au/jekyll-tags-page/ and stylesheet changes https://mmistakes.github.io/minimal-mistakes/docs/stylesheets/

## Setup navigation links

The MM theme has masthead navigation capability built-in. Details on using it are at MM's [Navigation](https://mmistakes.github.io/minimal-mistakes/docs/navigation/) . Here are the steps I took

1. Create a subdirectory and file `_data/navigation.yml` and open it for editing. I started with the following contents:

    ```yml
    ToDo: Add text from real file
    
    ```

Run `bundle exec jekyll serve --drafts` and ensure masthead navigation is present. Play around with making the browser wider and narrower, and note how the horizontal masthead links collapse into a navigation hamburger.

## Setup custom sidebar navigation

The MM theme has the custom sidebar navigation capability built-in. Details on using it are at [Custom sidebar navigation menu](https://mmistakes.github.io/minimal-mistakes/docs/layouts/#custom-sidebar-content) . Here are the steps I took:

1. Edit `_data/navigation.yml` . I added with the following contents:

    ```yml
    docs:
    - title:  Repositories Overview
      children:
        - title: "Overview Guide"
          url: /docs/overview-guide/
        - title: "Structure"
          url: /docs/structure/
        - title: "Testing"
          url: /docs/Testing/
        - title: "ReleaseProcess"
          url: /docs/ReleaseProcess/
        - title: "Upgrading"
          url: /docs/upgrading/
        - title: "EndOfLife"
          url: /docs/EndOfLife/
    - title:  SCM Conventions
      children:
        - title: "SCM for Code, Doc, and DB"
          url: /docs/SCM-Conventions/overview/
        - title: "Code SCM"
          url: /docs/Code-VersionControlProcess/
        - title: "Docs SCM"
          url: /docs/Documentation-VersionControlProcess/
        - title: "DB SCM"
          url: /docs/DataBase-VersionControlProcess/
        - title: "Peer Repository SCM"
          url: /docs/Peer-repository-AutoDoc-VersionControlProcess/
    ```

## Add rule for Git Merge

If a BugFix or new Post goes out on `main` while you are working on a Feature branch, you will need to rebase the feature branch onto the new head of `main`. There are likely to be a lot of files in `_site` with merge conflicts! since `_site` is all generated files, we can safely ignore any merge conflicts in the files under `site`. We can create a merge  to accomplish this by adding a custom merge driver, as follows:

1. Create the file `.gitattributes` in the root of the repo.
1. Add the line `/_site/**/*.* merge=keep-local-changes` and save the file.
1. Create (or edit) the file `~/.gitconfig`, which is your windows HOME directory, and contains the global git configuration settings.
1. Add the following block of text [Geordie answer to this SO question](https://stackoverflow.com/questions/12218977/git-add-merge-rule-to-config-for-specific-file):

   ```text
   [merge "keep-local-changes"]
      name = A custom merge driver which always keeps the local changes
      driver = true
   ```

1. You will need to close VSC and re-open it for the changes to the global `~/.gitconfig` to take effect.

## Rebase Feature branch onto the head of `main` after a site patch/post point release

ToDo: Replace with reference to the proper section in the Release Process document.

## Modify `-includes/gallery`

The `gallery` component opens an image link reusing the same tab as the parent document. Modern practice is to open an image link in a new tab. modify the `gallery` so that the anchor href now includes `target = "_blank" rel="noopener noreferrer"` . This will tell browsers to open the image in a new tab.

## Add the page `_pages/subscribe-to-bills-blog.md`

The page provides instructions on using [IFTTT](https://ifttt.com/) to subscribe to the site's RSS feed. Add the page `subscribe-to-bills-blog.md` to the root of the repo. The Front Matter should look like this:

  ```yml
    layout: single
    permalink: /subscribe-to-bills-blog/
    description: How to subscribe to posts from Bill's Blog site
    tags: [subscribe, "RSS Feed"]
    Category: technical
    ---   
  ```

Add content to the page explaining the steps necessary to setup an IFTTT trigger and target action that produces an e-mail message whenever the site's RSS feed indicates a change has been made to the site.

### Update masthead navigation

- Edit `_data/navigation.yml`
- Add the following to the `main` section:

  ```yml
   - title: "Subscribe"
      url: /subscribe-to-bills-blog/
  ```

## Add `ads.txt` file from Disqus

ADS stands for Authorized Digital Sellers. You can read more about ads.txt and the rationale for creating it, at [Ads.txt FAQ](https://help.disqus.com/en/articles/1765332-ads-txt-faq)  Disqus and other companies have cooperated to identify sellers with validated reputations. Disqus expects this file to be present in the root of the site. 

1. Create the file `ads.txt` in the root of the repo.
1. Copy the contents of https://disqusads.com/ads.txt into the file `ads.txt`
1. Save the file

This file needs to be maintained monthly. Setup a reminder to regularly compare the latest version of the file with the one local to your site, and update your local copy accordingly.

[ToDo: write a script to automate this, and reference the script here.]
[ToDo: write a post how to automate this, and schedule it to run monthly and notify the site admin's list.]

## Add draft post `bills-blog-pre-release-checklist.md`

ToDo:

## Add draft post `bills-blog-release-process.md`

ToDo:

## Add any `personal` posts to be published

If you have created any `personal` or `political` posts while working on this feature release, and would like to publish those posts along with this site release, follow the steps in the [Bills Blog Pre-Release Checklist](https://technical/<date>-bills-blog-pre-release-checklist) post and apply the post validation tests to any posts to be released

## Validate this post (..part04)

Follow the steps in the [pre-release checklist]() and apply the post validation tests to this post.

## prepare to release V0.04.000 of the site

Follow the steps in the [pre-release checklist]() and apply the site validation tests to the feature branch.

## Release V0.04.000 of the site along with any mew published posts

Follow the steps in the [Bills Blog Release Process]() post.

