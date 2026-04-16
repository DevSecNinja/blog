---
title: 'Let''s Encrypt leaks 3.125 email addresses'
date: 2016-06-11T07:51:45+00:00
draft: false
tags: ['Let''s Encrypt', 'Security', 'SSL Certificates']
aliases:
    - /2016/06/11/lets-encrypt-leaks-3-125-email-addresses/
description: ""
cover:
  image: ""
  alt: ""
---

First of all, I absolutely love Let's Encrypt. It's a very easy way to protect a website.

All [WordPress.com websites are protected](http://cloudenius.com/2016/04/09/https-everywhere-encryption-for-all-wordpress-com-sites/) with an SSL certificate from Let's Encrypt as well. I received an e-mail this morning from Let's Encrypt about their new Subscriber Agreement.

Above the message, there is a big list with 3.125 e-mail addresses including my own e-mail address.

Looks like they forgot to put those email addresses in the BCC of the email.

The e-mail was sent from the Let's Encrypt mailservers because the SPF record is valid: **Authentication-Results: spf=pass (sender IP is 198.2.180.10) smtp.mailfrom=mandrillapp.com;**

> Dear Let's Encrypt Subscriber, We're writing to let you know that we are updating the Let's Encrypt Subscriber Agreement, effective June 30, 2016. You can find the updated agreement (v1.1) as well as the current agreement (v1.0.1) in the "Let's Encrypt Subscriber Agreement" section of the following page: https://letsencrypt.org/repository/ Thank you for helping to secure the Web by using Let's Encrypt.

We're talking about a Certificate Authority here! Hopefully they'll protect the SSL certificates in a better way. **UPDATE**: [Official statement from Let's Encrypt](https://community.letsencrypt.org/t/email-address-disclosures-preliminary-report-june-11-2016/16867).
