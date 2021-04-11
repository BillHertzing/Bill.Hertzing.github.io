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
- [Markdown License badges](lukas-h/license-badges.md)
 

*Note* If you want to use a badge that refers to any of the repo's Community Health files (like `CONTRIBUTING` or `CODE OF CONDUCT` AND if you want to use ***default*** Community Health files, then specify the repo *GitHubUserName*/.github in the badge's repo field.

1. Create the file `ReadMe.md` in the root of the repo.
1. Edit the file, and add whatever content you think appropriate
1. Commit and push to the GitHub repo.
1. Validate your ReadMe file now displays on the GitHub repo's landing page.

## Add `ChangeLog.md`

Having a ChangeLog for your blog site will help user's understand changes you  have applied

[keep a changelog](https://keepachangelog.com/en/1.0.0/)

If you want to automate the ChangeLog to a degree, it is important that the commits in the repo have meaningful commit messages that are machine readable. Here are some examples of commit messages and tools that can read them.
[Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) also has a large bibliography of tooling around Conventional Commits
[Universal Changelog Generator action](https://github.com/marketplace/actions/universal-changelog-generator).

***Of you want to automate the generation of the ChangeLog, you need to write your commits in a standard format***

I hve a feature identified in the Far Future Milestone for automation in this area, so I'll start using commits in the style specified by [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/). According to that document, commits I've already made will just be ignored by the automated tooling, and the ChangeLog can be manually edited as I have done for the initial ChangeLog I create below.

1. Create the file `ChangeLog.md` in the root of the repo.
1. Edit the file, and add content appropriate for the site's "Birthday", and Release V1.01.1
1. Commit and push to the GitHub repo.
1. Validate your Changelog file now displays on the GitHub repo's landing page.

## Add commit message template

To make it easier to create commit messages that follow a standard template, add a git commit message template to the repository and configure git to use that file. The standardized commit message template I chose for my initial version of the template can be found at [Keeping Git Commit Messages Consistent with a Custom Template](https://dev.to/timmybytes/keeping-git-commit-messages-consistent-with-a-custom-template-1jkm).

1. Create the subdirectory `GitTemplates` in the root of the repo.
1. Create the file `git.commit.template.txt` in the subdirectory `GitTemplates`.
1. Add text similar to the following to the template `.txt` file, and save it.

  ```Text
    ToDo: Add final text just before release
  ```

1. Run `git config --global commit.template GitTemplates/git.commit.template.txt` to add the template to your global git config.
1. Run `git config --global core.editor "code --wait"` to add VSC as git's editor of choice. See also [MarredCheese's answer to StackOverflow question ](https://stackoverflow.com/questions/30149132/multiline-git-commit-message-in-vscode/54139152#54139152).
1. Run `git commit -a`
1. Validate that VSC is the editor for the commit message which comes up pre-populated with the template's text.
1. Click on the SCM icon in the sidebar. What was the single line commit message text box at the top has expanded to contain the non-comment template lines, and blank lines wherever there was a comment. Hmmm... Wonder how we can have only non-comment lines from the template in the SCM editor's commit text box, yet have the fulltemplate text at just a keystroke away if needed forr reference  ToDo: Figure that out.

When doing design work on a feature, it save some time if you edit the template to add a reference to the feature specification or the release milestone that calls out the feature under development. Likewise if you are working on a post, and doing the edit/build/view dance, editing the template may save you some time and keystrokes.

