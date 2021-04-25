---
title: ChangeLog
permalink: /ChangeLog/
description: Information about me personally and about this blog site
---

## 2021-04-25 Release V0.03.000

Published the post `personal/2021-04-25-Eulogy for molly` post
Published the post `technical/2021-04-25-how-i-setup-this-github-pages-blog-site-part-03.md`
Installed the following Gems locally:
  
    - `minimal-mistake-jekyll` theme GEM 
    - `jekyll-paginate`
    - `jekyll-sitemap`
    - `jekyll-gist`

Replaced `_config.yml` with `_config.yml` from the minimal-mistakes (MM) theme

    - Uncommented minimal-mistakes as a local theme
    - Added Author Bio and location
    - Turned on GitHub social link to profile, working
    - Turned on twitter social link to profile, working
    - Turned on GraphQL SEO attributes
    - Enabled comments on posts
      - Use Disqus as the comment provider
    - Enabled default front matter for all posts
      - Enabled Table of Contents and made it sticky to top of post
      - Enabled comments
    - Enabled `timezone: America\Denver`

Created local _includes/footer.html from MM theme's version to override the default footer
    - Modified copyright
    - Added link to default Community Health File `License`
    - Added link to default Community Health File `Contributing`
    - Added link to default Community Health File `Code of Conduct`
    - Added the site's Release Version

Created local `_includes/gallery` from MM theme's version to override the gallery component
    - Added `<span>{{ "{{" }} img.title }}</span>` below the `</img>` tag to provide a caption. *Note: will be upgraded to be responsive in a later revision*

Created local `_includes/head/custom.html` from MM theme's version to include custom favicon HTML information
    - Added the HTML necessary to deliver the correct favicon file to multiple types of browsers

Generated a set of favicon files suitable for multiple types of browsers, placed them into root of repo

Removed `layout: post` from Front Matter on all published posts
Removed `layout: page` from Front Matter on all pages
Added `layout: home` to Front Matter of `index.md` in root of repo (this is the site's landing page)

Added words to spellcheck dictionary
Fixed typos and edited for clarity the previous posts and pages
Incorporated bugfixes for Issues #4, #5, #6, #7, #8, #9, #10, #11, #12

Updated the `git.commit.template` from 0.02.000 to 0.03.00
Added a new branch SprintForRelease0.03.000 branched from the releases/0.02.000 tag

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

- Created the repository https://github.com/BillHertzing/BillHertzing.github.io
