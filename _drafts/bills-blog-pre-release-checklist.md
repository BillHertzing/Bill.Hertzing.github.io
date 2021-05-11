---
title: Bills Blog Pre-Release Checklist
Description: Checklist for use prior to starting the Release process for <Post/Bug/Feat> release
category: technical
tags: [Pre-Release Checklist, Process]
---

Things about the release candidate to validate before starting the [Release process](bills-blog-release-process.md)
## Conventions

<Feat/Bug/Post-Branch> is the name of the branch that is being evaluated for release. The branch being evaluated for release will be referred to as the Release Candidate in this document.

## Criteria and Evaluation 

1. Checkout the <Feat/Bug/Post-Branch> with Visual Studio Code (VSC).
1. Review any `warnings` that appear in VSC's `problems`. pane. Clean up the underlying issue, or decide they are OK to live with for this release. Commit any changes made during this step to `<Feat/Bug/Post-Branch>` using a WIP  commit message. Push these commits to the remote.

## Check text spelling, grammar, and case-consistency on proper names 

Using VSC:
  - Use a spell checker plugin and ensure it reports no misspellings
  
Using Grammarly:
  -  [ToDo: write instructions on using the unofficial Grammarly VSC plugin on a draft post]
  
Ensure that proper names that refer to software or hardware concepts and company names, are consistent across the site.
  - [ToDo: write a script that tests the site for proper noun casing consistency]

## Check post and page layout consistency

ToDo: 

## <a name="Site Checks"></a>Site Checks

The following subsections provide details about specific items to validate.

### Check Images

For posts that include images, ensure the links in the post properly reference images hosted in 3rd party clouds
- Images are created in multiple responsive sizes
- Image thumbnails are created
- Images are checked for any PPI in the metadata,and scrubbed
- Images comply with accessibility guidelines - `Alt` text and navigation aides
- Get final links to images (not videos)
    For Dropbox hosted images:
      - Get a Dropbox developer access token from https://www.dropbox.com/developers/apps. [ToDo: link to attributions on how to create a Dropbox account, developer credentials, and an app to allow API access to dropbox]
      - Run `$env:DropBoxAccessToken = "<DropBoxAccessToken>"
      - [ToDo: link to document describing how to access the ATAP Powershell BuildTooling modules]
      - Run `$env:psmodulepath = "./;" + $env:psmodulepath`
      - Run the Powershell script `Get-DropboxSharedLinks.ps1' -verbose -path "Dropbox-path-to-folder-having-links"`
      - Validate the references to images in the post use the link information returned 
      - [ToDo: A script to automate link checking the document and the links from Dropbox]
    - For Google Photos hosted images:
      - [ToDo: write instructions and scripts for Google Photo hosted images]
    - For Microsoft Drive hosted images:
      - [ToDo: write instructions and scripts for Microsoft Drive hosted images]

- [ToDo: write a script that tests each image the site and all its posts reference]


### Check internal links

Ensure that all links in the post that refer to anchor points within the same post, or to anchor points in other points, work correctly. All Headings in `.md` documents should include an explicit anchor point. Links to headers in `.md` documents should refer to the anchor point associated with that header. See also the many answers to this StackOverflow question [Cross-reference (named anchor) in markdown](https://stackoverflow.com/questions/5319754/cross-reference-named-anchor-in-markdown) for more insight into why explicit anchors are desirable..


### Check Styling

ToDo checklist including responsive tests

### Check Scripts

If the site contains any JavaScript functions, these need to be checked.

  - [ToDo: write a testing document that describes how to test each JS script / function incorporated into the site]
  - [ToDo: write a script that tests each JS script / function incorporated into the site]

### Check Security

It is very important to ensure that nothing in the site allows bad actors to violate its security. This is especially true of any site features that store persistent data

  - [ToDo: write a security document that describes how to test the site's security for data-at-rest, and data-in-transit]
  - [ToDo: write a security document that describes how to use `secrets` while developing the site]
  - [ToDo: write a script that tests the site for Security]

### Check Accessibility 

  - [ToDo: write a development and testing document(s) that describes how to design and test the site for Accessibility]
  - [ToDo: write a script that tests the site for Accessibility]

### Check Globalization and Localization

  - [ToDo: write a development and testing document(s) that describes how to design and test the site for Globalization and Localization]
  - [ToDo: write a script that tests the site for Globalization and Localization]

## Check the Release Candidate works on the Internet

The Release Candidate has to be tested "as if" it was publicly accessible from the Internet. This focuses on the availability of content that is served from locations other than the main site, e.g. images, JS libraries, and CSS libraries.

### Setup `ngrok``

 - See [Getting Started with ngrok](https://dashboard.ngrok.com/get-started/setup)

### Publish to Internet via ngrok

1. Run `$env:JEKYLL_ENV = 'production'; bundle exec jekyll serve` to ensure that `_site` has been built with no drafts and with Disqus comments enabled.
1. Run `ngrok` from a Powershell prompt.
1. Copy the ngrok link information that is displayed
1. Using multiple different computers and devices with multiple different screen sizes, evaluate the public site (ngrok link) against the criteria in [Site Checks](#Site Checks) .

Stop the local Jekyll server and close the ngrok channel

## Steps to publish a draft post

if the site release includes one or more posts to be published, follow these steps to move the post from its drafts state to the published state.

  - [ToDo: write a document that describes how to move a post from draft to production]
  - [ToDo: write a script that moves a post from draft to production]
1. Ensure the terminal is at the root of the repo
1. Run `bundle exec jekyll publish "_drafts/Word-Template-for-letter-to-CPA-HOA-regarding-sale-of-golf-course.md"``
1. Run `mv  _posts/2021-05-01-Word-Template-for-letter-to-CPA-HOA-regarding-sale-of-golf-course.md political/2021-05-01-Word-Template-for-letter-to-CPA-HOA-regarding-sale-of-golf-course.md`
1. *ToDo: fix the git issue, figure out how to tell git that the draft is renamed to the post. Git thinks its a delete and an add. Automate this 
1. Ensure the file has been moved and renamed, to the correct category subdirectory and the proper date prefix added.
1. Run `bundle exec jekyll serve` and validate the new post passes the [New Post Checklist](ToDo: Real Soon Now)


