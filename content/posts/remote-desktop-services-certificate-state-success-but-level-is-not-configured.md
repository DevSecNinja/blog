---
title: 'Remote Desktop Services - Certificate state ''success'' but level is ''not configured'''
date: 2015-02-19T19:56:00+00:00
draft: false
tags: ['Active Directory', 'ADCS', 'Certificates', 'Extended Validation', 'Microsoft', 'Remote Desktop Services', 'SSL']
description: ""
cover:
  image: ""
  alt: ""
---

I had a small issue with my Remote Desktop Services Lab environment. I wanted to add a by my PKI infrastructure signed certificate to the Remote Desktop Roles. I created a certificate template like in [this post](http://blogs.technet.com/b/askperf/archive/2014/01/24/certificate-requirements-for-windows-2008-r2-and-windows-2012-remote-desktop-services.aspx "Blog post").

When I was importing the certificates into the wizard, the certificate looks fine because the state after selecting the certificate says "Success".

![CertificateError](/images/2015/02/certificateerror.png) When you reopen the screen afterwards, it was like no certificate has been selected. I was able to see the certificate in my browser, so the selection was successful. I wasn't able to find out what was the problem on the internet, but I fixed it to change the certificate template.

In the "Subject Name" tab, make sure that the Subject name format is "DNS name" and under "Include this information in alternate subject name", "DNS name" is selected too.

That fixed it for me. [

![CertificateSuccess](/images/2015/02/certificatesuccess.png)](/images/2015/02/certificatesuccess.png)
