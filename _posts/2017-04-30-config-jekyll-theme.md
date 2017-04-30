---
layout: single
title:  Config Jekyll Theme
date:   2017-04-30
tags: jekyll theme
---
Spent an afternoon finding and configuring the site's theme. Ended up in [Minimal Mistakes](https://mmistakes.github.io/minimal-mistakes/) for its detailed documentation and rich features. Two alternatives worth to try after I become more familar with Jekyll are: [Lanyon](https://github.com/poole/lanyon) and [Amplify](https://github.com/ageitgey/amplify).

As said, the detailed documentation is what likes about this theme. So configuring is just following the doc step by step. Most features are new to me so I enable most of them just to get some experience and decide later whether to keep them on or not. Some changes I made are:

#### Enable Disqus

I need to apply for a `shortname` on Disquz, which is kind of cool.

#### Enable Twitter Cards.

Just supply your Twitter handle is all.

#### Enable Google Analytics

The document provides 2 options using Google but it seems now `google-universal` is the only way to go.

```yaml
analytics:
  provider               : false # false (default), "google", "google-universal", "custom"
```
