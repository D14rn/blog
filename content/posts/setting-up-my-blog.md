+++
date = '2024-11-22T18:41:59+01:00'
draft = false
title = 'Setting Up My Blog'
+++
## Introduction
For the past few days, I've been working on a project where one of the features is [authentication and authorization](https://www.ibm.com/think/topics/authentication-vs-authorization) using [OpenID Connect](https://openid.net/developers/how-connect-works/), and [Keycloak](https://www.keycloak.org/) is the service that was chosen to perform this role.

Today, I was trying to find some resources explaining how to use Keycloak properly, because I implemented everything and wanted to see if there were some improvements I could make. I came across [this post](https://karuppiah7890.github.io/blog/posts/introduction-to-keycloak/) after some research on google.

While this post didn't really help me find what I was looking for, I noticed that the blog it was part of was hosted on github pages (due to the github.io domain). So naturally, I branched off my current course of action and looked at [the repository](https://github.com/karuppiah7890/blog) of the blog's owner and I discovered that it was created using [Hugo](https://gohugo.io/).

I was very intrigued by how seemingly easy Hugo makes it to create static websites so I got the idea of using it to make my own blog, and here we are!\
P.S.: I did compare different Static Site Generators (
    [Gatsby](https://www.gatsbyjs.com/docs/glossary/static-site-generator/), 
    [Jekyll](https://jekyllrb.com/),
    [Next.js](https://nextjs.org/docs/pages/building-your-application/rendering/static-site-generation), 
    [Hugo](https://gohugo.io/), 
    [Eleventy/11ty](https://www.11ty.dev/), 
    [Zola](https://www.getzola.org/)
    ) they all seemed quite similar, and while Hugo did have quite a bit of criticism in the sources I checked, I still chose it, mostly because I already got familiar with it by checking out the repository of the blog I stumbled upon.

## How I set it up

The setup process was pretty straightforward, I just followed the instructions in:
- [The installation guide](https://gohugo.io/installation/) (didn't install Dart Sass & already had Git)
- [The quickstart guide](https://gohugo.io/getting-started/quick-start/)
- [Deploying and hosting on Github pages](https://gohugo.io/hosting-and-deployment/hosting-on-github/) (I removed the Dart Sass step and updated the HUGO_VERSION from 0.137.1 to 0.139.0)

I did encounter some new concepts like:
- [Difference between Powershell and Windows Powershell](https://learn.microsoft.com/en-us/powershell/scripting/whats-new/differences-from-windows-powershell?view=powershell-7.4&viewFallbackFrom=powershell-7.3)
- [Git submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules) for the themes (already encountered them but I went more in-depth this time)

Anyways, I'm not exactly sure what I wanna do with this blog, but it was a fun experience just setting it up!

## Quick references
### Links
- [Hugo Configuration](https://gohugo.io/getting-started/configuration/)
- [Hugo Commands](https://gohugo.io/commands/)

### Commands
```bash
# Adding the submodule repository
git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke

# Create a new post
hugo new posts/<post-name>.md
hugo new content posts/<post-name>.md

# Start live server with drafts enabled
hugo server -D
hugo server --buildDrafts

# After cloning a repository with a submodule
git submodule update --init --recursive
```