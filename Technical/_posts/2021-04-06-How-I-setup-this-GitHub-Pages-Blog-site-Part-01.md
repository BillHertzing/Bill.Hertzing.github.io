---
Title: How I setup this GitHub Pages Blog
date:   2021-04-04 12:31:43 -0600
tags: Jekyll "GitHubPages"
category: Technical
layout: post
---

I have been trying for a few years to setup a web site I can use for blogging. But since there are a lot of neat features I'd like to include, every prior attempt has foundered on getting it all to hang together, along with the problems of version control for everything. And of course cost is always a consideration. Now, I'm giving it another try, this time using the GitHub Pages to host my site, and building it with Jekyll, the static site generator. Here are the steps I've taken to implement the features I'd like to have.

If you would like to see a list of the articles online that have helped me create this site, please see the  <a href="#Attributions">Attributions</a> section below.

## Prerequisites

1. A Windows 10 PC (Laptop or desktop)
1. a GitHub account. make a note of your username, and throughout this document, replace *GitHubUserName* with YOUR GitHub username
1. Powershell installed and updated on Windows 10
1. Git for Windows (or alternative Git client) installed on Windows 10
1. Visual Studio Code (VSC) (or similar editor) installed on Windows 10
A. (VSC) GitHub extension module

## Install Ruby and Jekyll on your Windows PC

(if you are cleaning up a botched prior attempt (me!), run this command in a Powershell terminal window `gem uninstall -aIx`)

1. Install [RubyInstaller for Windows](https://rubyinstaller.org/). Select a recent Ruby+DevKit version (I picked `RubyInstaller 3.0.0-1 released`) and use the default options in the installation wizard. On the last step, you’ll want to keep the option “Run ‘ridk install’ to setup MSYS2 and development toolchain.” checked. ToDo: embed .png file of screenshots for these two steps
1. ToDo: Investigate using chocolaty to install both Ruby and MSYS2, whihc will make updating much easier
1. Close the Powershell prompt window, and open a new one (this one will have the updated environment PATH information)
1. At the Powershell prompt, Run `gem install jekyll bundle` This installed Jekyll V4.2.0 (on 2021-04-05), and a total of 28 gems ToDo: embed screenshot
1. Run `jekyll -v` and confirm Jekyll returns its current version number ToDo: embed screenshot

## Create a new git repository

1. Open a Powershell terminal, navigate to the location (directory) you want to be the parent of your repository. My parent directory is `C:\Dropbox\whertzing\GitHub\`.
1. Create a subdirectory `*GitHubUserName*.github.io`, and `cd` into it.
1. Run `git init`

## Create minimal Jekyll-compliant site source code

1. Run `jekyll new PATH` (Use the FULL Path to the repository on your windows PC i.e. `C:\Dropbox\whertzing\GitHub\BillHertzing.github.io`) which will create the bare bones of the new Jekyll-compliant site source code. ToDo: add jpg
1. (optional) I prefer to use `.md` instead of `.markdown` for the suffix of Markdown files, so I now run the two commands `mv about.markdown about.md` and `mv index.markdown index.md`

At this point, I'll diverge from the many other posts about setting up Jekyll, because I want to use non-approved Jekyll Plugins as well as a non-approved Jekyll theme. To do that, I will keep the site source code under the  `main` branch of this repository, map my local `.\_site` to the `gh_pages` branch of this repository, build the site locally on my Windows PC, and push `.\_site` to the `gh_pages` branch on GitHub.

1. edit the `_config.yml` file, and remove a lot of the boiler plate. At this point, mine looks like this:

```yml
# Jekyll configuration file for BillHertzing.github.io

title: Bill's Blog
description: >- # this means to ignore newlines until the next key, which is "baseurl:"
  Technical articles for my code repositories. Position papers on political issues. Cute pictures of the kids. I've got it all!
baseurl: "" # the subpath of your site, e.g. /blog
url: "https://BillHertzing.github.io" # This is a User GitHub Pages site, not a Project site
twitter_username: BillHertzing
github_username:  BillHertzing

# Build settings
markdown: kramdown
permalink: pretty
plugins:
  - jekyll-timeago
  
theme: minima
```

## Download the minima theme

Any Jekyll theme you want to use must first be downloaded to your Windows PC so run `gem install jekyll-theme-minima`.. Today (2021-04-06) it loaded jekyll-theme-minima-0.1.1.gem and 18 other gems (dependencies) as well.

## Verify the local site will build and serve locally on your Windows PC

It is a good idea to be able to see what your site will look like, before committing the changes to GitHub. By default, `jekyll build` will read the site's source form the current directory, and write it to a subdirectory `_site`. and `jekyll serve` will start a local web server and serve `_site` to `http://localhost:4000`. `jekyll serve` will also build the site if any source file has been changed.

1. Open a Powershell terminal and navigate to your repository.
1. Run `jekyll serve`

### Fixing issues

Did you really think that everything would 'just work'?  Hahaha! When I try this today, I get an error message "Could not find gem tzinfo-data". Typically, new versions of one tool might break a dependency used somewhere else. In this particular case, the latest version of Ruby (3.0.0 today) no longer includes that gem by default. So, I needed to run ` gem install tzinfo-data`. Then when I tried `jekyll serve `, I got an error message ""Could not find gem wdm". So I ran `gem install wdm`. And then again for `webrick`, whihc required `bundle add webrick`. Depending on how much things have changed between the time I write this and the time you try to follow it, there may be other dependency changes, so just keep on trying to build and fixing the issues, until `jekyll serve` completes and starts serving up pages.

`cannot load such file -- C:/Ruby30-x64/lib/ruby/gems/3.0.0/gems/bundler-2.2.3/libexec/bundle (LoadError)` - `gem install bundler`  then edit the gemfile.lock and change teh bundled with line at the bottomt to match the version just installed.

Finally Jekyll will serve the site locally. Use the browser of your choice and navigate to http://localhost:4000. with the minima theme it should look like this:
ToDo: Insert .jpg

## Replace the original `welcome-to-jekyll.markdown page

1. In the `_posts` subdirectory, add a new file with the format `*YYYY-MM-dd-welcome-to-*whatever*`. use your current year-month-day numerals, and change *whatever* to whatever you want to call your first welcome post.  I used `2021-04-06-Welcome-To-Bills-Blog.md`
1. look at the original file in the _posts directory, which was created by the initial `jekyll new PATH` command earlier, and copy the Front Matter to your new post, update the front matter to change the title, and optionally remove the categories.
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
1. Run `git remote add origin  <REMOTE_URL> `  Of course, replace <REMOTE_URL> with the URL you just copied from GitHub. Mine looked like this: `git remote add origin https://github.com/BillHertzing/Bill.Hertzing.github.io.git`
1. Run `git remote -v` to confirm that the origin is indeed set to the URL for the remote repository you just created on GitHub.
1. Run `git branch -M main` and then `git push -u origin main`  Pushes the changes in your local repository up to the remote repository
1. Verify the source code for your site is now in GitHub. ToDo: add jpg

## Setup Visual Studio Code (VSC) 

1. Open the Visual Studio Code application.
1. Select `Open folder` and navigate to the new repository you just created. To Do: insert jpg

## Confirm that VSC can push changes to GitHub

1. Open the about.md file for editing, select everything after the front matter (line 7 and onward as of today), and delete it. then add the word 'test' on line 7.
1. Save the file. Note that the Source Control button on the link now has a badge with the number (1) and the `about.md` file indicates M for Modified. ToDo: insert jpg 
1. Click the Source Control button. 
1. In the message box, enter `remove unneeded parts of about.md`, then click the `check` above the message box (alt text is 'Commit')
1. Note that the bottom status bar now shows there is one local commit that has not been pushed to the remote. ToDo: insert jpg
1. Click on that area of the status bar, and the change should be pushed to GitHub
1. On GitHub, open the about.md file, and confirm that the change has been pushed to the GitHub remote repository.

ToDo: Interesting, while working on this, I learned if VSC is not logged in to anywhere, and you chose to login to GitHub, there is an authentication interaction that stores some information into VSC somewhere. I should investigate and write it up...  It opened GitHub in Chrome (my default browser), and I entered my password to GitHub. There was a form asking if I wanted to authorize, said yes, then a redirect on github, and a dialog box saying that there was a uri that wanted to open VSC. I allowed that dialog to "open the VSC app. Since it was already open, it just switched me back to the VSC instance. Nothing added to the repository where I was working, so either somewhere in VSC or somewhere in Windows, there is now an association "vscode://vscode.github-authentication/did-authenticate?windowid=1&code=a_very_long_alphnumeric_string"

## Enable GitHub pages on the GitHub repository

1. Navigate to the `Code` view of the repository
1. Create the branch `gh-pages`. 
1. Open Setting on the GitHub repository. ToDo: insert jpg
1. Scroll down to the GitHub Pages section.
1. Type `gh-pages` for the branch name. ToDo: insert jpg

## Add a workflow file `deploy-site-to-github-pages.yml`

This workflow and the actions it contains are the key to an easy blogging workflow. A great piece of OSS for GitHub Actions, combined with a workflow trigger that detects a release tag, make it all work.

See the details of the Action here: [peaceiris/actions-gh-pages](https://github.com/peaceiris/actions-gh-pages) by peaceiris and other contributors, and the details of the trigger here: [Git Tag Based Released Process Using GitHub Actions](https://www.codingwithcalvin.net/git-tag-based-released-process-using-github-actions/) by Calvin A. Allen.

1. Create the directory and subdirectory `.github\workflows` in the repository.
1. Create the file `deploy-site-to-github-pages.yml` in the `.github\workflows` subdirectory

ToDo: figure out how, at site generation time (`jekyll build`) to read the contents of the actual file and update the text below with the actual contents.
ToDo: decide on a strategy for updating a historical post if the file changes. perhaps a revision tag for posts?
ToDo: Figure out how notify subscribers to the RSS feed if a existing post gets a new revision.
ToDo: Figure out how to e-mail an administrator if a code change triggers the need to create a post revision

Put the following yml code into the file, and then save it.

```
name: deploy generated site to GitHub Pages on gh-branch 

on:
  # Triggers the workflow on push requests to the main branch if the commit includes a tag that matches the Semantic Version release tag
  push:
    tags: releases/\d+\.\d+\.\d+
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
      
      # Deploys a source to a destination.
    - name: Deploy
      uses: peaceiris/actions-gh-pages@v3
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
        publish_dir: _site # the action will deploy the _site contents to the (default)gh-pages branch, root directory
        
```

Commit the new file and commit the changes.

## create an Environment for the deployment action

1. On GitHub, in the repository, under `Settings`, open the `Environment` tab, and click `Create Environment` ToDo: insert jpg
1. Name the Environment `deploy-site-to-github-pages`, and click `Configure Environment` ToDo: insert jpg
1. Click `x` on the following page to acknowledge the environment was created, and go back to the Settings->Environemnt page ToDo: insert jpg
1. Click on the name of the environment just created.
1. At the bottom of the page, click the `Add Secret` button. ToDo: insert jpg
1. Add a Secret with the name `ACTIONS_STEP_DEBUG` and value `true`. You can remove this Secret after the action has been debugged. There is an additional Secret `ACTIONS_RUNNER_DEBUG` whihc if set to `true` will provide more details in the logs. I like to set this, as well. ToDo: insert jpg

The final Environment should look like this: ToDo: insert jpg

## Remove _site from the .gitignore file

1. Edit the .gitignore file in the root of the repository, and remove the `-site` line. save
1. Validate the site build and displays as expected locally on your Windows PC
1. Note that the Source Control icon has a number, and the Changes editor now shows multiple new files under _sites to be committed
1. Commit all the changes. I  used the message "Start tracking `_site`"  *note* I made the changes to the original post, as specified above at (ToDo: insert link to previous place ) at this point in the development, so the jpg file also hows me removing one file and adding another file in `_posts` ToDo: insert jpg
1. Sync with the remote repository.
1. Validate the `_site` and its files are now present on the GitHub repository. ToDo: insert jpg

## Review the workflow run

1. Navigate to the actions tab in your repository. ToDo: insert jpg
1. Drill down into the latest workflow run. ToDo: insert jpg
1. Drill down into the job log. ToDo: insert jpg
1. Expand the `Deploy` step. ToDo: insert jpg

## troubleshooting the workflow run

uh-oh, another issue that needs troubleshooting. Luckily that problems has been noted in the documentation for the GitHub Action, at [First Deployment with GITHUB_TOKEN](https://github.com/peaceiris/actions-gh-pages#%EF%B8%8F-first-deployment-with-github_token). Instructions there tell us to 

1. Go to the repository's Settings tab, scroll down to GitHub Pages section, change the source to gh-pages branch and save.
1. While the example says to just deploy again, our workflow is supposed to only trigger on release tags, so trigger the workflow manually by going to Actions, and click on the workflow name in the left column. ToDo: insert jpg
1. You should see a 'Run workflow' button. Click it, and the workflow will run. Go back to Actions tab, and there should be a new workflow run. Drill down into it, and expand the log, and open the Depolu section again, and we see...  ToDo: insert jpg

darn, still not working. Looks like this is the problem `cp: no such file or directory: /home/runner/work/Bill.Hertzing.github.io/Bill.Hertzing.github.io/_site/.*`.
I've updated the publish_dir from _site to ./, no joy, and tried 


## Invoke `deploy-site-to-github-pages` manually


