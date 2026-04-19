---
title: "The Current State of Software"
date: 2026-04-19T19:30:00+02:00
author: "Valentijn Harmers"
draft: false
showtoc: false
description: "Post discussing the current state of software."
categories: ["Technology"]
tags: ["software"]
cover:
  image: "posts/state_of_software/Keyboard.jpg"
  alt: "Keyboard"
  relative: true
  hidden: false
---

I was using my old Acer laptop, running Windows Vista recently. This device is my first ever laptop. It’s around 20 years old, but besides a heavily degraded battery, it’s still humming along just fine. The system is not connected to the internet and I mostly use it to play some old games.

While I was working on the laptop, I realized how responsive the system was. We often have memories of old tech being slow, but Windows Vista felt just as fast and snappy as my new Macbook Pro (pretty funny considering Windows Vista was considered bloated and slow at its time of release). Where did things go wrong? I asked myself. The answer to that question soon followed as I realized what this system was missing: an active internet connection.

## The internet
Going on the web used to be exiting. I still remember going to a website called [Speel Eiland](https://www.speeleiland.nl) to play games. The website still exists to this day, but many of the games have disappeared, because the Flash technology created by Adobe has since been discontinued.

You used to visit websites to enjoy their content, but now that content is buried behind tons of advertisements, auto-play videos, and animations. You can’t visit a news site without getting blasted by ads. You can’t even get to reading the article anymore. Using an Adblocker is a requirement for keeping your sanity these days.

Once you load a webpage, it isn’t unusual for more than 200 parties to start a bidding war for your attention right in your web browser. Your computer has to handle hundreds of connections, just to serve you a piece of text. It isn’t too strange for regular websites to take more than two seconds to load and download more than 30 Megabytes worth of data to your device.

That’s more than [15.000 pages of text](https://howbigisthis.com/?size=30+MB), just so you can read an article. For your information: this page you are reading right now is about 300 Kilobytes in size (around a 100 Kilobytes when you excude the cover image). That about 150 pages of text. Our devices haven’t become slower, the tech we use has been getting heavier to run, often with no benefit to us.

For some technologies like video streaming and online conference calls, the large data usage makes sense, but for other things it doesn’t. Sending an e-mail, chatting with someone, reading a news article, or ordering a pizza are not tasks that should require many resources.

## Web frameworks
Web frameworks are also something to look at when it comes to performance. You can divide a webpage into three parts: the HTML, which provides the content; the CSS, which provides the styling; and the JavaScript, which provides the interaction. In the past, most of the heavy lifting was done on the web server, which would dynamically render the content of each page and send it to the user. The web browser only had to show the user what it had received.

Over time, however, more and more of the work was done in the browser instead. JavaScript allows a developer to execute code in the browser of the user instead of on the server. This is useful for doing things like animations, but also allows for updating a small part of a webpage instead of requesting a whole new copy from the web server. This is very useful for things like real-time dashboards, where the JavaScript periodically fetches new data and adds it to the already existing data on the page, without the user needing to press the refresh button in their browser.

As more and more logic moved from the server into the browser, the Javascript codebases became more difficult to manage. Different frameworks popped up, aiming to solve these problems. The first of such frameworks, or more of a library, that I was introduced to was [jQuery](https://jquery.com/). This library made using Javascript less clunky. It simplified the selection of an element on the page, and made it easier to create animations and fetch new content.

Using jQuery is less relevant today, since modern JavaScript has improved to such a point that it is no longer necessary. Nevertheless, all kinds of new frameworks have emerged to solve some kind of problem with JavaScript. You have frameworks like React, Vue.js, Angular, and Svelte.

These frameworks promise to make it easier for developers by handling complex issues like state and event management. These frameworks do, however, add complexity to the website. A lot of functionality is abstracted away for the developer, and the website visitor won’t notice anything of their existence either, but the browser has to load, interpret, and execute all the instructions present in these frameworks.

This means that using something as React has a performance impact, especially when you add additional modules to that setup. This might be worth it, but it is at least something to take into consideration. Using frameworks has a cost that might not be worth paying.

As a developer, you are essentially adding something to your website that you do not fully understand and control. You also have to invest a considerable amount of time into learning to use your chosen framework, and there is no guarantee that it will be around for the years to come.

I had this happen to me with ‘Angular.js’. I had convinced my internship mentor that it was the right choice for the website that I needed to build. I put lots of work into learning it and ended up delivering the website. The framework was discontinued by Google a couple of years later.

I think that JavaScript frameworks are not worth it when you are building a website that serves mostly static content.

## From our local drives into the cloud
I am old enough to remember a time where all documents were saved to the local drive of your laptop or desktop computer. You were the one that was responsible for managing them. This meant that you had to organize your files in a folder structure that made sense and make backups regularly. This took some work, but it meant that you owned the files you had.

This started to change when services like Dropbox started popping up. Now you could upload your files to these services and they would keep them safe for you. You could even access them from multiple locations now. No need to burn files to a CD or copy them to a USB stick like some kind of caveman. This new way of doing things did introduce some problems, however. The biggest things on my mind are centered around Ownership, Fragmentation, and Accessibility.

### Ownership
The cloud might sound like some kind of fuzzy place, but it’s essentially just someone else’s computer. And this means you lose some control over your things when storing them there. You don’t fully own your files anymore. A service provider, like Dropbox, can prevent you from signing into your account and accessing your files.

There are enough stories on the internet where people ended up being locked out of their accounts because of some unforeseen event. It is therefore important to keep copies of your files in a place that you fully control, like your own computer. I also prefer to use services that use end-to-end encryption, so the service provider cannot snoop around in my personal files.

Also be wary of single sign-on options. I rarely use my Google account to sign into other services, and make an effort to create separate accounts for every service. Being fully independent from service providers is difficult, however. Especially when some of them make your data difficult to access.

Services like Dropbox are easy, since you have access to every individual file. But what about products like Milanote, Prezi, or Feedly, where it’s not simply file storage, but a software product? How can we get our data when it’s stored in a format that is out of our control? Luckily, the EU has stepped in on this one and made it mandatory for companies to supply you with the information that they have stored about you.

You can download an archive of your data and keep it as a backup. This is, however, still something that keeps me worried. I don’t like it when companies keep your data hostage. I would rather keep the data and run the software on my own system where it is under my control.

### Fragmentation
When using all of these cloud services, it can be difficult to keep track of where all of your stuff is. You have the majority of your game library on Steam, but also some on GOG and uPlay. Some of your files are in your Google Drive, but there are also some files in your Microsoft OneDrive. Your notes are in Milanote, and you also have some backups in Backblaze.

In the pre-cloud era, all of that stuff was just on your laptop. You had all your games on CDs and used a simple external hard drive for backups. I am not saying that all of this was ideal, but it was easier to oversee and manage.

### Accessibility
When you store your information on someone else’s system, you become reliant on them for accessing and manipulating that information. Your own system is fully committed to you. All of its processing power, memory, and storage capability is at your disposal. This is not the case in a cloud environment. You will have to share system capacity with all the other cloud users.

I came to realize this when Mozilla’s Pocket service got discontinued, and I had to look for a replacement. I ultimately settled for Goodlinks. One of the first things that I noticed after migrating was how fast things were. Looking something up in Pocket always felt slow; the performance of the servers wasn’t that great.

Goodlinks runs on my local machine and synchronises data between devices through iCloud. The searching for links is fast, since I have my devices all to myself. Ever since then, I have been looking to replace cloud solutions with alternatives which run locally. I have since then also replaced my RSS reader Feedly with Current Reader.

## Chromium everywhere
Different operating systems have different graphical toolkits. Windows has Winforms and WPF, macOS has Cocoa, and Linux systems have GTK and Qt. Besides that, you also have HTML and CSS for websites and mobile systems like Android. Those are loads of different systems! And you would have to make different versions of your application for all of them!

Developing and maintaining all of these different versions takes a lot of time and effort, so developers looked for other solutions. They came up with an ingenious idea: What if we make a website that looks like an application and run it in a web browser on the user’s device, and then we hide the top bar, and no one will be the wiser.

The one of the first of these solutions was Cordova (formerly known as PhoneGap). Developers would build their apps using web technologies, and their app would run in a Webview on the targeted device. This allowed developers to build apps for iOS, Android, and Windows Phone with a single codebase.

Then came Electron, which ships an instance of the Chromium Browser, the open-source version of Google Chrome, along with the website. This might all sound fine and dandy, but web browsers are not known for their small system footprint. These things love to eat up memory and processing power. Having to run 5 of these things, just to do basic system tasks, is silly.

Here is an example to prove my point. Rufus is a tool for creating bootable USB sticks. It only runs on Windows and is 2 Megabytes in size. Etcher is a similar cross-platform tool. It makes use of Electron, and the macOS version is almost 400 Megabytes in size. 400 Megabytes! Just to display some buttons. It’s baffling how little respect modern software developers seem to have for the available resources on the systems of their end users.

## Closing words
I had originally planned for this post to be a bit more structured, but I ended up dumping all of my grievances with modern software products in here. It’s not that I think that we should rewind the clock and go back to how things were in the past. I am, however, of the opinion that modern software solutions have poor performance and give users little control.

The best solution that I have seen is the applications in the Apple ecosystem. Within this ecosystem, applications run on the user’s system and store all their application state in iCloud. The state then syncs between all of your Apple devices.

I like this system, because application logic is executed on your own devices, ensuring good performance. Application state is also kept in a central location; there is no need to create different accounts for everything. The only disadvantage is that you now have a large dependency on Apple for storing your data.

It would be nice if we had a system where you could select your own data provider. This would be a platform where you can store your files and application data, and would also handle things like notifications. You can either choose a single data provider which you trust, spread your data among multiple providers, or be your own data provider by self-hosting.

It has been more popular to self-host Open Source solutions, in an attempt to get back control over one's own data. I’m, however, not convinced that this is the solution for the majority of people. The initial setup might be easy, but maintaining a collection of self-hosted solutions over time is a whole different matter. You will have to deal with things like backups, hardware failure, data migrations, certificate expiries, and updates. For most people, that’s too much effort.

I am convinced that it is possible to let companies handle the complicated stuff while providing users with the control they need. Sadly, companies are not incentivized to build their products in such a way, since harvesting user data and making them dependent on your product is too profitable. The users of these products are not aware that there is another way and simply accept things the way they are.

This all reminds me about a documentary that I watched some time ago. Its called ["Dodelijke Zorg"](https://www.npostart.nl/2doc/15-09-2022/KN_1727593) and is a Dutch documentary about software used by hospitals. The documentary describes a situation where hospitals are reliant on a single main supplier of software, and this supplier uses its position in the market to maximize profits at the cost of their customers. It shows you how important it is to have control over one's own data.

So, that's it. I think that I have made my standpoint clear here. Time to start working on a new post.
