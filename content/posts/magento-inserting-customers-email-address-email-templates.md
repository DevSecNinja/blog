---
title: 'Magento – Inserting the Customer’s Email Address into the Email Templates'
date: 2013-12-01T14:56:26+00:00
draft: false
tags: ['General']
description: ""
cover:
  image: ""
  alt: ""
---

A customer asked me to define the customer's email address in the order confirmation emails, sent out by Magento. You will have to edit or create a new template and add this shortcode:```
{{htmlescape var=$order.getCustomerEmail()}}

```This code will display the email address of the customer in the order emails. If you have any questions, let me know!
```
