+++
date = '2024-11-22T22:29:01+01:00'
draft = false
title = 'Social Icons in Hugo Ananke Theme'
+++
## Introduction
After completing the initial setup of my blog, I wanted to add a social icon in the header/navbar. After some searching, I found [this documentation](https://github.com/theNewDynamic/gohugo-theme-ananke/wiki/Social-media-network-setup/) on the [Ananke theme](https://themes.gohugo.io/themes/gohugo-theme-ananke/)'s [wiki](https://github.com/theNewDynamic/gohugo-theme-ananke/wiki).

## Why am I writing this post?
Even though there is a [wiki page](https://github.com/theNewDynamic/gohugo-theme-ananke/wiki/Social-media-network-setup/) "explaining" how to configure social icons, I was still confused by it, so I'm writing this in case it might help someone else.

## How it works
> All samples in this documentation will refer to configuration in config/_default/params.toml and use the TOML format. If you have problems translating that into your configuration situation and format (JSON, YAML) please join us in the Discussion Forum.
>- ananke.social.share configures share buttons/links on single pages/posts
>- ananke.social.follow configures social network links in "follow us on social media" widgets
>- ananke.social.networks configures single networks. if user wants to extend, they add a new item to their local param section
>- ananke.social.$slugname is individual configuration for the networks defined in ananke.social.networks that is to be set for the implementing site in the individual configuration

Now, I'm not using [`config/_default_params.toml`](https://gohugo.io/getting-started/configuration/#configuration-directory), I'm using `hugo.toml`, I'm guessing they do pretty much the same but we are already starting to get a mismatch.

Secondly, I don't know what are
- ***share buttons/links on single pages/posts***
- ***social network links in "follow us on social media" widgets***
- ***the rest of the presented configurations***

This might be a lack of reading comprehension or another issue, but I wasn't able to understand what these configurations *actually* represented.

I basically guessed that
```toml
[ananke.social.follow]
new_window_icon = false
networks = [
  "facebook",
  "bluesky",
  "linkedin"
]
```
is used to define which social networks to "enable".
and
```toml
[params.ananke.social.linkedin]
username = "patrickkollitsch"
profilelink = "https://th.linkedin.com/in/patrickkollitsch/"
```
is used to define the social network's specific configuration (That was an easy guess).

Now, in the first configuration, you have to prepend `params.` to `ananke.social.follow` like this
```toml
[params.ananke.social.follow] # not [ananke.social.follow]
new_window_icon = false
networks = [
    ...
```
or it just won't work.

Anyways, if you copy pasted properly, it should look like the following:

![Socials Icons in the navbar](/images/social_icons.png)

## Customize the social icons
If you want to modify the look of the social icons, you will need to copy Ananke's `"follow.html"` partial in [`themes/layouts/partials/social/follow.html`](https://github.com/theNewDynamic/gohugo-theme-ananke/blob/40c8d5f5eea3034ce80b7c86d705da1027b638c4/layouts/partials/social/follow.html) and paste it into your own [`layouts/partials/social/follow.html`](https://github.com/D14rn/blog/blob/153012cd56ca580ed39676c231b821d1a7f72374/layouts/partials/social/follow.html) so that Hugo can use your custom partial instead.

Also, yes, as far as I know (which isn't a lot), you will have to manually update your custom partial every time Ananke's is changed/updated (or not if the update doesn't break anything).

## My configuration
I only wanted a GitHub icon that redirects to the blog's repository, so I did the following.

hugo.toml
```toml
[params.ananke.social.follow]
networks = [
  "github"
]

[params.ananke.social.github]
username = "D14rn"
profileLink = "https://github.com/D14rn/blog"
```

layouts\partials\social\follow.html
- Copied the file from Anankes's
- Deleted the title and aria-label attributes inside the &lt;a&gt; tag because it annoyed me to have some text popup when I was hovering the icon

## Conclusion
I hope this article helped you, or maybe it didn't, but hey, such is life!

## Quick references

### Links
- [TOML](https://toml.io)
- [Ananke Gohugo Theme](https://themes.gohugo.io/themes/gohugo-theme-ananke/)
- [Ananke Wiki](https://github.com/theNewDynamic/gohugo-theme-ananke/wiki)