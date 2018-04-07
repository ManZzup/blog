---
title: Jekyll in a sub-domain with GitHub Pages
layout: post
subtitle: A guide to hosting a static non-Jekyll website along with a Jekyll blog in GitHub Pages using the same custom domain and different sub-domains
image: http://manzzup.github.io/blog/public/images/2/pages.png
---

> #### A guide to hosting static non-Jekyll website along with a Jekyll blog in GitHub Pages using the same custom domain and different sub-domains

We all love GitHub pages.

It's free and it's Awesome! 
I practically host all my static content in GitHub, my portfolio included. Something about my portfolio is that due to some bizzare reason it is made in [React](https://reactjs.org/). So the static content is actually the build output of the React app. But my blog on the other hand is running on Jekyll, so far turning out to be my favourite blogging platform.

Here's  the issues, I need to host two kind of static content, but from the same custom domain and I want to host both of them using GitHub Pages!

| [http://manujiththecoder.me](http://manujiththecoder.me) | I want my portfolio here, coming from my main GitHub repo and **not Jekyll**  |
| [http://blog.manujiththecoder.me](http://manujiththecoder.me) | I want the **Jekyll blog** here, also to be hosted in GitHub |

Problemo!

Let's try to build piece by piece.

1) GitHub luckily enables users to host two kinds of pages. The *organization* repo, which is hosted in [YOUR-NAME.github.io](YOUR-NAME.github.io) and *project* repos, which will be hosted as [YOUR-NAME.github.io/project](YOUR-NAME.github.io/project). So first we create our portfolio web site at the organization repo. In my case, [manzzup.github.io](manzzup.github.io) would host my React portfolio. Now we create a second repo, I would call it **blog**. So essentially the link to content hosted in this repo would be served at [manzzup.github.io/blog](manzzup.github.io/blog).

2) Most importantly enable Jekyll for this second repo. For that you goto your repo, navigate to **Settings** and under **GitHub Pages** options, set the **source** to *master* branch or the *docs* branch as per your requirement. Great! Now your blog is working neatly at [YOUR-NAME.github.io/blog](YOUR-NAME.github.io/blog)

3) Next is to configure our custom domain to work as we intend to. Let's say your domain is [mydomain.com](mydomain.com), now you need to point [mydomain.com](mydomain.com) to [YOUR-NAME.github.io](YOUR-NAME.github.io) and [blog.mydomain.com](blog.mydomain.com) to [YOUR-NAME.github.io/blog](YOUR-NAME.github.io/blog).  Goto your organization repo setting and set the custom domain to *mydomain.com* and that of the blog repo to *blog.mydomain.com*. This process is well documented in [Quick start: Setting up a custom domain](https://help.github.com/articles/quick-start-setting-up-a-custom-domain/).

| ![GitHub Pages settings](/public/images/2/pages.png) |
| *GitHub Pages settings* |

4)  Final step is to configure your DNS records to make everything work. You can follow the GitHub guide above or simply set the records as follows.

| **Record Type** | **Host** | **Value** |
| A | @ | 192.30.252.153 |
| A | @ | 192.30.252.154 |
| CNAME | www | yourdomain.com |
| CNAME | blog | YOUR-NAME.github.io |

This woud do.