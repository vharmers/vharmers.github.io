---
title: "The OpSec blog series - Introduction"
date: 2022-09-07T01:31:21+02:00
author: "Valentijn Harmers"
draft: false
description: "Introduction to the OpSec blog series"
categories: ["Technology", "OpSec Series"]
tags: ["opsec", "windows", "linux", "macos"]
---

Have you ever had the desire to improve the security of your systems but had no idea how to do it? You might have read all kinds of articles on the web about hacked companies that needed to pay large sums of money to get access to their data again. But what can you do, when you are just a system administrator of a small company with a non-existent security budget? Well, you can start reading the OpSec blog series in order to acquire the knowledge you need to make your environment more secure and give hackers a hard time.

My name is Valentijn Harmers and I have been working for Fox-IT/NCC Group as a DevOps Engineer for about 5 years now. Working at Fox has been a special experience. After finishing my Bachelors degree, I wanted to do something with software development, Linux and IT security. I went looking for a job but had a difficult time finding a job that had all 3 elements, but I was a greedy man and was committed to finding the perfect job for me. My job-seeking journey ended at Fox, where they were willing to start me off as a DevOps Engineer for the Threat Intelligence department.

I have done many different tasks over the years, but am currently specializing in cloud infrastructure and security. There is no particular grand idea behind this move. I just didn't like data-center visits, so moving my attention to the cloud made sense. I have always been interested in learning from others and have in turn been more than willing to share my own knowledge and experience. The OpSec blog series gives me the opportunity to share knowledge and experience among a larger audience.

So far the personal introduction. Let's get back on topic and discuss what this blogging series will look like. I will start off by explaining some general theoretical knowledge in order to lay down a foundation. I can then build the rest of the blog posts on top of it. Each post will cover a particular topic like chat communication, drive encryption or authentication. Large topics can be stretched over multiple blog posts. Each post would preferably contain a theoretical and a practical part.

I haven't decided on a definitive topic list yet, but I have the following topics in mind:

* Communication - PGP and SSL/TLS
* Communication - Secure chat applications
* Disk encryption
* Authentication - 2FA and MFA
* Authentication - Secrets Management
* Authentication - Going passwordless
* Infrastructure as Code - Ansible
* Infrastructure as Code - Git
* Asset/Vulnerability management

I think its also a good plan to set a scope for this blog series:

* We don't want the posts to be too difficult to follow. You should be fine if you can open up a command terminal or Powershell prompt and have some basic networking knowledge
* The posts will focus on small companies and individuals. All the introduced applications are free of charge and easy to set up, but might not scale well in enterprise environments
* I will write instructions for Microsoft Windows, Mac OS, Ubuntu and Fedora operating systems

{{< notice info >}}
These info blocks contain extra information which you are not required to know in order to understand the rest of the post. Feel free to skip them if you hate reading.
{{< /notice >}}

{{< notice warning >}}
I will use these warning blocks to warn you of potential adverse consequences.
{{< /notice >}}

## What is IT Security?

Let's talk about what IT Security actually is, or more how I see it. IT Security consists of two parts: Information Technology (IT) and Security. IT is all about technology, processes and people. Security is all about confidentiality, integrity and availability, which is also known as the CIA triad. Let's take some time to explain both of these terms.

Some sleazy salesman might have tried to convince you otherwise, but there is no magic software solution that will fix all of your problems and protect you from evil hackers. This is because every solution you deploy will need to be managed by people. And those people will need to have a process to follow in order to maintain the solution and respond to events in a uniform manner. You will need all three elements to be effective.

People who have followed any security certification such as (ISC)² CISSP, (ISC)² SSCP or CompTIA Security+ will know about the CIA triad. It is one of the first things they introduce you to. Confidentiality is about only sharing data with those who are allowed to have access to it. Integrity is about ensuring data is complete and accurate. And Availability is about ensuring data is accessible to those who need it in a timely fashion.

Those who have obtained the Systems Security Certified Practitioner (SSCP) certification will also be acquainted with the CIANA acronym. CIANA is CIA + Nonrepudiation and Authentication. Nonrepudiation prevents people from being able to deny something they have said. The easiest example of this is the use of signatures.

When you make a promise to someone, this promise can be written down in the form of a contract. Your signature on this contract proves that you know about the promise and are committed to keeping it. You cannot, later on, deny that you never knew about it and can be held accountable if you break the terms of the contract.

Authentication is the process of verifying that someone is who they claim to be. You take on an identity and supply proof that you are who you say you are. The identity is generally a username and the proof is a password, but there are also all kinds of other proofs you can use such as an OTP code or a fingerprint. Even things like body weight can be used as a proof. Authentication is something of great importance. Most breaches of security happen because of compromised credentials. Attackers find a way to login on a privileged account and take things from there.

This might be a lot of information to take in at once if you are new to the IT Security field. But just remember: IT Security is all about ensuring Confidentiality, Integrity, Availability, Nonrepudiation and Authentication (CIANA) and this is all achieved by Technology, Processes and People (TPP). There is also a longer version of CIANA which is CIANAPS where the P and S stand for Privacy and Safety, but I will leave it at CIANA for now. I can recommend the SSCP CBK (second edition) written by Mike Wills if you are interested in knowing more about CIANA and its practical application in IT Security.

## Why would you need IT Security?

Now we know what IT Security is, it's time to discuss why you would need it and how it contributes to the success of a company or your own private life. And to explain this one, I need to go back in the past. You see, went I was still a kid, I played a strategy game called "Stronghold". The game would give you a piece of land to build your hold on. You would start off with a 'lord's keep' and some resources such as wood, stone and food to get you started.

The goal of the game was to develop your economy and reach a certain goal such as "deliver 400 pieces of bread before the end of the year", but the game wouldn't make it easy for you. Enemy soldiers would periodically invade your land and try to destroy everything you have built. You could resist these attacks by building fortifications and recruiting soldiers, but this required resources produced by your economy. You needed stone or wood to create walls and you needed weapons and villagers to create troops. Economy and security were highly dependent on one another.

And the enemy soldiers weren't the only thing you had to worry about. There were also natural disasters such as famine and disease you had to deal with. Grain crops would fail, impacting your bread production or your cows would become sick preventing the production of cheese. Each one of these problems had the possibility of causing a chain reaction. A shortage of food made unhappy villagers. Unhappy villagers would eventually leave to find a better future elsewhere. Leaving villagers would lead to understaffing, which would cause parts of the production process to stop functioning, continuing the spiral of decline.

This game taught me a lot. Went I started out, I desperately tried to build a wall around all of my buildings. I didn't want to lose anything but ended up losing everything. The construction costs for the wall were too high and in situations where I actually managed to build it, I didn't have enough archers to defend all of it, leading to gaps in my defenses. I learned to layer my defenses. I would build a stone wall around my most important buildings and used a combination of wooden walls and watchtowers for the other buildings.

I would lose some farms and hunter shacks with every attack, but those were easily rebuilt. I would always keep some resources and jobless villagers on hand to compensate for these losses. At this point you might be thinking: "I thought this guy would explain why I needed IT Security, but all he does is talk about some game he played when he was a kid". You will need to read between the lines for this one. Replace the buildings with assets (such as servers, databases and printers), villagers with employees and soldiers with SOC analysts, security officers and security engineers and you have a company. A stone wall becomes a firewall and a watchtower becomes an Intrusion Detection System (IDS).

This game taught me that there is a delicate balance between acquiring new things and protecting what you already have. As long as you have something of value, there will be others who will want to take it away from you. And the easier you make it, the more tempted they will be to act on their desires. This doesn't mean you should be paranoid about security. You just need enough of it to not make it worth their while. You will need to ask yourself the question: "What am I or is my company worth?". And when answering this question, it is important to not only look at tangible things like laptops, servers and paper records but also at intangible assets like trade secrets.

When you know what you are worth, you can start protecting the things that are yours. You will have to make tough decisions on where to focus your defense. Ideally, you want to protect everything, but like in Stronghold, this is just not feasible. This doesn't mean you just "let it be". You should make plans about what to do if one of these assets is lost to you.

IT Security can be hard. You are trying to create a stable environment in a chaotic world. You feel like a shock absorber in a car. You take the pummeling from the outside world so the rest of the company can do what they do best. And the better the shock absorber functions, the smoother the ride will be.

## System setup

It is time to do something practical. We will install a package manager on our system. A package manager is an application that can be used to install, update and remove other applications (revered to as packages). Using a package manager over manually installing every application has several advantages:

* The applications are downloaded from a trusted source
* It's easy to keep all applications updated with the latest (security) patches
* It's quicker. I can install the Firefox web browser, GIMP and Libre Office on a Windows system with just one command: `choco install firefox gimp libreoffice`

Below you will see installation instructions for the different operating systems.

### Microsoft Windows

For Windows we are going to install the [Chocolatey](https://chocolatey.org) package manager.

**Step 1:** Open up an [administrative Powershell](https://www.howtogeek.com/742916/how-to-open-windows-powershell-as-an-admin-in-windows-10/) window

**Step 2:** Run the following command in the window:

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.
Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString
('https://community.chocolatey.org/install.ps1'))
```

**Step 3:** Ensure the application was installed successfully by running: `choco -?`

### macOS

For MacOS we are going to install the Homebrew package manager.

**Step 1:** Open up a Terminal window

**Step 2:** Run the following command in the window:
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

**Step 3:** Ensure the application was installed successfully by running: `brew --help`

**Step 4 (optional):** Disable telemetry by running the following command: `brew analytics off`

### Ubuntu/Fedora

Ubuntu and Fedora already have package managers of their own. There is no need to install anything for now.

## Closing remarks

This will be all for today. Take your time to process all the information I have given you. Don't forget to relax once in a while. Maybe play a game to take your mind off things. I will see you in the next post.
