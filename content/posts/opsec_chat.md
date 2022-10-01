---
title: "The OpSec blog series - Chat platforms"
date: 2022-10-01T02:18:38+02:00
author: "Valentijn Harmers"
draft: false
showtoc: true
description: "The third post in the OpSec series covering Chat Platforms"
categories: ["Technology", "OpSec Series"]
tags: ["opsec"]
cover:
  image: "posts/opsec_chat/chat.jpg"
  alt: "chat"
  caption: "Image by [Shabaz khan](ttps://pixabay.com/nl/users/siez18-1400060/?utm_source=link-attribution&amp;utm_medium=referral&amp;utm_campaign=image&amp;utm_content=2281309) from [Pixabay](https://pixabay.com/nl//?utm_source=link-attribution&amp;utm_medium=referral&amp;utm_campaign=image&amp;utm_content=2281309)"
  relative: true
  hidden: false
---

*This post is part of a larger series. You can find all posts over [here]({{< ref "/categories/opsec-series">}})*

Hello and welcome to a new blog post in the OpSec blog series. As already mentioned in the [previous post]({{< ref "opsec_mail" >}}), this one will be about chat platforms.

I can still remember a time when I was in school and carried around a Sony Ericsson J110 dumb phone. I didn't use it much. It was just for contacting my parents in case of emergencies. All the cool kids in my class had these BlackBerry devices and they used an application called BlackBerry Messenger (BBM) to send messages to each other. I was told that it was cheaper to use BBM than to send messages over SMS.

Although I never used BBM personally, it was the first time I came into contact with a chat platform. The first platform that I actually used was Skype (I know it's more of a video conferencing platform, but it also has chat functionality). I got introduced to WhatsApp when I got my first smartphone which was a Samsung Galaxy Gio. It was the first time I could send messages from my phone without worrying about costs. I had a pre-paid SIM card and sending an SMS was still quite expensive back then.

I have experimented with many chat platforms throughout the years but always had to put in a great amount of effort to persuade others to make the switch. Chatting with yourself is not a lot of fun after all. Different chat platforms target different audiences. Teams targets business users while Telegram has become more of a social media. I will be focusing on the more security-focused chat platforms.

I have picked four platforms that I will compare to each other. I will promise that this will be an honest comparison without any bias towards any of them ... Ah, who am I kidding. I will obviously use this opportunity to praise my two favorite platforms and hate on the two I am forced to use. Here we go!

## The rating system
I would like to base the ratings on the CIA triad, but I will add the letters 'A' and 'P'. The A stands for Authentication and the P stands for Privacy. This is what it is going to look like:

* **Confidentially;** Indicates how good the chat platform is in keeping things secret. Chat messages should only be accessible to those who are part of the conversation
* **Integrity and Availability;** I have combined these two into one rating. Here we will determine how good a chat platform is in keeping chat records complete and available
* **Authentication and Trust;** Indicates how well the platform authenticates its users. Strong authentication controls make it difficult for attackers to impersonate others and gain access to conversation history. I have also sneaked user trust in here because it is heavily related to authentication. Users will need the ability to be sure that they are actually communicating with the right person. Authentication is about proving that you are the owner of a particular account and user trust is about proving that a particular account belongs to you
* **Privacy;** Here we focus on how much of your personal data you need to supply to the platform in order to participate. We also take a look at what the platform is allowed to do with your data

Each rating will be assigned one of the following scores: terrible, bad, neutral, good or excellent. The platforms that I have chosen to compare are Keybase, Matrix (Element), WhatsApp and Signal. All these platforms have a security/privacy focus (or at least had this focus in the past).

### The baseline
The neutral score is used as a baseline. The criteria for the baseline are based on what the average chat platform has to offer. If one of our reviewed platforms performs significantly better than the baseline then it will get a ‘good’ or ‘excellent’ rating. I will give it a ‘bad’ or ‘terrible’ rating when it performs worse than the baseline.

Here are the criteria:

* **Confidentiality;** The platform secures the connection between client and server with something like TLS. End-to-end encryption is offered optionally
* **Integrity and Availability;** Integrity of messages is ensured by comparing checksums. Users can access their data from multiple devices
* **Authentication and Trust;** The user has to sign in with a username and password. Two-factor authentication is optionally provided, but is not enabled by default
* **Privacy;** The platform collects some basic personal information like your name, e-mail address and phone number. The data is not shared with other third parties for advertising purposes. The user has the ability to close down their account (the right to be forgotten)

**Start warning:** These criteria are not based on some research article but on what makes the most sense to me personally.
**End warning**

## The rating
Now the rating will finally commence. Every platform will have its own section, except WhatsApp and Signal since they are very similar to each other. I have also added sections where I share my personal experiences and thoughts. These sections will however not be part of the review process.

### Keybase
[Keybase](https://keybase.io/) is an end-to-end encrypted messaging and file-sharing service. It was created by Chris Coyne and Max Krohn (and others) and started off in 2014 according to its [Wikipedia](https://en.wikipedia.org/wiki/Keybase) page. Keybase focuses on security and functionality. It offers a wide array of services such as:

* 	One-to-one messaging
* 	Group chats (revered to as ‘Teams’)
* 	Big Teams (multiple chat channels in a single group)
* 	File sharing
* 	Stellar crypto wallet integration
* 	The ability securely encrypt and sign data and transfer it through a different channel. You can generate encrypted and/or singed "blocks" which can be pasted in an e-mail or posted on a website just like with PGP
* 	Encrypted git repository hosting
* 	The ability to map social media accounts to your Keybase identity
* 	Command line support for those super hackers out there who can't be bothered to leave the comfort of their glorious terminal window to use a filthy GUI application

#### Confidentiality
Keybase started off using PGP but later moved to the [NaCL](http://nacl.cr.yp.to) (pronounced as 'salt') library. All communications are end-to-end encrypted and Keybase also offers Forward Secrecy (FS). FS allows the use of throwaway keys for the encryption of messages. These keys are deleted after a certain period of time and ensure messages cannot be decrypted even when the main key has been compromised.

Forward Secrecy is only used for what is referred to as exploding messages. These are messages that get deleted after a pre-configured period of time. Keybase is not the only service to offer FS, Signal has it too for example. There is however something interesting about the implementation of Keybase.

The key used to encrypt these exploding messages only gets rotated on a daily basis, while other implementations rotate the key for every message. [According to their documentation](https://book.keybase.io/docs/chat/ephemeral), they do this because they want to ensure good performance even in large groups. The complexity of the Keybase system was another reason that was mentioned.

The decision to store user data on their own servers does score them points on availability, but a system where messages are only stored until they can be safely delivered does provide better confidentiality. I have also taken their FS implementation into account and have decided to give Keybase a 'good' rating on confidentiality.

Keybase has also been audited by the colleagues of NCC Group in 2019. The audit report has been made publicly available and can be found over [here](https://keybase.io/docs-assets/blog/NCC_Group_Keybase_KB2018_Public_Report_2019-02-27_v1.3.pdf).

#### Integrity and Availability
All messages and files in Keybase are digitally signed which ensures integrity. All data is also stored on the servers of Keybase which ensures availability even then you lose access to all of your devices, but you do need a copy of your encryption key.

The platform also has multi-device support, which means you can chat with multiple devices at the same time. This allows you to pick up where you left off on another device if your current device gets eaten by a crocodile or something.

Keybase has applications available for Android and iOS, but also for Windows, macOS, Debian, Ubuntu, Fedora and Arch Linux. This also makes the platform more approachable for people who don't have a smartphone for example.

Most of the data generated by the platform is not kept in a normal database on a server, but published on a ‘signature chain’. All the data on this chain is immutable and can therefore not be changed without invalidating the whole chain. This ensures data integrity even when the server has been compromised.

A hash of each signature chain (every account has its own), is periodically stored on the Bitcoin blockchain. This essentially allows the Keybase servers to check if any of the signature chains have been tampered with.

Keybase allows you to store files in what they call the Keybase FileSystem (KBFS). Every user gets a private and a public folder. The private folder is for storing your private stuff, which is only accessible to you, and the public folder is accessible to everyone. Every team also has its own folder and you can also create shared folders with others.

KBFS works a bit differently than what you may be used to. Services like Dropbox, Google Drive and Mega synchronize your files to a folder on your system. KBFS however presents itself as a separate filesystem on your OS. Files are downloaded and decrypted on the fly when you access them.

When using it, I have noticed that especially uploading files can be quite slow. The encryption process also takes a considerable amount of computing resources. It is also important to know that this feature is still in beta. Keeping copies of your important files would therefore not be a bad idea.

I am giving Keybase an ‘excellent’ rating for Integrity and Availability since all your chat conversations are available to you on any device at any time. Their signature chain solution also ensures the integrity of user data even when the server is compromised.

#### Authentication and Trust
Keybase has an interesting authentication model. You start with picking a username and configuring a password. You then install and configure the app on one of your devices and start chatting away.

There is only one thing that is important to understand. Your login credentials can only be used for administrative actions like changing your email address, adding a profile picture or following others. It does not allow you to use the chat functionality nor does it allow you to access any of your files.

The key used for encrypting and decrypting files and chat messages is only stored on your devices. A new device has to be authorized by an existing device. You also have the option to create a paper key (referred to as a couch key in Keybase). This key is supposed to be stored in a safe place and used as a backup if you lose access to all of your devices.

In the event that you lose access to all your devices and your paper key backup, Keybase allows you to reset your account from the web interface (as a logged-in user). This will however mean that you lose access to your files and chat history. You essentially start over from nothing.

Further hardening is possible by enabling ‘Lockdown mode’. Enabling this option essentially makes your password worthless since all actions through the web interface are disabled. You can only make changes to your account from your devices. You will be completely locked out of your account when you lose access to all of them (and the backup key). This feature will however make it very difficult for hackers to access your account since they will now need access to your devices.

Apart from tying devices to a user, Keybase also allows users to create trust relationships with each other. The platform uses a “web of trust” model. Users can follow each other just like they would on social media platforms such as Twitter.

Keybase even goes a step further. It also you to connect your other social media accounts to your Keybase account, expanding the web of trust beyond the bounds of the platform.

Authentication and trust is where Keybase shines. Its advanced authentication features in combination with its web of trust earn it a well-deserved ‘excellent’ rating.

#### Privacy
{{< notice warning >}}
I am not a lawyer or someone who is certified to give legal advice. I will try to summarize the privacy policies of the to be reviewed products and services to the best of my ability, but cannot guarantee that I won’t make any mistakes while trying to understand, simplify and summarize the text.

Basically, when stuff gets serious, don’t rely on advice from some dude on the internet. You can quote me on that one!
{{< /notice >}}

Keybase has a pretty clean and easy to understand [Privacy Policy](https://keybase.io/docs/privacypolicy). Here is a summary of what is collected:

* Account info: This covers things like your name, avatar picture, e-mail address and information about the social media accounts you have linked to your profile
* Files and Data: All your files and chat messages are stored on the servers of Keybase in an encrypted format
* Account activity: Essentially a record of things you do in Keybase. Examples of this include editing account information, following other users and linking other social media accounts to your Keybase profile

The Keybase server infrastructure is hosted in the U.S. This means they have to comply with U.S. laws and regulations. The data of EU citizens is transferred and stored under the Privacy Shield Framework.

You also have to understand that certain actions are recorded on a signature chain. And once it’s on the chain, it can never come off. You can decide to follow someone and later change your mind and unfollow them, but a record of your actions will always remain.

Your account’s signature chain is publicly accessible by anyone. This is so anyone can verify the integrity of the web of trust.

Keybase only collects what is necessary for their service to function and is clear about what they collect. They will therefore receive a ‘good’ rating. I have not given them an excellent rating because users do not have control over where their data is stored. The U.S. also isn’t known for its good privacy laws.

{{< notice info >}}
Some of you might be confused why I gave Keybase a high rating on privacy because the company is in the hands of Zoom now. I have rated Keybase on its current situation and not a possible future one.

The point is that Keybase is not allowed to grant its parent company access to its user data under the current privacy policy. This might happen in the future, but Keybase would have to update its privacy policy and notify its users of the change first. You also always have the possibility to close your account if that ever happens.
{{< /notice >}}

#### Personal input
Keybase contains all the features I would ever dream of. Solid multi-device support, no worries about data backups and an easy to use web of trust. The thing is however that it is mostly targeted at geeks (Geekbase would be a more fitting name). What is a regular user going to do with a crypto wallet and encrypted Git repositories?

Keybase is also the only reviewed chat platform that doesn’t support video calling. It does however allow you to intergrade with Google Meet or Zoom by using bots.

I think one of the most important things left to tell you is that Keybase has been acquired by Zoom in 2020. Both Keybase and Zoom have published blog posts where they announce the acquisition (you can read them for yourself over [here](https://keybase.io/blog/keybase-joins-zoom) and [here](https://blog.zoom.us/zoom-acquires-keybase-and-announces-goal-of-developing-the-most-broadly-used-enterprise-end-to-end-encryption-offering/).

The plan is to integrate much of the functionality built for Keybase into Zoom. Zoom obviously wants to improve the security and privacy of its product after facing harsh scrutiny from IT security professionals at the start of the pandemic. I think its safe to say that Keybase is end of life. We are all just waiting for the termination notice at this point.

I however did decide to include Keybase in this review since I do envoy the service and am impressed by how knowledgeable the people at Keybase are. I enjoyed reading their blogs and documentation. I especially liked that they explained why they were making certain design decisions and what kind of factors they were taking into account. I will certainly miss it when it stops.

### Matrix
Matrix is a real-time communication protocol. The protocol is part of an open standard. The aim of the protocol is to make real-time communication work seamlessly between different service providers. It essentially wants to be the e-mail equivalent for chat communications.

The protocol has been in development since 2014 but is only out of beta since 2019. The development is overseen by The Matrix.org Foundation. Apart from developing the protocol, the foundation has released a server implementation called Synapse but is working on a new implementation called Dendrite.

The protocol was originally developed by New Vector Ltd before the ownership moved over to the Matrix Foundation. New Vector does however still take care of the development of the client implementation called Element (formally known as Riot Chat).

With Matrix, users are free to choose their own service provider and client application. This is a very big deal since most chat platforms give you no choice in the matter. At the moment of writing, Matrix itself is the biggest provider but more should emerge as the protocol becomes more popular. A lot of people and companies also set up their own server essentially becoming their own providers.

Matrix has become quite popular in Open Source communities and governments. Different projects like KDE, Jellyfin and Mozilla call Matrix their home. The [German army (Bundeswehr)](https://element.io/case-studies/bundeswehr) and [national healthcare system](https://matrix.org/blog/2021/07/21/germanys-national-healthcare-system-adopts-matrix) use Matrix to communicate internally. I also read [this](https://hermannschule.de/hermannpost.html) article about a school that started using Matrix to facilitate communications between students, teachers and parents.

Here follows a quick summary of the features of Matrix:

* One-on-one chats
* Group chats (revered to as ‘Rooms’). Rooms can be either public or private
* Video conferencing (by using [Jitsi Meet](https://meet.jit.si))
* Support for End-to-end encryption
* Multi-device support
* Choice between different chat clients such as [Element](https://element.io), [Fluffy Chat](https://fluffychat.im) or [Fractal](https://wiki.gnome.org/Apps/Fractal)
* You can choose your own provider and even host your own server if you want to. A server running the Matrix server application is revered to as a ’Home server’

#### Confidentiality
Matrix uses its own crypto library called [Olm](https://gitlab.matrix.org/matrix-org/olm). Olm is an implementation of the [Double Ratchet Algorithm](https://signal.org/docs/specifications/doubleratchet/). This Algorithm was developed by Open Wispher Systems in 2013. This company was also responsible for the development of the Signal chat messenger and the Signal protocol.

Curve25519 key pairs are used to establish a shared secret between two parties who want to communicate with each other. This secret is then used to establish the Double Ratchet session.

{{< notice warning >}}
I will explain more about Double Ratchet when we come to the review of WhatsApp and Signal. For now, you just need to know that it is an algorithm that supplies Forward Secrecy.
{{< /notice >}}

Matrix uses the Megolm Group Ratchet for encrypting group messages. This algorithm is more suited for sending messages to a large group of people. It is however not as secure as the Double Ratchet, since it only provides Partial Forward Secrecy. Some confidentiality is exchanged for performance in this situation. It allows Matrix to have rooms with thousands of members.

All chat messages are stored on the servers of the chosen service provider. The chat history is kept indefinitely by default, but there is also experimental support for [Retention Policies](https://github.com/matrix-org/synapse/blob/develop/docs/message_retention_policies.md).

A Matrix server can be federated with other servers, but can also run perfectly fine on its own. You can even have a closed-off network of federated servers that are not connected to the main network on the internet. This is the main reason why governments have taken a great interest in Matrix.

Solid encryption, Retention Policies and private hosting earn Matrix an ‘excellent’ rating on confidentiality.

#### Integrity and Availability
The thing that makes Matrix special is the fact that there is no ‘main’ server. The network consists out of a collection of federated servers that are located all over the world. This makes the network as a whole practically impossible to take down.

Matrix also supports the use of multiple devices. This allows users to switch to a different device when their current device fails. Clients exist for just about any OS. I wouldn’t be surprised if someone created a client implementation for a smart fridge or something.

I have given Matrix an ‘excellent’ rating on Integrity and Availability.

#### Authentication and Trust
The authentication system of Matrix works in a similar way to the system Keybase uses. You protect your account with a password and your chat history is encrypted with an encryption key. Even when an attacker manages to get into your account, they will not be able to read your chat history. You can decrypt your chat history from another device by using a feature called “Cross singing”.

And before I explain what this feature entails, I will have to explain the basics first:

* Every device that is logged in on your account has its own encryption key
* When Bob and Alice start a chat, their devices will all exchange keys
* When Alice sends a message from one of her devices, this message will be encrypted and sent to all other devices participating in the chat

This explains the encryption part but how does Alice know that all Bob’s devices are actually controlled by Bob? Matrix gives users the ability to verify each other’s devices. Alice and Bob can meet up in person and verify their devices by means of a verification process. This process requires them to compare public key fingerprints which are often displayed as QR codes.

But what happens if Bob buys a new phone? Normally Alice and Bob would have to meet again and verify Bob’s new device. This isn’t needed anymore with Cross-Singing enabled.

With Cross-Singing, both Bob and Alice will generate a Master key. This key can then be used to certify the owner’s devices and the master keys of other users (Note: I simplified things here a bit; the real situation is a bit more complex). So whenever Bob has a new device, he just certifies his new device with his Master key (by using one of his existing devices). And since Alice trusts Bob’s Master key, she will also trust his new device.

Bob’s new device will now also be trusted by his other devices. This is important since it allows the new device to retrieve the encryption key used for historical chat messages from Bob’s other devices.

Matrix also gives you the option to store your Master key and other important key material on the server as an encrypted backup. The backup is protected by password that is chosen by the user or randomly generated on the device. This password should not the same as your account password. This would allow you to certify a new device even when you don’t have any of your other devices on hand.

Keybase essentially does a similar thing but in Keybase it is more abstracted away. There is also one major difference between the implementation in Keybase and Matrix. Device certification is mandatory in Keybase but optional in Matrix.

{{< notice warning >}}
You might have noticed that I use the words “verify” and “certify” a lot and you might assume they mean the same thing. There is a difference between the two, however. To verify a key means that you check if the public key you have matches the public key of your partner. A certification process also produces “formal proof”.

This proof usually involves the process of using your private key to sign the public key of the person who is to be certified. The proof can then be shared with others. In OpenPGP, these proofs are published on a key server; with TLS you will get this proof in the form of a certificate; Matrix clients publish proofs on the server and Keybase publishes all proofs on the Signature Chain. You can compare it with a situation where you get a proof of attendance in the form of a paper certificate or badge after attending a course or seminar.

The difference between the two is important. Certification provides nonrepudiation, verification does not. You can always deny that the verification ever happened. Certification cannot be denied afterwards because a proof is created.

Note that Matrix and Element use the term ‘verify’ while it is actually a certification process since a proof in the form of a digital signature is created.
{{< /notice >}}

It is also important to know that Cross-Signing only protects the confidentiality of historical chat messages and nothing else. Matrix doesn’t have a lockdown mode as Keybase has.

A hacker, let’s call him Jack, who has gained access to Bob’s account can still listen in on the conversation between Bob and Alice. This is because devices will also send new chat messages to unverified devices (at least with the Element clients).

You can however disable this behavior by going into: user settings -> security -> advanced -> never send messages to unverified sessions -> enable. This will however require you to also verify your chat partners before being able to send messages to them.

Jack can also communicate with Alice through Bob’s account but Alice will be able to see that these messages are coming from an unverified device.

Here is a screenshot of what that would look like:

![](matrix.png)

As usual, the interface language is in Dutch but I will explain what is happening here. Every user has a little shield in front of their name. The shield is black by default but turns green when you have certified the user (which involves meeting up in person and scanning QR codes). The shield will turn red when an uncertified device joins the chat.

The screenshot above clearly shows the red shield next to my name. The popup shows that I have three devices. Two of them are certified and one called “Tablet” is marked as untrusted because it hasn’t been certified.

Within Matrix, it is only possible to create one-on-one trust relationships. This means that if four people want to have a conversation, six certifications need to happen before all of them trust each other. You can calculate this with the following formula: `N(N - 1)/2`  where N is the number of participants. So when you have a chat room with 50 members, `50(50 - 1)/2 = 1225` certifications have to take place before all members have trust relationships with each other.

It is safe to say that one-on-one trust relationships don’t scale well. It is doable with a small group of friends or family, but not with a larger group of people. This scaling problem is usually solved by using either a web or chain of trust. There is a [proposal](https://github.com/matrix-org/matrix-spec-proposals/pull/2882) for adding a web of trust to Matrix, so we might see it in the future.

I have given Matrix a ‘good’ rating on Authentication and Trust. It didn’t get an ‘excellent’ rating because of the trust scaling problem.

#### Privacy
The [privacy policy](https://matrix.org/legal/privacy-notice) of the Matrix.org server can be summarized in the following points:

* The following account information is collected:
	* Username
	* Password (stored as a hash)
	* Display Name (if you configured one)
	* Your e-mail address
	* Your phone number (if you choose to provide it)
* You can close your account and have to right to be forgotten:
	* Messages only accessible to your account will be deleted from the server within 30 days
	* Users you have already communicated with will get to keep their copy of the conversation history
	* New members who have joined a room will not be able to access your past messages (existing members will get to keep their copy of your messages though)
* The foundation uses a combination of Third Party hosting services namely: UpCloud, Mythic Beats and Amazon Web Services
* Application data logs, which include username, user IP and user agent, are kept for no longer than 180 days
* There is no mention of where the server running the Matrix Home Server is located. Their privacy policy is based around GDPR and in the section “Transfers of your Data”, it is stated that data will be transmitted to other Home Servers outside of the EU. This hints that their own Home Server is inside of the EU, but I am just making an assumption here.

But that’s just the privacy policy of the most popular server. There are many other servers out there. You can find a list [here](https://joinmatrix.org/servers/). You can also host your own server. [This](https://theselfhostingblog.com/posts/self-hosting-your-own-matrix-server-on-a-raspberry-pi/) guide explains how to do it on a Raspberry Pi.

It is furthermore important to know that having control over all of your data can be difficult. As mentioned in one of the points above, your provider will try to delete your messages from rooms if you request to be forgotten. Those rooms can however be located on other servers that are not under the control of your provider. Your provider will pass your request to be forgotten on to other servers, but it is up to them to actually delete your data.

I have decided to give Matrix an ‘excellent’ rating on Privacy. No other chat platform allows you to choose whom to entrust with your personal information.

#### Personal input
Matrix solves one big problem I have been having with chat platforms. It’s the problem where you are forced to use the chat platform that your friends and colleagues use. You need to use the client that is provided by the platform, you need to have an OS that they support and you have to store your data on their servers.

Matrix allows everyone to participate. There are different clients to choose from and even different server implementations. It doesn’t matter if you are on Android, iOS, macOS, Windows or some Linux distro. There will be a suitable client for you. You can even create one yourself if you have the required technical skills.

I am however also aware that an open system can have its drawbacks. It is difficult to get things done in an open system because introducing changes requires lots of coordination with others. Apple was able to quickly switch its processor model from an Intel chip to its own ARM chip because it controlled the OS and the hardware. Microsoft has however been struggling with ARM for years.

Apple has a great deal of flexibility to shape and develop their product how they want to while Microsoft needs to get other parties on board too. Apple’s strategy however a bit of a double-edged sword. A dictator can use his power to do a great amount of good for his people but this same power can be used to do great evil.

I think my greatest worry about Matrix is that it becomes something that’s only used by nerds and not by regular people. Another worry I have is about the public servers. A lot of these servers are hosted by hobbyists and volunteers. And I am sure that these people do this with great passion but they aren’t exactly bound by some kind of SLA.

Regular users have high standards when it comes down to availability. They want a chat app that just works. They will leave and look elsewhere when things are too slow or buggy. Nerds have a higher tolerance when it comes down to this stuff, especially when they believe in the technology behind it.

Matrix and New Vector will have to up their game if they want to compete with big boys such as Whatsapp, Signal and iMessage. The Element client can be quite buggy sometimes. Especially the Android client deserves some love. I tested it on an Android tablet and it was practically unusable. Certifying another user didn’t work because I got stuck in one of the dialog boxes so I couldn’t finish the process.

I am overall convinced that Matrix has potential, but I have my doubts if it is able to realize it.

### WhatsApp and Signal
WhatsApp was launched in 2009 by Brian Acton and Jan Koum. It quickly gained popularity and was later bought by Facebook for a staggering 19 billion dollars in 2014. Brian Action left the company in 2017 to start a nonprofit group, which later developed the Signal messenger. Jan Koum left WhatsApp a year later due to concerns about privacy, advertising and monetization by Facebook.

Signal started off under the name of TextSecure. It was initially developed by Whisper Systems and launched in 2010. Twitter acquired the company a year later. The service eventually was discontinued, but Twitter did release the source code of the application.

The application was later further developed by Open Whisper Systems, which was founded by the original owner of Whisper Systems (Moxie Marlinspike). Open Whisper Systems became the Signal Technology Foundation in 2018 when Moxie Marlinspike and Brian Acton decided to join forces.

Both WhatsApp and Signal have similar features:

* Both make use of the Signal protocol for end-to-end encryption
* Both can be used for one-to-one and group chats
* Both can be used for video and voice calls
* Signal offers an option to evade censorship by redirecting network traffic through proxies

#### Confidentiality
WhatsApp and Signal both use the Signal protocol for end-to-end encryption.   The protocol uses Extended Triple Diffie-Hellman (X3DH) for initial key negotiation and the Double Ratchet Algorithm for providing Forward Secrecy.

X3DH allows two parties to agree on a single shard key. Your phone will essentially generate a public and private key and sends the public one to the servers of Signal. Anyone who wishes to communicate with you can then send you an initial message by using your public key. The message will be held by the Signal server and later picked up by your phone when it is online. Your phone will then be able to decrypt the message with the private key.

The Double Ratchet Algorithm allows the rotation of encryption keys. Every message is encrypted with its own unique key. The new key is derived from the old one. It is not possible to reconstruct the old key with the new key. Even when an attacker manages to get access to the current key, it is not possible to decrypt previous messages.

As the name implies, the Double Ratchet Algorithm uses two Ratchets. One is used for protecting historical messages and the other is used for protecting future messages. This makes the connection ‘self healing’.

There are some nice Youtube videos that explain these subjects in more detail. Check them out if you want to know more:

* [Diffie-Hellman key exchange](https://www.youtube.com/watch?v=NmM9HA2MQGI)
* [Double Ratchet](https://www.youtube.com/watch?v=9sO2qdTci-s)

You can also take a look at the specifications for X3DH and Double Ratchet over [here](https://signal.org/docs/specifications/x3dh/) and [here](https://signal.org/docs/specifications/doubleratchet/).

The use of state of the art encryption earns both Signal and WhatsApp an ‘excellent’ rating.

#### Integrity and Availability
As with Keybase and Matrix, the integrity of all messages is checked before they are processed further. There are some differences when it comes to availability though. Keybase and Matrix keep the messages on the server while Signal and WhatApp remove them after they have been picked up. This strategy gives the user better confidentiality but comes at the cost of availability since they now lose all their chat history when their device gets lost or stops working.

WhatsApp has the option to make scheduled backups to Google Drive or iCloud, but these backups were stored unencrypted for some time. The option to encrypt backups was only recently introduced. Another thing is the Recovery Point Objective (RPO). The RPO indicates how much data is lost when a backup restore needs to happen.

WhatsApp allows you to configure a scheduled backup frequency. You can choose between a daily, weekly or monthly backup schedule. Your smallest configurable RPO would then be one day since you would lose up to a maximum of one day of chat history if your device fails. This is not that bad, but both Keybase and Matrix have an RPO of zero.

The backup capabilities of Signal are even more limited than those of WhatsApp. Signal can only make backups on Android. Backups are also stored on the device itself. You would have to manually copy the backup to a storage provider of your choice.

Apart from the RPO, you also have the Recovery Time Objective (RTO). The RTO indicates how much time you need to recover from a failure. With both Signal and WhatsApp you would need to:

* Get a new SIM card if the device was stolen or take the existing one out of your broken phone. You could also choose to keep a backup SIM card at the ready, but it would need to be registered on a different number since you can’t have two SIMs with the same number
* Insert the SIM into your backup phone
* Go through the registration process (assuming you already have the applications installed)
* Restore the backup (if you have one)

Let’s say this process would take you half an hour (assuming the backup phone is close to you and you don’t need to get a new SIM). And I am being nice here since I didn’t include the re-verification of all your contacts. This isn’t bad but then again, the competition provides the ability to just continue on one of your other devices (which doesn’t even need to be a phone).

Availability is not the strong suit of both WhatsApp and Signal. They both clearly underperform when compared to the competition. I have decided to give WhatsApp the ‘bad’ and Signal the ‘terrible’ rating.

#### Authentication and Trust
Both Signal and WhatsApp work with phone numbers instead of usernames. Phone numbers are verified by sending a text message with a unique code to the registered number. Contracts are pulled from the phone’s own address book.

Both platforms provide the ability to verify the keys of conversation partners. This can be done by scanning QR codes or manually comparing the key fingerprints. Signal offers the option to mark a contact as verified, but WhatsApp does not offer such an option. Keys are tied to devices which means that the verification has to be repeated if a user switches to a new device.

Both platforms also give the user the ability to secure their accounts with a PIN code. This prevents others from registering on their phone numbers. WhatsApp enforces a six-digit code while Signal allows longer alphanumerical PINs.

I am giving Signal and WhatsApp a ‘bad’ rating on Authentication and Trust. Using text message verification as a second-factor authentication method is already deemed risky. Most services have replaced it with push notifications or TOTP. The telephone network was not designed to be used as an authentication broker and, in my option, should not be used as such.

#### Privacy
The [Privacy Policy of Signal](https://signal.org/legal/#privacy-policy) can be summarized as follows:

* Signal tells not to profit from your personal data
* Signal stores the phone number you use to register. All other profile data is stored in an [encrypted format](https://signal.org/blog/signal-profiles-beta/)
* Your messages are kept in a queue if they can’t be delivered to your device (because it is offline). These messages are then deleted from the server after they have been properly delivered
* Signal can optionally use your address book to discover other Signal users. Contact information is sent to the server in a hashed format
* Signal may share your information with Third Parties
* Your user data is stored in the U.S.
* I couldn’t find anything about a logging policy. I do assume they at least keep some basic logs that contain things like IP addresses and device identifiers

The [Privacy Policy of WhatsApp](https://www.whatsapp.com/legal/privacy-policy/?lang=en) is a lot more complicated. It can be summarized as follows:

* Your Account information such as your phone number, profile name and profile picture is stored on the servers of WhatsApp
* WhatsApp can optionally use your address book to discover other WhatsApp users. Contact information is sent to the server in a hashed format. This information is not shared with the parent company (Meta)
* Undelivered messages are queued if they cannot be delivered. These messages are then deleted from the queue when they are successfully delivered or when the messages are still undelivered after 30 days
* They basically collect everything they can get away with. From your interaction with the app to the battery level and signal strength of your phone
* Your information is shared with Third Party providers such as Meta
* Your user data is stored in the U.S.

EU citizens fall under a different [Privacy Policy](https://www.whatsapp.com/legal/privacy-policy-eea). It is essentially the same as their normal Privacy Policy, but a lot more detailed. They are also more specific on what data they share with Third Parties.

I have given Signal a score of ‘good’ on privacy. It has not received an ‘excellent’ score because the platform requires you to share your phone number with your conversation partner.  This only allows you to communicate with friends, family and colleagues but not with some stranger you met on the internet for example. I have no problem with putting my Matrix and Keybase usernames on my contact page, but wouldn’t dare to list my phone number there.

WhatsApp obviously gets a ’terrible’ score when it comes to privacy. The company claims that respect for their users’ privacy is coded into their DNA, but at the same time, they pull every bit of data they can get their hands on off your phone.

#### Personal input
I am going to be honest with you. I don’t really like WhatsApp and Signal. I don’t like the whole phone-centric approach. It requires me to take a device with a small screen out of my pocket, while I have a big screen in front of me.

And sure, both of them have desktop apps. But they are reliant on your phone, which means they cannot be used as a fallback option. There is also no tray icon so you have to keep the window open all the time (also looking at you Element).

Both of these platforms just tire me out. I am tired of having to manage backups or having to start from scratch after a device swap or reset. I just want my chats to be there when I log in.

I am tired of the ‘Your security number with X has been changed’ messages. Just get rid of the [TOFU](https://en.wikipedia.org/wiki/Trust_on_first_use) already. Or at least allow for trust relationships between users instead of devices. People should trust people and not their devices. Devices change all the time. It is just not maintainable this way.

I am tired of having to worry about account takeovers because of something like a [SIM swapping attack](https://en.wikipedia.org/wiki/SIM_swap_scam). There is just nothing you can do about it. You are fully reliant on your phone carrier to have your back. And yes, you can set up a PIN and I have done so with Signal.

WhatsApp will however spam you with prompts until you become so irritated that you disable it again. I have saved the PIN in my password manager. There is no reason to bother me with these reminder prompts. Signal luckily has an option to disable them.

Most would say that WhatsApp and Signal are easy to use. I think that they are very difficult to use properly. Most people are just not using them properly.

## Results
Here follows an overview of all the ratings:

|   | Keybase | Matrix | Signal | WhatsApp |
| - | ------- | ------ | ------ | -------- |
| Confidentiality | good | excellent | excellent | excellent |
| Int and Avail | excellent | excellent | terrible | bad |
| Auth and Trust | excellent | excellent | bad | bad |
| Privacy | good | excellent | good | terrible |

It is kind of up to you how you interpret these results. You might rank them by the highest score or by the average score. I personally like to rank them by using the Lowest score since a chain is only as strong as its weakest link. This method would create the following ranking:

1. Matrix; lowest rating was ‘good’ on Auth and Trust
2. Keybase; lowest rating was ‘good’ on Confidentiality and Privacy
3. Signal; lowest rating was ‘terrible’ on Integrity and Availability
4. WhatsApp; lowest rating was ’terrible’ on Privacy

This ranking does however not mean everything. Most will choose WhatsApp because it has the biggest user base. You might give Matrix a try if you are already taking the effort to move away from WhatsApp. You can always move to Signal if Matrix is a bit too bleeding edge for you.

Just know that although Signal is a better choice than WhatsApp. It has inherited the same design problems. It is especially great fun to use it in a company setting where phone numbers are recycled as existing employees leave and new ones are onboarded.

Keybase can also be an option if you want something that is more stable than Matrix and has more features than Signal. Just know that its future is uncertain and you might be forced to move to something else later on.

## Closing words
I was actually planning to make this post shorter than my last one. ‘How hard could it be. Just compare some chat platforms. It should only take a week or two’ I thought. What a little naive boy I was, eating more than I could chew, but I am nevertheless pleased with the end result.

During my research, I have noticed that chat platforms in general don’t handle user trust very well. It feels like a degradation when compared to older technologies like SSL/TLS and OpenPGP.

I know it is sexy to claim that your product uses ‘Super advanced military grade quantum proof encryption’, but giving people the proper tools to verify and ideally also certify their conversation partners is just as important.  Especially now people can do stuff like having video meetings with government officials while impersonating someone else with deep fake technology ([source](https://nltimes.nl/2021/04/24/dutch-mps-video-conference-deep-fake-imitation-navalnys-chief-staff)).

I am fully aware that user trust is hard. It is not like encryption where you have a magic formula where plaintext goes in and cipher text comes out. User trust requires active participation from the users themselves. It is one of the reasons why tools like GnuPG are so difficult to use. This however does not mean that it can be ignored.

The next post in the OpSec blog series will be about passwords and multi-factor authentication. Thanks for reading and see you at the next one!
