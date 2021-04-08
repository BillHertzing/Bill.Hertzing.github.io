---
Title: How I setup this GitHub Pages Blog
date:   2021-04-06 12:31:43 -0600
tags: Jekyll "GitHubPages"
category: Technical
layout: post
---

I have been trying for a few years to setup a web site I can use for blogging. But since there are a lot of neat features I'd like to include, every prior attempt has foundered on getting it all to hang together, along with the problems of version control for everything. And of course cost is always a consideration. Now, I'm giving it another try, this time using the GitHub Pages to host my site, and building it with Jekyll, the static site generator. Here are the steps I've taken to implement the features I'd like to have.

If you would like to see a list of the articles online that have helped me create this site, please see the  <a href="#Attributions">Attributions</a> section below. (ToDo: coming in release V0.02.0 and explained in Part 02 of this post)

## Prerequisites

1. A Windows 10 PC (Laptop or desktop)
1. a GitHub account. make a note of your username, and throughout this document, replace *GitHubUserName* with YOUR GitHub username
1. Powershell installed and updated on Windows 10
1. Git for Windows (or alternative Git client) installed on Windows 10
1. Visual Studio Code (VSC) (or similar editor) installed on Windows 10
1. (VSC) GitHub extension module

## Install Ruby and Jekyll on your Windows PC

*Note* if you need to clean up a botched prior attempt (me!), and you would like to remove all gems you may have installed, run this command in a Powershell terminal window `gem uninstall -aIx`)

ToDo: Investigate using [chocolatey](https://chocolatey.org/) to install both Ruby and MSYSY2, as this will greatly simply keeping the toolchain up-to-date.

1. Install [RubyInstaller for Windows](https://rubyinstaller.org/). Select a recent Ruby+DevKit version (I picked `RubyInstaller 3.0.0-1 released`) and use the default options in the installation wizard. On the last step, you’ll want to keep the option “Run ‘ridk install’ to setup MSYS2 and development toolchain.” checked. ToDo: embed .png file of screenshots for these two steps
1. Close the Powershell prompt window, and open a new one (this one will have the updated environment PATH information)
1. At the Powershell prompt, Run `gem install jekyll bundle`. This installed Jekyll V4.2.0 (on 2021-04-05), and a total of 28 gems. ToDo: embed screenshot
1. Run `jekyll -v` and confirm Jekyll returns its current version number. <img src="https://www.dropbox.com/s/mvcm5kio1b3ocim/001%20Validate%20Jekyll%20Version.png?raw=1" alt="Jekyll version 4.2.0"  style="vertical-align:bottom"> 
ToDo: Add responsive sizes attribute and create multiple sizes of the image.

## Create a new git repository

1. Open a Powershell terminal, navigate to the location (directory) you want to be the parent of your repository. My parent directory is `C:\Dropbox\whertzing\GitHub\`.
1. Create a subdirectory `*GitHubUserName*.github.io`, and `cd` into it.
1. Run `git init`. <<img src="https://www.dropbox.com/s/mvcm5kio1b3ocim/001%20Validate%20Jekyll%20Version.png?raw=1" alt="git init results"  style="vertical-align:bottom">

## Create minimal Jekyll-compliant site source code

1. Run `jekyll new PATH` (Use the FULL Path to the repository on your windows PC i.e. `C:\Dropbox\whertzing\GitHub\BillHertzing.github.io`) which will create the bare bones of the new Jekyll-compliant site source code. ToDo: add jpg
1. (optional) I prefer to use `.md` instead of `.markdown` for the suffix of Markdown files, so I now run the two commands `mv about.markdown about.md` and `mv index.markdown index.md`

 I may want to eventually develop a Jekyll Plugin plugin and I know I'll want to eventually publish my own Jekyll theme, so might as well start with with an approach that will support that. So at this point, I'll diverge from the many other posts about setting up Jekyll. Because I want to use the latest Ruby and MSYS2 components, non-approved Jekyll Plugins and a non-approved Jekyll theme, I will keep the site source code under the  `main` branch of this repository, map my local `.\_site` to the `gh_pages` branch of this repository, build the site locally on my Windows PC, and push `.\_site` to the `gh_pages` branch on GitHub.

1. edit the `_config.yml` file, and remove a lot of the boiler plate. At this point, mine looks like this:

```yml
# Jekyll initial configuration file for BillHertzing.github.io V0.01.0

title: Bill's Blog
description: >- # this means to ignore newlines until the next key, which is "baseurl:"
  Technical articles for my code repositories. Position papers on political issues. Cute pictures of the kids. I've got it all!
baseurl: "" # the subpath of your site, e.g. /blog
url: "https://BillHertzing.github.io" # This is a User GitHub Pages site, not a Project GitHub Pages  site
twitter_username: BillHertzing
github_username:  BillHertzing

# Build settings
markdown: kramdown
permalink: pretty
theme: minima
```

## Download the minima theme

Any Jekyll theme you want to use must first be downloaded to your Windows PC so run `gem install jekyll-theme-minima`.. Today (2021-04-06) it loaded jekyll-theme-minima-0.1.1.gem and 18 other gems (dependencies) as well.

## Verify the local site will build and serve locally on your Windows PC

It is a good idea to be able to see what your site will look like, before committing the changes to GitHub. By default, `jekyll build` will read the site's source from the current directory, and write it to a subdirectory `_site`. and `jekyll serve` will start a local web server and serve `_site` to `http://localhost:4000`. `jekyll serve` will also build the site if any source file has been changed.

1. Open a Powershell terminal and navigate to your repository.
1. Run `jekyll serve`

### Fixing issues

Did you really think that everything would 'just work'?  Hahaha! When I try this today, I get an error message "Could not find gem tzinfo-data". Typically, new versions of one tool might break a dependency used somewhere else. In this particular case, the latest version of Ruby (3.0.0 today) no longer includes that gem by default. So, I needed to run `gem install tzinfo-data`. Then when I tried `jekyll serve`, I got an error message ""Could not find gem wdm". So I ran `gem install wdm`. And then again for `webrick`, which required `bundle add webrick`. Depending on how much things have changed between the time I write this and the time you try to follow it, there may be other dependency changes, so just keep on trying to build and fixing the issues, until `jekyll serve` completes and starts serving up pages.
I also ran into problems with the Bundler version, getting the error `cannot load such file -- C:/Ruby30-x64/lib/ruby/gems/3.0.0/gems/bundler-2.2.3/libexec/bundle (LoadError)`. After updating the Bundler with `gem install bundler` I needed to edit the `Gemfile.lock` and change the `bundled with` line at the bottom to match the version just installed/updated.

I also changed the command I was using to build and serve to `bundle exec jekyll serve`

Finally, when you've wrung out the bugs, Jekyll will serve the site locally. Use the browser of your choice and navigate to http://localhost:4000. With the minima theme it should look like this:
ToDo: Insert .jpg

## Replace the original `welcome-to-jekyll.markdown` page

1. In the `_posts` subdirectory, add a new file with the format `*YYYY-MM-dd-welcome-to-*whatever*`. use your current year-month-day numerals, and change *whatever* to whatever you want to call your first welcome post.  I used `2021-04-06-Welcome-To-Bills-Blog.md`
1. look at the original file in the _posts directory, which was created by the initial `jekyll new PATH` command earlier, and copy the Front Matter to your new post, update the Front Matter to change the title, update the date to match that of your filename and optionally remove the categories.
1. In the new post, enter your initial draft of whatever you want to see on your first post, and save the file.
1. Delete the original file in the _posts directory.

## Push the source code to GitHub

Now that we have things working locally, lets get our site stored up on GitHub. GitHub offers detailed instruction on how to do this here [Adding an existing project to GitHub using the command line](https://docs.github.com/en/github/importing-your-projects-to-github/adding-an-existing-project-to-github-using-the-command-line). What follows here are the summarized steps I took.

1. Open a Powershell terminal and navigate to your repository.
1. Run `git add .`  This will add all the local files to your local repository and stage them for a commit
1. Run `git commit -m "First commit"`  This Commits the tracked changes and prepares them to be pushed to a remote repository.

### Create a new repository on GitHub

Detailed instructions here [Create a new repository on GitHub](https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/creating-a-new-repository) To avoid errors, do not initialize the new repository with README, license, or gitignore files. You can add these files after your project has been pushed to GitHub.

1. Login to your GitHub account  ToDo: Add .jpg
1. Click the New Repository button.
1. Enter a name and description, select Public, and don't check anything under the `initialize this repository with:` section. ToDo: Add .jpg
1. Click the big `Create repository` button at the bottom.
1. ToDo: insert jpg of the result, and highlight the link to copy
1. Copy the HTTPS link showing at the top of the page.

### Push the local repository to the remote repository

1. Open a Powershell terminal and navigate to your repository. Or just reuse an already open Powershell terminal.
1. Details are available at [Managing remote repositories](https://docs.github.com/en/github/getting-started-with-github/managing-remote-repositories)
1. Run `git remote add origin  <REMOTE_URL>`  Of course, replace <REMOTE_URL> with the URL you just copied from GitHub. Mine looked like this: `git remote add origin https://github.com/BillHertzing/Bill.Hertzing.github.io.git`
1. Run `git remote -v` to confirm that the origin is indeed set to the URL for the remote repository you just created on GitHub.
1. Run `git branch -M main` and then `git push -u origin main`  Pushes the changes in your local repository up to the remote repository
1. Verify the source code for your site is now in GitHub. ToDo: add jpg

## Setup Visual Studio Code (VSC)

1. Open the Visual Studio Code application.
1. Select `Open folder` and navigate to the new repository you just created. To Do: insert jpg

## Confirm that VSC can push changes to GitHub

1. Open the `about.md` file for editing, select everything after the front matter (line 7 and onward as of today), and delete it. then add the word 'test' on line 7.
1. Save the file. Note that the Source Control button on the link now has a badge with the number (1) and the `about.md` file indicates M for Modified. ToDo: insert jpg
1. Click the VSC Source Control button inside the left toolbar.
1. In the message box, enter `remove unneeded parts of about.md`, then click the `check` above the message box (alt text is `Commit`)
1. Note that the bottom status bar now shows there is one local commit that has not been pushed to the remote. ToDo: insert jpg
1. Click on that area of the status bar, and the change should be pushed to GitHub
1. On GitHub, open the about.md file, and confirm that the change has been pushed to the GitHub remote repository.

ToDo: Interesting, while working on this, I learned if VSC is not logged in to anywhere, and you chose to login to GitHub, there is an authentication interaction that stores some information into VSC somewhere. I should investigate and write it up...  It opened GitHub in Chrome (my default browser), and I entered my password to GitHub. There was a form asking if I wanted to authorize, said yes, then a redirect on github, and a dialog box saying that there was a uri that wanted to open VSC. I allowed that dialog to "open the VSC app. Since it was already open, it just switched me back to the VSC instance. Nothing added to the repository where I was working, so either somewhere in VSC or somewhere in Windows, there is now an association "vscode://vscode.github-authentication/did-authenticate?windowid=1&code=a_very_long_alphanumeric_string"

## Enable GitHub pages on the GitHub repository

1. Navigate to the `Code` view of the repository
1. Create the branch `gh-pages`.
1. Open Setting on the GitHub repository. ToDo: insert jpg
1. Scroll down to the GitHub Pages section.
1. Type `gh-pages` for the branch name. ToDo: insert jpg

## Add a workflow file `deploy-site-to-github-pages.yml`

This workflow and the actions it contains are the key to an easy blogging workflow. A great piece of OSS for GitHub Actions, combined with a workflow trigger that detects a release tag, make it all work.

See the details of the Action here: [Deploy to GitHub Pages](https://github.com/marketplace/actions/deploy-to-github-pages) by James Ives and other contributors, also [github-pages-deploy-action](https://github.com/JamesIves/github-pages-deploy-action).
See the details of the trigger here: [Git Tag Based Released Process Using GitHub Actions](https://www.codingwithcalvin.net/git-tag-based-released-process-using-github-actions/) by Calvin A. Allen.

1. Create the directory and subdirectory `.github\workflows` in the repository.
1. Create the file `deploy-site-to-github-pages.yml` in the `.github\workflows` subdirectory

ToDo: figure out how, at site generation time (`jekyll build`) to read the contents of the actual file and update the text below with the actual contents, and run those contesnts through a regexp replacement to escape the {{ "%{" }} and {{ "{{" }} so the publish process doesn't do any logic.
ToDo: decide on a strategy for updating a historical post if the file changes. Perhaps a revision tag for posts?
ToDo: Figure out how notify subscribers to the RSS feed if a existing post gets a new revision.
ToDo: Figure out how to e-mail an administrator if a code change triggers the need to create a post revision
ToDo: When a new site gets published, is that a good time to note any post revisions into the ChangeLog?

Put the following yml code into the file, and then save it.

```yml
name: deploy generated site to GitHub Pages on gh-branch 

on:
  # Triggers the workflow on push requests to the main branch if the commit includes a tag that matches the Semantic Version release tag
  push:
    # tags: [ releases/\d+\.\d+\.\d+ ] # yep, the first element of the tags array is a regular expression. Modify the RegExp if you use a different format for your release tags
    branches: [ main ]
  # This line allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

jobs:
  # This workflow contains a single job called "deploy-site-to-github-pages"
  deploy-site-to-github-pages:
     # The type of runner that the job will run on
    runs-on: ubuntu-latest  # ToDo: investigate if a specific ubuntu is better

     # Steps represent a sequence of tasks that will be executed as part of the job
    steps:
      # Checks-out your repository under $GITHUB_WORKSPACE, so your job can access it
    - name: Checkout code
      uses: actions/checkout@v2
      
    - name: Deploy 🚀
      uses: JamesIves/github-pages-deploy-action@4.1.1
      with:
        branch: gh-pages # The branch the action should deploy to.
        folder: ./_site # The folder the action should deploy.
```

Save the new file and commit the changes.

## Create an Environment for the deployment action

1. On GitHub, in the repository, under `Settings`, open the `Environment` tab, and click `Create Environment`. ToDo: insert jpg
1. Name the Environment `deploy-site-to-github-pages`, and click `Configure Environment`. ToDo: insert jpg
1. Click `x` on the following page to acknowledge the environment was created, and go back to the `Settings->Environment` page. ToDo: insert jpg
1. Click on the name of the environment just created.
1. At the bottom of the page, click the `Add Secret` button. ToDo: insert jpg
1. Add a Secret with the name `ACTIONS_STEP_DEBUG` and value `true`. You can remove this Secret after the action has been debugged. There is an additional Secret `ACTIONS_RUNNER_DEBUG` which if set to `true` will provide more details in the logs. I like to set this, as well. ToDo: insert jpg

The final Environment should look like this: ToDo: insert jpg

## Remove `_site` from the `.gitignore` file

1. Edit the .gitignore file in the root of the repository, and remove the `_site` line. Save.
1. Run `bundle exec jekyll serve` to validate the site builds and displays as expected locally on your Windows PC.
1. Note in the VSC sidebar that the VSC Source Control menu-item icon has a number, and the Source Control Changes editor window now shows multiple new files under `_sites` to be committed.
1. Commit all the changes. I used the message "Start tracking `_site`"  *NOTE* I made the changes to the original post, as specified above at (ToDo: insert link to previous place ) at this point in the development, so the jpg file also shows me removing the original post file and adding my own first post file in `_posts` ToDo: insert jpg
1. Sync with the remote GitHub repository.
1. Validate the `_site` and its files are now present on the GitHub repository. ToDo: insert jpg

## Review the workflow run

1. Navigate to the `Actions` tab in your GitHub repository. ToDo: insert jpg
1. Drill down into the latest workflow run. ToDo: insert jpg
1. Drill down into the job log. ToDo: insert jpg
1. Expand the `Deploy` step. ToDo: insert jpg

## Troubleshooting the workflow run

ToDo: see if there are any problem with the deploy action, another GitHub action did have problems here

## Invoke `deploy-site-to-github-pages` manually

ToDo:

## Add the MIT LICENSE file

This site uses the MIT licenses. Of course, feel free to chose a different license if such is more appropriate for your site. You can find the text of many popular licenses at the Open Source Initiative page [Licenses & Standards](https://opensource.org/licenses)

1. Under the root of the repository, add a new file `LICENSE`, and copy the appropriate text from one of the OSI-approved licenses into the file, and close it.

## Modify the footer template

It is a good idea to put a link to the license somewhere on each page, and the page footer is an unobtrusive place for this. I also like to put the copyright notice there. I followed the detailed instructions here [GitHub Pages Jekyll Minima Customize Footer](https://cyberloginit.com/2018/05/05/github-pages-jekyll-minima-customize-footer.html#:~:text=To%20customize%20the%20footer%2C%20you,Then%20customize%20footer.) by Cyber Log in IT.

1. Add a directory `_includes` to the root of the repository.
1. Copy the `footer.html` from the [Minima GitHub repository](https://github.com/jekyll/minima) into the `_includes` subdirectory.
1. Customize `footer.html` to your own needs.

The footer.html file from the minima theme looks like this:

```html
<footer class="site-footer h-card">
  <data class="u-url" href="{{ "/" | relative_url }}"></data>

  <div class="wrapper">

    <div class="footer-col-wrapper">
      <div class="footer-col">
        <p class="feed-subscribe">
          <a href="{{ "{{" }} 'feed.xml' | relative_url }}">
            <svg class="svg-icon orange">
              <use xlink:href="{{ "{{" }} 'assets/minima-social-icons.svg#rss' | relative_url }}"></use>
            </svg><span>Subscribe</span>
          </a>
        </p>
      {{ "{%" }}- if site.author %}
        <ul class="contact-list">
          {{ "{%" }} if site.author.name -%}
            <li class="p-name">{{ "{{" }} site.author.name | escape }}</li>
          {{ "{%" }} endif -%}
          {{ "{%" }} if site.author.email -%}
            <li><a class="u-email" href="mailto:{{ "{{" }} site.author.email }}">{{ site.author.email }}</a></li>
          {{ "{%" }}- endif %}
        </ul>
      {{ "{%" }}- endif %}
      </div>
      <div class="footer-col">
        <p>{{ "{{" }} site.description | escape }}</p>
      </div>
    </div>

    <div class="social-links">
      {{ "{%" }}- include social.html -%}
    </div>

  </div>

</footer>
```

I modified mine to look like this:

```html

```
