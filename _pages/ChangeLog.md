---
title: ChangeLog
permalink: /ChangeLog/
description: Information about me personally and about this blog site
layout: single
---

## 2021-05-22 Release V0.04.000

- Created branch `SprintForRelease0.04.000`
- Updated commit template to 0.04.000.
- Created post "how-i-setup-this-github-pages-blog-site-part-04.md".
- Added plugin [jekyll-compose](https://github.com/jekyll/jekyll-compose)
- Added plugin [jekyll-minifier](https://github.com/digitalsparky/jekyll-minifier)
- Added plugin [jekyll-archives](https://jekyll.github.io/jekyll-archives/)
- Added plugin [jekyll-relative-links](https://github.com/benbalter/jekyll-relative-links)
  - Updated all posts and pages to use relative links
- Created a subdirectory `_pages` at the repo root
- Moved all .md files to the subdirectory `_pages`
- Created a new landing page layout for the site using `splash` layout
  - Overrode MM's `splash` layout with a local `_layouts/splash.html` file
  - Added blocks of Liquid from `single.html` to ensure that content will stay within the center column
  - Added author_profile and custom sidebar nav elements to the local `splash` layout
- Modified `_pages/index.md`, renamed it to `_pages/Home.md`
  - Changed layout to `layout: splash`
  - Added `permalink: /`
  - Added content for the site's splash landing page
- Added carousel component and included it on Home page
- Built a Gem `flexible_include` that can read the contents of a file on the local filesystem
- Created three .md files in `_pages` for the Community Health files
  - All use `layout: single`
  - Created `_pages/Code-of-Conduct.md`, using `flexible_include`to read the file by the same name in ../.github repository
  - Created `_pages/Contributing`.md, using `flexible_include`to read the file by the same name in ../.github repository
  - Created `_pages/License.md`, using `flexible_include`to read the file by the same name in ../.github repository
- Created three pages to be used as landing pages for post archives
  - Created `category-archive.md` for listing posts by category.
  - Created `tags-archive.md` for listing posts by tags.
  - Created `year_archive.md` for listing posts by date.
- Added `_data/navigation.yml` for masthead navigation, with the following menu items.
  - About
  - Posts by Date
  - Posts by Category
  - Posts by Tags
  - Subscribe
  - ChangeLog
  - Contributing
  - Code of Conduct
- Added author profile and sidebar navigation as default for all pages in `_config.yml`
- Added custom sidebar navigation
  - Added docs sidebar navigation information to `_data/navigation.yml` .
  - Used titles that reflect the documentation that will be available in my other repositories
- Made the Release Version number in the footer a link to ChangeLog permalink
  - Changed `_includes/footer.html`
    - Changed references to `Contributing` and `Code-of-Conduct` from the .github repo to local .md pages.
    - Added the ChangeLog.md link
- Moved all Published posts to one of the subdirectories of `_posts` : technical, personal or political
- Changed default Front Matter in `_config.yml` for posts so that Permalinks are `/:slugified_categories/:year/:name`
- Updated all cross-document and internal links to posts and pages to use relative_url
- Cleaned up layouts and permalinks for all published and draft posts
- Slugified all page and post names
- Modified `gallery` component to open images in a new tab
- Added post `technical/2021-05-22-bills-blog-release-process.md`
- Added post `technical/2021-05-22-bills-blog-pre-release-checklist.md`
- Added page `subscribe-to-bills-blog.md`
- Added post `personal/2021-05-07-hiking-emigration-canyon-miners-trail.md`
- Added post `personal/2021-05-17-scout-cave-trail-st-george-ut.md`
- Added post `personal/2021-05-20-petrified-sand-dunes-loop-trail-st-george-ut.md`
- Added the file `ataplogo.bmp` to the repo root
- Added Authorized Digital Sellers file from Disqus, `ads.txt`
- Added `_config.Development.yml` to allow for development-specific settings
  - set site.URL to "localhost" for development builds
- Added rule to use custom merge driver for `_site` subdirectory and its children
- Added custom merge driver to the global `~/.gitconfig` file
- ***Disabled jekyll-minifier***

## 2021-05-02 Release V0.03.001

- Created draft post `2021-05-01-Word-Template-for-letter-to-CPA-HOA-regarding-sale-of-golf-course` .
- Created two Word documents as referenced in the post body.
- Put the Word documents into Dropbox, created shared links to the documents, referenced them in the post body.
- Moved post from `_drafts` to `political`, added date prefix to post's filename.

See Issue #14

## 2021-04-25 Release V0.03.000

- Published the post `personal/2021-04-25-Eulogy for molly`
- Published the post `technical/2021-04-25-how-i-setup-this-github-pages-blog-site-part-03.md`
- Installed the following Gems locally:

  ```yml
  minimal-mistake-jekyll theme GEM
  jekyll-paginate
  jekyll-sitemap
  jekyll-gist
  ```

- Replaced `_config.yml` with `_config.yml` from the minimal-mistakes (MM) theme.

  ```yml
  - Uncommented minimal-mistakes as a local theme
  - Added Author Bio and location..
  - Turned on GitHub social link to profile.
  - Turned on twitter social link to profile.
  - Turned on GraphQL SEO attributes.
  - Enabled comments on posts.
    - Use Disqus as the comment provider.
  - Enabled default front matter for all posts.
    - Enabled Table of Contents and made it sticky to top of post.
    - Enabled comments.
  - Enabled `timezone: America\Denver` .
  ```

- Created local `_includes/footer.html` from MM theme's version to override the default footer.

  ```yml
  - Modified copyright.
  - Added link to default Community Health File `License` .
  - Added link to default Community Health File `Contributing` .
  - Added link to default Community Health File `Code of Conduct` .
  - Added the site's Release Version.
  ```

- Created local `_includes/gallery` from MM theme's version to override the gallery component.

  ```yml
  - Added `<span>{{ "{{" }} img.title }}</span>` below the `</img>` tag to provide a caption. *Note: will be upgraded to be responsive in a later revision*
  ```

- Implemented Favicon

  ```yml
  - Generated a set of favicon files suitable for multiple types of browsers, placed them into root of the repo.
  - Created local `_includes/head/custom.html` from MM theme's version to include custom favicon HTML information.
    - Added the HTML necessary to deliver the correct favicon file to multiple types of browsers.
  ```

- Modified the `pages` and `posts` to change from `minima` layouts to MM layouts.

  ```yml
  - Removed `layout: post` from Front Matter on all published posts.
  - Removed `layout: page` from Front Matter on all pages.
  - Added `layout: home` to Front Matter of `index.md` in root of repo (this is the site's landing page)
  ```

- Added words to spellcheck dictionary
- Fixed typos and edited for clarity the previous posts and pages
- Incorporated bugfixes for Issues #4, #5, #6, #7, #8, #9, #10, #11, #12

- Updated the `git.commit.template` from 0.02.000 to 0.03.00
- Added a new branch SprintForRelease0.03.000 branched from the releases/0.02.000 tag

## 2021-04-15 Release V0.02.000

- add subdirectories for _drafts, political/_posts, personal/_posts
- Add a ChangeLog.md , create content for V0.1.0, V0.2.0
- Add Commit Template
- Add ReadMe.md
- Add Code of Conduct to Community Health Files repository
- Add Community Guidelines  to Community Health Files repository
- Add Issue Template (for Bug and for Feature Request) to Community Health Files repository
- add jekyll-timeago plugin
- add jekyll-include-cache plugin
- update footer with last Release tag version number and release (commit) date
- add published post "How I setup this GitHub Pages Blog site, Part 02" under technical subdirectory
- add published post "Case for a non-anonymous Internet, Part 01" under political subdirectory
- add published post "Welcome to the Personal section of my site" under personal subdirectory

## 2021-04-07 Release V0.01.000

Initial creation of site

- Jekyll tooling including Ruby and MSYS2 on Windows 10
- Created Milestones for Releases V0.01.0 - V0.04.0
- Created the following files:
  - .gitignore
  - index.md
  - about.md
  - LICENSE.html
  - _config.yml
    - theme:minima
  - .github/workflows/deploy-site-to-github.yml
  - _includes/footer.html
  - _posts/2021-04-06-Welcome-To-Bills-Blog.md
  - technical/_posts/2021-04-06-how-i-setup-this-github-pages-blog-site-part-01
  
## 2021-04-06 Birthday

Initial creation of repository

- Created the repository [BillHertzing.github.io](https://github.com/BillHertzing/BillHertzing.github.io)
