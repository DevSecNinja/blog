---
title: 'Self-Hosted WordPress.org vs WordPress.com'
date: 2016-04-13T18:00:34+00:00
draft: false
tags: ['LetsEncrypt', 'Reviews', 'Self-Hosting', 'WordPress.com', 'WordPress.org']
aliases:
    - /2016/04/13/self-hosted-wordpress.org-vs-wordpress-com/
description: ""
cover:
  image: ""
  alt: ""
---

A couple of months ago I decided to migrate my blog from a self-hosted WordPress.org blog to WordPress.com. In this blog post, I'll tell you why I did that.

#### **No maintenance required**

A self-hosted WordPress.org installation needs maintenance. Plugins as well as the WordPress installation needs to be updated multiple times per month. I know there is an automatic update mechanism for WordPress which works fine for a basic installation of WordPress, but there is a chance that the upgrade will break your plugins and you have to restore a back-up to temporarily fix your website.

Now you can start troubleshooting what happened.

That brings us to another point and that is: keeping WordPress up and running with back-ups.

You have to restore a back-up every couple of weeks to check if your back-up still works.

You have to think about what happens with your blog if the server crashes or - even worse - if the datacenter is on fire.

#### **Plugins needed for a good WordPress.org installation**

Plugins are a great way to add functionality to WordPress. On my self-hosted blog, I had some SEO and Caching plugins active because WordPress is really slow without that.

Plugins can contain bugs as well and could possibly harm your blog.

With WordPress.com, your blog will be amazingly fast like mine is right now.

WordPress.com has some really good DDoS protection to protect your site when it's under attack.

By default, WordPress.com has some extra functionality.

Those features can be installed on a self-hosted WordPress.org installation too, by installing [WordPress JetPack](https://wordpress.org/plugins/jetpack/).

Because I build and maintain a lot of IT environments during work hours, I didn't want to maintain a blog and a web server in my spare time.

#### **Free SSL**

As of April 8th, all custom WordPress.com blogs are SSL protected by Let's Encrypt! I requested this feature a couple of months before the introduction, and I think that WordPress received a lot of those requests as well. Google will improve your ranking if your site is protected with SSL. This was one of the reasons for me not to migrate to WordPress.com before. It's nice to see all WordPress.com sites are SSL protected now!

#### **Pricing**

WordPress.com is free with a \*.wordpress.com domain (e.g. jvrtech.wordpress.com).

If you want a custom domain for your WordPress site, that starts at +/- $ 18 per year.

Don't forget to apply for the Privacy Protection for $ 8 per year as well, because this will hide your name in the WHOIS data of your domain.

This will protect you from getting a lot of spam from companies that want to maintain or design your website.

So that will cost you $ 26 per year in total.

That's like $ 2.16 per month.

It's amazingly fast, secure and requires no maintenance.

The downside of this is that your site will contain ads.

If you are just started blogging, that's fine.

If you want to remove those ads from your site, you can upgrade your plan to Premium.

That will cost you $99 per year, and includes the domain and Privacy Protection.

That's $ 8.25 per month.

Most web hosting companies will charge you like $ 3 per month for the hosting, $ 2 per month for the domain and $ 2 per month for the SSL certificate.

#### **Verdict**

##### **WordPress.com**

\+ No Maintenance needed. + It's requires little knowledge about hosting or setting up a domain. Your blog will be online within minutes. - No plugins can be installed. - No custom templates can be downloaded from the internet and installed, but you'll find some good free and paid templates in the WordPress.com store. WordPress.com will cost you $ 8.25 per month without ads.

##### WordPress.org (Self-Hosted)

\+ Highly customizable. You can make or install any plugins you want and change the lay-out to your needs. If you want a custom template, this is the way to go. + Can be cheap if you search for a cheap hosting company.

- Needs a caching solution.

- Needs maintenance and a back-up strategy.

- You need to know how to setup and maintan a WordPress site on a hosting platform. Hosting for WordPress.org will cost you around $ 5 - 10 per month and can be cheap if you buy hosting from a cheap hosting provider (not recommended) or can be quite expensive if you have a lot of page visits. Happy blogging! Let me know why you are using a self-hosted WordPress.org installation or WordPress.com in the comments section! _WordPress didn't pay me to write this blog post. It's just my opinion._
