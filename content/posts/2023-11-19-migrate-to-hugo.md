---
title: Migrate to Hugo
date: 2023-11-19
enableGiscus: true
tags: [hugo, github pages]
---
Yesterday, I finally spent some time to fix my broken blog. Previously my blog was miserable: it didn't have HTTPS so every time you visit you need to take a deep breath and tell your browser that you want to proceed with the high risk. Then about 2 weeks go the website was completely melt down. I wish I had took a screenshot but basically all the styles were gone, and the blog were like the kind of website that you could build by letting a money typing on a computer in the 90s.

So I have to fix it. My goal is to write blog every week and attracting visitors. Having visitors is vital because without it I wouldn't be motivated to keep writing and improve my writing. And I know that a broken site won't get any visitor, especially for a random author like me. Plus it's really embarrassing to see that my personal website broken like that.

Next the question is how to fix it. I could try troubleshooting the issue, fix it and call it a day. But the thing is I completely forgot how the site generator ([Jekyll](https://jekyllrb.com/)) and the theme ([minimal-mistakes](https://github.com/mmistakes/minimal-mistakes)) I used works. Plus the version of the theme was so outdated (I resumed blogging recently after 6-year break). So the effort I spent fixing it could be equivalent to starting from scratch. For example, I don't even remember how to preview the article before publishing it!

After some serious research and debating (less than 10 min) I decide to migrate to [Hugo](https://gohugo.io/). The reasons are:
* It's written in Go, my favorite programming language, so if anything went wrong I could in theory debug it
* It's fast. I'm mostly taking other people's words here but as a Gopher, I'm confident it surely will be faster than ruby, python or nodejs based application
* They were used in two of my previous start-up employers to generate company blogs so I know from first hand experience that it can be trusted by company therefore could suit a individual blogger like me.
* I don't want to waste time researching site generators so the second I think of Hugo I know that's it!

So I open the [Quick start](https://gohugo.io/getting-started/quick-start/) and within 5 mins I saw my new blog running locally filled with existing articles. It was great out-of-box experience.

I picked the [PaperMod](https://github.com/adityatelange/hugo-PaperMod/) theme as I quite like its minimalistic style and rich feature sets. The 7.5K stars on Github definitely make choosing it easier. This took me about another 10 min.

Next is to add navigation links. Basically I want my blog to have an Archive, About and Search page. The [Archive](https://github.com/adityatelange/hugo-PaperMod/wiki/Features#archives-layout) and [Search](https://github.com/adityatelange/hugo-PaperMod/wiki/Features#search-page) link are easy as they are mentioned in the documentation. The About page is not that straightforward though as it was not covered so I have to use try-and-error to get it done.

I then added the favicon, google analytics, social icons (twitter and github), all with ease as either the theme wiki has the how-to or could be found in the demo website's repo's [config](https://github.com/adityatelange/hugo-PaperMod/blob/exampleSite/config.yml).

So far my new blog has all the bells and whistles of my previous blog and running happily on my mac. Then I followed the [official guide](https://gohugo.io/hosting-and-deployment/hosting-on-github/) to deploy it to github pages. Unlike my previous blog which was deployed on a branch, Hugo used github Action to deploy. At first I thought this is too complicated compared to the just-push-the-branch approach. But again it worked out-of-box the first time the Action got triggered and I could see my branch new blog running on my domain. Not too bad!

![my home page after first deploy](/first-hugo-deploy.png)

However, in the github pages setting, there were 2 errors. One is that github says the DNS's check is not successful and it's due to incorrect IP setting in my domain's DNS setting. And the other is that I couldn't enforce HTTPS because again something wrong with my domain setting. I logged in to my domain registrar (Google) and deleted a weird A record with some 19x.xxx.xxx IP in it as I thought it must be some testing I did a few years ago and I forgot to clean up. But I was wrong because after deleting it, I couldn't visit my blog under my domain! Panic, panic!

It turns out the A record is needed if I want to visit my blog using [apex domain](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site#configuring-an-apex-domain) but my guess is that over the years the IP addresses are changed so that's why it was complaining. After adding back the A record with the new IPs, my site is back.

![google domain custom records](/google-domain-custom-records.png)

Even better when I check back custom domain setting in github pages, I find that can enable the **Enforce HTTPS** option!

![github custom domain setting](/github-custom-domain-setting.png)

This cost me about 1 hour but it surely feels good to see your site joining the crowd to use HTTPS and chrome doesn't throw all the scary things to you.

The last thing I did is to add a comment section to my blog. Initially I thought Disqus is the way to go; after all, it's mentioned in the [official doc](https://gohugo.io/content-management/comments/). But there's a fatal flaw: it's not free (and all the privacy related reasons. but most importantly is it's not free). So I need an alternative. After seeing several blogs adopting [Giscus](https://giscus.app/), I decided to give a try. I thought it was an easy thing given the experience I had with Hugo so far but man I was wrong!

I mainly followed this [article](https://www.justinjbird.me/2023/adding-comments-to-a-hugo-site-using-giscus/) to add the comment section. After I add the Giscus script to my customized footer template, I can see the comment section loaded. The only problem is that it's shown in every page, including homepage, search page. It should only be shown in the blog page as I don't want to see comments on my homepage. But I couldn't disable them successfully as somehow the param was not working properly. After troubleshooting it for 2 hours, I find that it has something to do with the `partialCached` on the following [line](https://github.com/adityatelange/hugo-PaperMod/blob/master/layouts/_default/baseof.html#L24)

```
    {{ partialCached "footer.html" . .Layout .Kind (.Param "hideFooter") (.Param "ShowCodeCopyButtons") -}}
```

My theory is: `partialCached` is using some cache to render footer to speed up as most of time the footer of every page is same. But in my case, I added the Giscus partial to the footer and the partial will show or hide comments based on params of each page and they could be different. Once I replace `partialCached` with `partial` it works as expected. It was very night then so I decided to go with this workaround and find a better solution in the future.

This is my first Hugo experience. BTW, after my new blog is up I had a glance of my recent blogs. They look terrible: big chunk of dense plain text glued together. That's why I'm trying to use more styles here. But I think I also need a better font and tweak other things such as spacing or colors to make it more visibly appealing.
