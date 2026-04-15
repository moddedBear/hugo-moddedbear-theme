# Hugo moddedBear Theme

## Overview

The Hugo moddedBear theme is a lightweight [Hugo](https://gohugo.io/) theme based on the following:
- [Bear Blog](https://bearblog.dev)
- [Hugo Bear Blog](https://github.com/janraasch/hugo-bearblog)
- [Bear Cub (from which this theme is forked)](https://github.com/clente/hugo-bearcub)

This theme has many of the same goals as Bear Blog and the various other themes inspired from it. It's fast and minimal, but it also strives to provide some of the more advanced features many personal bloggers will appreciate out of the box.

When I started my website, I used Jan Raasch's Hugo Bear Blog theme. Over time I found myself overriding the theme to add features and tweaks often enough that it made less and less sense to be using the theme in the first place. I decided to refactor by moving my changes into a proper theme of their own, which is what you're looking at now. In the process, I've tried to make the theme as organized and customizable as possible in case others want to use it or learn from it.

The best place to see the theme in action is on [my website](https://moddedbear.com), though there is an example site included with the theme to help you get started.

## Differences from the Bear Cub theme

Features from the [Bear Cub theme](https://github.com/clente/hugo-bearcub) have been kept intact unless otherwise noted. These are the notable differences.

### Additions
- Automatic light/dark mode
- Overhauled homepage
  - Avatar image
  - Recent and featured post sections
  - Tag list
  - All features can be individually hidden via config
- Easy theming via CSS properties
  - Copy `/assets/properties.css` from the theme to `/assets` in your site and edit to taste
- Easy Mastodon/Fediverse integration via config
  - Profile verification
  - Author attribution
- Optional table of contents
- External post comments
  - Add a link on your frontmatter to somewhere where people can leave a public comment, like a Mastodon or other social media post
- Anchor links on headings in posts
- RSS feeds for each tag (these were already being generated but are now linked to when filtering by tag)
- Custom home footer
  - Useful for webrings or similar
- A ntfy ping widget allowing visitors to send messages to a ntfy topic
- Integrated [bubbles.town](https://bubbles.town) widget

### Changes
- Tweaked generated social card colors
- Replaced "reply by email" link with generic link to contact page
  - May be better if like me you have multiple forms of contact
- Default config puts blog permalinks at `/` instead of `/blog/`
- Minor style tweaks to taste

## Installation

Follow Hugo's [quick start](https://gohugo.io/getting-started/quick-start/) to
create an empty website and then clone **Hugo moddedBear** into the themes directory as
a [Git submodule](https://git-scm.com/book/en/v2/Git-Tools-Submodules):

```sh
git submodule add https://github.com/moddedBear/hugo-moddedbear-theme themes/hugo-moddedbear
```

Make sure the theme is set in your site config:

```toml
theme = "hugo-moddedbear"
```

## Configuration

**Hugo moddedBear** can be customized with a `hugo.toml` file. Check out the
[configuration](https://github.com/moddedBear/hugo-moddedbear-theme/blob/main/exampleSite/hugo.toml)
of the example site for more information.

```toml
# Basic config
baseURL = "https://example.com"
theme = "hugo-moddedbear-theme"
copyright = "John Doe (CC BY 4.0)"
defaultContentLanguage = "en"

# Generate a nice robots.txt for SEO
enableRobotsTXT = true

# Generate "Bearblog"-like URLs !only!, see https://bearblog.dev/.
disableKinds = ["taxonomy"]
ignoreErrors = ["error-disable-taxonomy"]

[permalinks]
  blog = "/:slug/"
  tags = "/blog/:slug"

# Setup syntax highlighting without inline styles. For more information about
# why you'd want to avoid inline styles, see
# https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/style-src#unsafe_inline_styles
[markup]
  [markup.highlight]
    lineNos = true
    lineNumbersInTable = false
    # This allows Bear Cub to use a variation of Dracula that is more accessible
    # to people with poor eyesight. For more information about color contrast
    # and accessibility, see https://web.dev/color-and-contrast-accessibility/
    noClasses = false

# Multilingual mode config. More for information about how to setup translation,
# see https://gohugo.io/content-management/multilingual/
[languages]
  [languages.en]
    title = "Hugo moddedBear"
    languageName = "en-US 🇺🇸"
    LanguageCode = "en-US"
    contentDir = "content"
    [languages.en.params]
      madeWith = "Made with [Hugo moddedBear](https://github.com/moddedBear/hugo-moddedbear-theme)"
  [languages.pt]
    title = "Hugo moddedBear"
    languageName = "pt-BR 🇧🇷"
    LanguageCode = "pt-BR"
    contentDir = "content.pt"
    [languages.pt.params]
      madeWith = "Feito com [Hugo moddedBear](https://github.com/moddedBear/hugo-moddedbear-theme)"

[params]
  # The description of your website
  description = "Hugo moddedBear Theme Demo"

  # The path to your favicon
  favicon = "images/favicon.png"

  # These images will show up when services want to generate a preview of a link
  # to your site. Ignored if `generateSocialCard = true`. For more information
  # about previews, see https://gohugo.io/templates/internal#twitter-cards and
  # https://gohugo.io/templates/internal#open-graph
  images = ["images/share.webp"]

  # The path to your avatar image for use on the home page. It should be somewhere
  # in the /assets directory. You can comment or remove this line to hide the image.
  avatarImage = "images/avatar.png"
  avatarImageAlt = "My avatar" # A description of your avatar image

  # This title is used as the site_name on the Hugo's internal opengraph
  # structured data template.
  # See https://ogp.me/ and https://gohugo.io/templates/internal#open-graph.
  title = "Hugo moddedBear"

  # Dates are displayed following the format below. For more information about
  # formatting, see https://gohugo.io/functions/format/
  dateFormat = "Jan 2, 2006"

  # If your blog is multilingual but you haven't translated a page, this theme
  # will create a disabled link. By setting `hideUntranslated` to true, you can
  # have the theme simply not show any link
  hideUntranslated = false

  # (EXPERIMENTAL) This theme has two options for its CSS styles: "original" and
  # "herman". The former is what you see on Bear Cub's demo (an optimized
  # version of Hugo Bear Blog), while the latter has a more modern look based on
  # Herman Martinus's version of the Blogster Minimal theme for Astro.
  themeStyle = "herman"

  # (EXPERIMENTAL) This theme is capable of dynamically generating social cards
  # for posts that don't have `images` defined in their front matter; By setting
  # `generateSocialCard` to false, you can prevent this behavior. For more
  # information see layouts/partials/social_card.html
  generateSocialCard = true

  # Whether to hide the footer containing copyright and "made with" notices.
  hideFooter = false

  [params.home]
    hideRecent = false
    numRecent = 5 # Number of recent posts to display
    hideFeatured = false
    hideTags = false

  [params.blog]
    # The path to your contact page for visitors to be taken to when clicking the
    # reply link at the end of a post. Comment to disable this functionality.
    # contactPage = "/contact"
    useBubbleWidget = false  # add a widget for bubbles.town to the bottom of each post
  
  [params.list]
    tagsOnTop = false # Display tags at top of the post list instead of bottom

  # Social media. Delete any item you aren't using to make sure it won't show up
  # in your website's metadata.
  [params.social]
    twitter = "example" # Twitter handle (without '@')
    facebook_admin = "0000000000" # Facebook Page Admin ID
    fediverse = "https://example.com/@me" # Link to profile for verification

  # Author metadata. This is mostly used for the RSS feed of your site, but the
  # email is also added to the footer of each post. You can hide the "reply to"
  # link by using a `hideReply` param in front matter.
  [params.author]
    name = "John Doe" # Your name as shown in the RSS feed metadata
    email = "me@example.com" # Added to the footer so readers can reply to posts
    fediverse = "@me@example.com" # For attribution (@user@example.com)

  # Parameters for the ntfy ping widget
  [params.ntfy]
    # server = "example.com"  # comment to disable the widget
    # topic = "blog-pings"
    # token = "token"  # ideally should be tied to a user with limited access

```

## Contributing

If you come across any problems while using **Hugo moddedBear**, you can file an
[issue](https://github.com/moddedBear/hugo-moddedbear-theme/issues) or create a [pull
request](https://github.com/moddedBear/hugo-moddedbear-theme/pulls).
