---
title: Subscribe To Bill's Blog
layout: single
permalink: /subscribe-to-bills-blog/
description: How to subscribe to posts from Bill's Blog site
tags: [subscribe, "RSS Feed"]
Category: technical
---

## Get Notified of New Posts

The site provides an RSS Feed, and anyone can setup their systems to get an e-mail when a new post is published.

In the spirit of Open Source Software (OSS), the components to do this are free, and the instructions are not too onerous. In fact the instructions come from an article published at [Gizmodo](https://gizmodo.com/).

[Turn Gmail Into an RSS Reader With IFTTT](https://gizmodo.com/turn-gmail-into-an-rss-reader-with-ifttt-1582552035) by David Nield published May 28th, 2014.

Details and fascinating possible exploration paths into home automation are in teh article, but here are teh specific details I used. You can only have three applets on the IFTTT free plan. I'm going to show you how to create one of them.

1. Register at IFTTT.com. Your login will open the doors to some pretty cool home automation you can do.
1. The applet we will create will look similar to this: ToDo: insert jpg.
1. From the Gizmodo article (Edited to insert the RSS feed for `Bills Blog`):

   ```text
    ...sign up for a free account 
    and then click the `Create` button at the top to start building a recipe. 
    Choose `Feed` as the trigger channel 
    then pick `New feed item`. 
    Enter a valid RSS link
      —such as https://billhertzing.github.io/feed.xml 
    -and click `Create Trigger`.
    Congratulations! You have completed the first half of the process.
   ```

1. Set up the Action. Again, the text is from the Gizmodo article.

    ```text
    Select `Email` as your action channel (not Gmail).
    If you don't already have an email address associated with IFTTT then you'll be prompted for one.
    Select `Send me an email` as the action (it should be the only option available).
    You can customize the layout of the emails you receive.
    ```

1. Save

And that's it! You will get an e-mail each time I publish a new post, or edit an existing post.  I strongly suggest you check out the Gizmodo article, which discusses how to use stars and categories to organize your e-mails from multiple RSS feeds, since once you learn this skill, you may want to subscribe to other site's feeds, too!
