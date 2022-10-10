---
title: "Creating a digital life raft"
date: 2022-09-09T17:40:52+02:00
author: "Valentijn Harmers"
draft: false
description: "Learn how to create a digital life raft to use in emergencies"
categories: ["Technology"]
tags: ["opsec", "macos", "windows", "linux"]
cover:
  image: "posts/life_raft/beach.png"
  alt: "Beach"
  caption: "Image by [Cris Ramos](https://pixabay.com/nl/users/cris00001-4795139/?utm_source=link-attribution&amp;utm_medium=referral&amp;utm_campaign=image&amp;utm_content=2245049) from [Pixabay](https://pixabay.com/nl//?utm_source=link-attribution&amp;utm_medium=referral&amp;utm_campaign=image&amp;utm_content=2245049)"
  relative: true
  hidden: false
---

Over the span of our lives, we accumulate a lot of stuff. Some of this stuff is precious to us so we keep it in a secure place like a safe or strongbox. Some of this precious stuff can also be digital and therefore must be secured into digital strongboxes and safes but what happens when you lose the key?

When your work in IT, you have a minimum of two employers: the company you work for and your family. I am the designated IT support and data custodian at home. It’s my job to keep all family pictures and other important files complete and available. And after going through the experience of losing my pictures of our vacation trip to Paris years ago, I am next to paranoid when it comes to making backups.

I have around 8 copies of all important data. I keep backups on laptops, external drives and 3 different cloud storage providers, but there is one little problem: it’s all encrypted. My greatest fear, apart from being randomly attacked by apes, is that I somehow lose access to the encryption keys.

Like a good boy, I store all my passwords in a password manager, but what if I forget the master password?  You know that thing when you type a password so often it becomes muscle memory but then you forget the actual password? And then you can’t type it anymore when you realize that you forgot it? Truly the stuff of nightmares.

And how will my family be able to access the data if something happens to me? I could easily be abducted by aliens, isekaied to another world or ascend to another plane of existence by accident.

I therefore came up with a system that allows me or my family members to access my password database in case of emergency. And no it doesn’t involve just giving my parents a written copy of my master password because that would be too easy.

The first step would be to collect copies of all the necessary files you want to put in your “digital life raft”. Put them all in one folder.

Then we use an application such as [7-Zip](https://www.7-zip.org) to create a password protected archive from the folder. Windows users can download the installer from the [7-Zip website](https://www.7-zip.org/download.html). MacOS users can use [Keka](https://www.keka.io/en/) instead. You are free to use something else if you want.

Now it’s time to add the magic sauce. We are going to split the archive password into multiple parts using [Shamir’s Secret Sharing](https://en.wikipedia.org/wiki/Shamir%27s_Secret_Sharing) (SSS). The idea behind SSS is that you can split a given secret into an X amount of shares. Reconstructing the secret requires an Y amount of those shares (where Y <= X of course).

You can use the following [website](https://iancoleman.io/shamir/) to split your password into parts and combine those parts to reconstruct the password. You can save the page as an HTML file to your computer if you want to use it offline.

It is recommended to build the page from source. You will need Git and Python3 installed on your system. These are the steps you need to take:

```bash
git clone https://github.com/iancoleman/shamir.git/
cd shamir
python3 ./compile.py
```
Then you can open the file called `shamir-standalone.html` with your browser. There is also an older alternative called [PassGuardian](http://passguardian.com) you can take a look at.

Both of these websites use the [secrets.js](https://github.com/grempe/secrets.js) Javascript library, which is an implementation of SSS. The library has been audited in 2019. You can read the audit report over [here](https://github.com/grempe/secrets.js/blob/master/audit/SLA-01-report.pdf) if it makes you feel better.

![Gandi Quote](crypto_gandi.jpg)

{{< notice info >}}
There is also a [command line implementation](http://point-at-infinity.org/ssss/) for Unix/Linux systems. On Debian, you can install it with the following command `apt-get install ssss`. It is also available for macOS through [Homebrew](https://brew.sh). You can install it with `brew install ssss`.  Use the `ssss-split` and `ssss-combine` commands to create and combine the shares.
{{< /notice >}}

Once you have created the shares and distributed them to your family members and trusted friends, you still have to store your archive somewhere safe. I would recommend you store it on a read-only medium. Don’t use USB sticks since the data on them can easily get corrupted or deleted by accident. Burn the archive to a CD or store it on an SD card (don’t forget to put it in read-only mode by flipping the switch on the side).

It’s also not a bad idea to include a copy of the needed software and instructions. You can get a portable version of 7-Zip over [here](https://portableapps.com/apps/utilities/7-zip_portable).
