---
Title: How I setup this GitHub Pages Blog, Part 4
tags: Jekyll GitHubPages
description: Fourth group of steps in setting up a Jekyll generated blogging site hosted on GitHub Pages which uses any plugin, theme, Jekyll version or Ruby version.
category: technical
---

Welcome to the fourth part of this series detailing how I setup this blog site hosted on GitHub Pages. If you have not yet seen the first posts in the series [How I setup this GitHub Pages Blog Site Part 01]({% link technical/_posts/2021-04-06-how-i-setup-this-github-pages-blog-site-part-01.md %}), [How I setup this GitHub Pages Blog Site Part 02]({% link technical/_posts/2021-04-17-how-i-setup-this-github-pages-blog-site-part-02.md %}), and [How I setup this GitHub Pages Blog Site Part 03]({% link technical/_posts/2021-04-17-how-i-setup-this-github-pages-blog-site-part-03.md %}) you should probably give them a quick review, to become familiar with how the site has been built up to this point.

The next steps will be to implement the features specified in [Milestone 0.04.0](https://github.com/BillHertzing/BillHertzing.github.io/milestone/4). I've already created Milestones for Release V0.05, [Milestone 0.05.0](https://github.com/BillHertzing/BillHertzing.github.io/milestone/5) as well and updated the Milestone *Release Far Future* to reflect whats planned for later. Release V0.05 calls for creation of a  Github project for tracking future features,So at that point hopefully, there will be a single point for tracking and reporting on planned and requested features.

## add a new branch `SprintForRelease0.04.000`

- Run `git branch create SprintForRelease0.04.000`

## Add jekyll-compose

jekyll-compose adds commands that help streamline the creation and publishing of posts. Installation instructions and details can be found in [jekyll-compose](https://github.com/jekyll/jekyll-compose). What follows are th steps I took and choices I made for this site.

1. Edit the  Gemfile in the root of the repo.
1. Add `gem 'jekyll-compose', group: [:jekyll_plugins]` just above the `plugins:` key.
1. Run `bundle`

Refer to detailed instructions in [jekyll-compose](https://github.com/jekyll/jekyll-compose) for using the new commands. This post was drafted and published using the commands added by this tool, and it made the process much much easier. I created the draft of this post using the command `bundle exec jekyll draft "how-i-setup-this-github-pages-blog-site-part-04"`, which placed a file containing just Front Matter in the `_drafts` directory.

## Update the commit template

- Edit `GitTemplates/git.commit.template.txt` and change `03` to `04`
- save the file

## First commit on the sprint branch

Commit the changes and use VSC to synchronize changes with the remote, then inspect the Github repository to ensure the branch and first commit exist on the repo. I like using Git Lens along with Git Graph. ToDo: insert jpg You can see the site development history clearly. 

To show what a feature develeopment branch looks like withg more than one commmit, I'll make a small one now.

Afterwards, this is what it looks like ToDo: insert jpg.
