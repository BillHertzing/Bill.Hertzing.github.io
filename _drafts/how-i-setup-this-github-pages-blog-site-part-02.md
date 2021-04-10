---
Title: How I setup this GitHub Pages Blog, Part 2
tags: Jekyll "GitHubPages"
layout: post
description: Second steps in setting up a Jekyll generated blogging site hosted on GitHub Pages which uses any plugin, theme, Jekyll version or Ruby version.
---

Welcome to the second part of this series detailing how I setup this blog site hosted on GitHub Pages. If you have not yet seen the first post in the series [How I setup this GitHub Pages Blog](TBD), you should probably give it a quick review, to become familiar with how it all started.

The next steps will be to implement the features specified in [Milestone 0.02.0](https://github.com/BillHertzing/BillHertzing.github.io/milestone/2).  I like to plan my development efforts using GitHub Milestones. They are quick and easy to create and maintain, especially for tiny sites like mine that have no collaborators. Of course I don't ***have*** to create Milestones, but I've found that there is always "feature creep" in releases if I don't take the time to write down what is going into the next release, and what's on tap for some future release. This helps me keep to the release cadence I want, and ensures these posts corresponding to each release don't get too big!

This release is mostly adding files that are common to a good reposity, and then adding the ability to add comments to a post.

Lets move on!

## Create `_drafts` folder

Being able to work on a draft of a post, and not have that draft appear on the production site, is important during development. Jekyll has built in support for drafts, using a `_drafts` folder. Simply create the folder `_drafts` under the root of your repository.

## Create a draft post

1. Create the file `how-i-setup-this-github-pages-blog-site-part-02.md` under the new `_drafts` subdirectory. Do not add the *YYYY-MM-DD* prefix to this file.
1. Add the following Front Matter text to the file. Modify it as appropriate for your site. *Note* There is no `date:` key in a draft post. Jekyll will insert that key when you promote the post out of `_drafts` and publish it for the first time.

    ```markdown
    ---
    Title: How I setup this GitHub Pages Blog, Part 2
    tags: Jekyll "GitHubPages"
    layout: post
    description: Second steps in setting up a Jekyll generated blogging site hosted on GitHub Pages which uses any plugin, theme, Jekyll version or Ruby version.
    ---

    Add text you want to see in your second post
    ```

1. Save and commit.
1. Run `bundle exec jekyll serve --drafts`. Jekyll will build the drafts with the current date so they will be easy to find at the top of your (chronologically sorted) post listings.
1. Validate your new post exists locally.

## Community Health files

GitHub encourages authors to ensure their repositories are setup for building communities for healthy and effective collaboration. Details are at [Building communities](https://docs.github.com/en/communities). The first guideline is [Setting up your project for healthy contributions](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions). Among other things, it recommends [Adding a code of conduct to your project](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/adding-a-code-of-conduct-to-your-project) and [Setting guidelines for repository contributors](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/setting-guidelines-for-repository-contributors). But what if you have more than one repository? Do you have to duplicate these files in every one? No, you can setup defaults for these files, and have every repository inherit from your default. Details are in [Creating a default community health file](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file).

### Create `.github` repo

I'm not going to repeat here the instructions you can find on the GitHub doc above. But at this point in the development of this site, I created the new `.github` public repository under my username, and added the `CODE_OF_CONDUCT.md` and `CONTRIBUTING.md` files to the `.github` repo. ToDo: insert jpg

*Note* I changed my GitHub theme to Dark, so the screen shots of GitHub are going to look different from Part 1 of this series!

Now go look at your site's repository in GitHub, drill down into `Insights`, and then the `Community` tab, and you can see that both of these files are now present in this repository's Community Profile! ToDo: insert jpg

### How to link to these default files

Lets add links to both of these files, both here, and in the `_includes/footer.html` template. From the `Insights->Community` page, click the `Code of conduct` link, the in the browser's address bar, copy the URL showing. Mine looks like this: `https://github.com/BillHertzing/.github/blob/main/CODE_OF_CONDUCT.md`. Create a markdown link to this as follows:

<notextile>[Code of Conduct](https://github.com/BillHertzing/.github/blob/main/CODE_OF_CONDUCT.md)</notextile> produces [Code of Conduct](https://github.com/BillHertzing/.github/blob/main/CODE_OF_CONDUCT.md)

Repeat for `CONTRIBUTING.md`.

<notextile>[CONTRIBUTING](https://github.com/BillHertzing/.github/blob/main/CONTRIBUTING.md)</notextile> produces
[CONTRIBUTING](https://github.com/BillHertzing/.github/blob/main/CONTRIBUTING.md)

## Add `ReadMe.md`

The `ReadMe.md` file at the root of a repo will get displayed to visitors on the repo's landing page. Here are some posts with great ideas

- [A Beginners Guide to writing a Kickass README](https://meakaakka.medium.com/a-beginners-guide-to-writing-a-kickass-readme-7ac01da88ab3#:~:text=A%20great%20README%20file%20helps,basic%20introduction%20to%20the%20software.)
- [A template to make good README.md · GitHub](https://gist.github.com/PurpleBooth/109311bb0361f32d87a2)
- [A curated list of awesome READMEs](https://github.com/matiassingers/awesome-readme)
- [awesome-github-badges](chetanraj/awesome-github-badges) - add some badges to the readme
- [badges](https://github.com/aleen42/badges) - To make badges more standard and acceptable.

1. Create the file `ReadMe.md` in the root of the repo.
1. Edit the file, and add whatever content you think appropriate
1. Commit and push to the GitHub repo.
1. Validate your ReadMe file now displays on the GitHub repo's landing page.
