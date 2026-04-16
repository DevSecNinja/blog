---
title: 'Finding the Ultimate Password Manager'
date: 2020-01-05T09:00:00+00:00
draft: false
tags: ['1Password', 'Bitwarden', 'Dashlane', 'DevSecOps', 'LastPass', 'Password Manager', 'Passwords', 'Security']
description: ""
cover:
  image: ""
  alt: ""
---

**In this blog post, I wrote down my considerations & requirements around finding my next password manager. I've been a LastPass Family user for several years, but I am going to switch to a new password manager.

In 2015, LastPass was sold to LogMeIn.

It didn't feel good, but it wasn't a deal breaker for me.

Recent security issues issues like [this one](https://www.forbes.com/sites/daveywinder/2019/09/16/google-warns-lastpass-users-were-exposed-to-last-password-credential-leak/) or [this one](https://www.pcworld.com/article/3184153/lastpass-fixes-serious-password-leak-vulnerabilities.html) made me freak out a bit.

Last but not least, the parent company of LastPass - LogMeIn - sold itself to private equity firms.

That was it - I needed a new password manager and while I'm on this journey to find a new password manager, I'm sharing it with the rest of the world.** **I hope this blog post will help you in finding your ultimate password manager.**

## Requirements

LastPass offers a very rich feature set, so I wanted to make sure that I capture everything I want from a new password manager.

| Feature                                                   | Lastpass                    | 1Password                   | DashLane      | Bitwarden                                      |
| --------------------------------------------------------- | --------------------------- | --------------------------- | ------------- | ---------------------------------------------- |
| Password Generator                                        | X                           | X                           | X             | X                                              |
| Family package                                            | X                           | X                           | -             | X                                              |
| Share credentials with family                             | X                           | X                           | ~             | X                                              |
| MFA with YubiKey                                          | X                           | X                           | X             | X                                              |
| Emergency Access                                          | X                           | -                           | X             | -                                              |
| Store sites & notes                                       | X                           | X                           | X             | X                                              |
| Easy import from LastPass                                 | N/A                         | X                           | X             | X                                              |
| Stats about how safe my passwords are                     | X                           | X                           | X             | X                                              |
| iOS App, integration with autofill and with Touch/Face ID | X                           | X                           | X             | X                                              |
| MSFT Edge extension                                       | X                           | X                           | X             | X                                              |
| Servers hosted in Europe                                  | ~                           | X                           | X             | -                                              |
| Automatic password rotation                               | X                           | -                           | X             | -                                              |
| Easy-to-use password suggestions                          | X                           | X                           | X             | X                                              |
| Support easily accessible                                 | X                           | X                           | X             | X                                              |
| Detailed release notes are available                      | X                           | X                           | X             | X                                              |
| Remove account without contacting support                 | X                           | X                           | X             | X                                              |
| Price per month in EUR                                    | Premium: 2,67, Family: 3,56 | Premium: 2,65, Family: 4,75 | Premium: 3,33 | Premium: 0,74, Family: 0,90, Family Prem: 3,88 |

## LastPass

I've been a LastPass Premium/Family user for 5 years now and while I'm happy with their services, I also feel that they can do more on innovation and improving the product. The Edge Chromium extension isn't as stable as I would like to see and isn't as polished as 1Password.

You might have seen that the table above lists a `~` with the 'Servers hosted in Europe' requirement. LastPass offers the option to store your vault in Europe as [mentioned on their support page](https://support.logmeininc.com/lastpass/help/where-is-my-lastpass-enterprise-vault-data-stored). Account data will still be hosted in both the United States and Europe, but it isn't in a separate tenant like 1Password does. I will dive deeper into this in the next chapter.

## 1Password

### Stats about how safe my passwords are

The Watchtower feature gives you insights on the health of the items in the vault. It tells you when an account was registered at a compromised or insecure website. It will also tell you when you have expiring entities. Additionally, you can compare your passwords with the HaveIBeenPwned.com database to find out if you have any compromised accounts.

- ![](/images/2019/12/image-6.png)

- ![](/images/2019/12/image-7.png)

### Servers hosted in Europe

1Password offers their services in the US region with 1Password.com, 1Password.ca for Canada and in the Europe region with 1Password.eu. Right from the start you can register in a certain region which is completely separated from the other regions. Registering an account in the European region is a bit more expensive. With the currency rate today (27th of December, 2019), it's 29 euro cents more expensive to buy the Family plan with 1Password.eu: $ 4.99 vs € 4,75.

1Passwords [states that they are GDPR complian](https://1password.com/legal/gdpr/)t, which is something you don't see organizations mentioning often. Besides that, 1Password says that they are using the [Amazon AWS EU Frankfurt region based in Germany](https://discussions.agilebits.com/discussion/86340/questions-about-eu-server).

### Additional Pros

**Multiple Vaults**\
With LastPass I've used folders in the beginning but I mostly use the search function.

This now results in a completely uncategorized Password Manager.

Being able to create separate vaults with 1Password makes way more sense: one for private, one shared and one for work.

You can even mark a vault as 'Safe for Travel', so it will keep the vault on the device during travel.

One thing I would like to see from 1Password is adding additional controls to these vaults. E.g. accessing the Private vault requires re-authentication with a second factor. I see a lot of potential in this feature.

While it is possible to change the icons of the vault to easily identify a vault, I would have liked to see a possibility to select some standard icons.

**Lots of options while creating a new entry**\
I always liked the idea of using 'templates' before you create an entity in LastPass. When you are adding server credentials to your vault, it will show you a form with fields for the server name, username and password. 1Password has even more templates that you can use:

![](/images/2019/12/image-4.png)

There are also multiple fields (or labels) that you can configure when creating a new entity. With LastPass, I always ended up adding more details to the notes section, so I really like this approach. When compared to other password managers, 1Password does this really well:

![](/images/2019/12/image-5.png)

**Saving Multi-Factor Authentication codes in 1Password**\
This is a feature I'm not sure if I like it or not. One one hand, I think that it would stimulate users to activate multi-factor authentication on web sites, as 1Password will take care of filling in the one-time password. But on the other hand, Multi-Factor Authentication enforces a user to keep two things separate: something you know and something you have, for example. If you put all your eggs in 1Password's basket, a hacker only needs access to 1Password to compromise all your accounts.

An important thing to mention is that it doesn't seem to be possible to export your Multi-Factor Authentication entries (or 'seeds'). While you can easily export your passwords and notes to move to another password manager, this might result in a 1Password lock-in. If you often use Multi-Factor Authentication and you want to move to another password manager, you have to manually reconfigure tens or hundreds of seeds to your platform of choice. Something to think about...

### Things to improve for 1Password

**Multi-Factor Authentication during registration**\
Multi-Factor Authentication is such an important feature to prevent cyber criminals from stealing your secrets. I would have liked to see 1Password prompt me to configure MFA during the registration process, instead of doing it manually in the settings menu afterwards.

The bad thing is that it's even hidden under the menu item called "My Profile".

After opening your Profile, you have to click on the "More Actions" menu to get it configured.

Other password managers also don't prompt you actively to enable MFA, but 1Password makes it hard to find by hiding it in a dropdown menu:

![](/images/2019/12/image.png)

Hiding the Two-Factor Authentication Menu under More Actions

**YubiKey for Multi-Factor Authentication only available after configuring the Authenticator App**\
One of the first things I wanted to check out is the integration with [YubiKeys for Multi-Factor Authentication](https://support.1password.com/security-key/).

Unfortunately, this option wasn't available until I configured the authenticator app for Two-Factor Authentication.

The screen below will just show you the option to configure the Authenticator App, without mentioning anything about a YubiKey. I would be nice if the 1Password team can make this a greyed out option stating that the Authenticator App needs to be configured first.

![](/images/2019/12/image-2.png)

No option to configure YubiKeys

After setting up the Authenticator App as a second factor, the YubiKey setup was a breeze:

![](/images/2019/12/image-3.png)

**Emergency Access**\
One of the features I really like from LastPass is the emergency access feature. It feels way more comfortable that my family has access to my account when they need it. Especially in this digital day and age, someones online footprint is huge. Being able to provide access to my online accounts when I'm in an emergency feels good and also forces me to keep my vault organized.

1Password does have a feature to reset a family members password, but that still requires access to someone's email account. It's a nice feature to have when a team member forgets it's password, but it's not the same as emergency access. If you use this feature, make sure to select multiple family owners as owners can only reset passwords of members!

### Conclusion on 1Password

1Password overall feels pretty solid - a bit more polished when compared to LastPass. I really like the Watchtower feature to keep my passwords and other details 'healthy'. The lack of the emergency access feature is a deal breaker to me, especially with the higher price when compared to LastPass.

## Dashlane

Dashlane is, when compared to 1Password, rather vague about where the data is hosted. I found a [blog post](https://blog.dashlane.com/dashlane-tech-stack/) and [Subprocessor list](https://www.dashlane.com/privacy/subprocessor) stating that their web services and databases are hosted on Amazon Web Services in the Dublin (Ireland) region. I recommend Dashlane to mention this on a more prominent location.

While I expect that a Brexit won't change anything immediately with regards to data privacy, it's something to keep an eye out for.

After registering at Dashlane, I got prompted to download the Dashlane app instead of the browser extension.

When the Dashlane app was installing, I started to download the extension for Microsoft Edge (Chromium). I quickly realized that the app for Windows has way more functions when compared to the browser extension, as you can see below.

Also the app doesn't seem to scale correctly on a 4K screen. I really like the idea of being able to use the browser extension, so this is a dealbreaker to me:

![](/images/2019/12/image-10.png)

### Conclusion on Dashlane

After spending quite some time finding out where Dashlane is hosted and under which regulations they fall, I started to wonder why I have to do all that while 1Password just mentions it on [one of their pages](https://support.1password.com/regions/). After finding out that the Windows app has way more functionality than the extension and that there is no family plan, I started to look for other options.

On a positive note, I really like the direction that Dashlane is heading. Especially with support for Windows Hello to unlock your vault and for the fact that they include a VPN service with the premium option. If you're not looking for family features and don't mind using the Windows app, Dashlane is still a solid option.

## Bitwarden

### Use Command Line tools to access the vault

A feature I was really excited about is the command line support from Bitwarden. You can use this tool on several platforms to manage your vault. On Windows, you have to work with an executable called `bw.exe`, which you can use to login with `bw login <email> <password>`. With `bw list items` and `bw get` you can retrieve the objects available in the vault. If you have an organization account, you can use the RESTful API to manage your vault. Awesomeness!

![](/images/2020/01/image.png)

Use Command Line tools to access the Bitwarden vault - [Source](https://bitwarden.com/#download)

### Pricing

This was me, seeing the pricing of Bitwarden for the first time:

While other password managers are charging at least 2 or 3 euro's for premium, Bitwarden charges 74 euro cents per month! That's such a big difference I'm starting to wonder how Bitwarden can maintain the platform. But on the other hand, their Families and Teams pricing seems to be reasonable.

### Things to improve for Bitwarden

**Hosted Bitwarden in Europe region**\
Unfortunately, Bitwarden does not offer to host a vault in the Europe region, like 1Password and LastPass. Of course you can decide to host the free "self-hosted" installation of Bitwarden. Personally, I don't want to manage a critical service like a password manager. I think that organizations like Bitwarden, 1Password and LastPass are way more capable of doing that with dedicated operations teams.

**Emergency Access**\
Unfortunately, an Emergency Access for Bitwarden isn't available.

## Conclusion

All 4 Password Managers I've looked into are solid options. The basic features are all built-in, but features like Emergency Access and hosting in Europe can make a big difference.

I can really recommend to write down what you expect from a password manager and request a trial for at least 2 or 3 password managers. A password manager is a tool you use often and might use for the next couple of years.

### What am I going to do?

Personally I prefer what 1Password has to offer, except for the fact that they are missing an emergency access feature. When 1Password will offer that, I'm going to make the switch to the European version of 1Password.

> This blog post isn't sponsored and based on my opinion.
