---
title: "The OpSec Series - Authentication"
date: 2023-03-14T20:00:00+01:00
author: "Valentijn Harmers"
draft: false
showtoc: true
description: "The fourth post in the OpSec series covering Authentication"
categories: ["Technology", "OpSec Series"]
tags: ["opsec", "linux", "mac", "windows"]
cover:
  image: "posts/opsec_auth/auth.png"
  alt: "authentication"
  caption: "Image by [mohamed_hassan](https://pixabay.com/users/mohamed_hassan-5229782/?utm_source=link-attribution&amp;utm_medium=referral&amp;utm_campaign=image&amp;utm_content=6573326) from [Pixabay](https://pixabay.com//?utm_source=link-attribution&amp;utm_medium=referral&amp;utm_campaign=image&amp;utm_content=6573326)"
  relative: true
  hidden: false
---

*This post is part of a larger series. You can find all posts over [here]({{< ref "/categories/opsec-series">}}).*

We have arrived at one of the most hated parts of security: Authentication. Everyone knows the frustration of having to type in a username and password before accessing the systems you need to do your work. You even need specialized applications in order to keep track of all of these credentials. I sometimes feel like a stamp collector but instead of collecting stamps, I am collecting passwords.

And for a long time, there wasn’t a lot of development in this area. Things have been changing around in this space, however. Technologies like Single Sign-On (SSO) and Multi-factor Authentication (MFA) have gained popularity over the years. There are even efforts being made to eradicate the concept of passwords altogether.

Let’s take some time to discuss all of these options and look at their pros and cons and discuss what proper authentication should look like without driving your users insane. Before we start however, it’s worthwhile to mention the most common ways attackers break into accounts:

* Brute-forcing
* Credential stuffing
* Phishing
* Malware
* Abusing recovery methods

Brute-forcing is simply trying out passwords until you get the right one. This process is usually not done by hand but with an application such as [Hydra](https://github.com/vanhauser-thc/thc-hydra). The application will need a list of passwords to try. You can create these lists yourself or use lists compiled by others.

Credential stuffing also involves tying out passwords but the passwords are taken from leaked user databases of previously hacked companies. These databases are usually sold on dark web marketplaces and contain login information like usernames, email addresses and (weakly hashed) passwords.

This information is then used to try to login to other services since people have the tendency to reuse passwords between services. There are services like  [Have I Been Pwned](https://haveibeenpwned.com/) that allow you to check if your login information has been leaked.

Phishing is one of the most well-known ways for hackers to obtain login information. The hackers trick non-suspecting users to enter their login information into a fake version of a well-known website such as Twitter or Facebook. These attacks rely on a combination of user habits and emotions like greed or fear.

Smart hackers put their victims under pressure by adding a sense of urgency. They promise a reward or punishment if a victim acts or doesn’t act within a short timeframe. This forces the victim to act before thinking it through.

An attacker can also convince their victims to execute a piece of malware. These “evil” applications are often hidden within other “good” applications or file formats. A popular way is to hide the malware in an Excel Workbook file as a macro.

{{< notice info >}}
Malware infections with macros have become less popular because Microsoft software is now blocking them by default.
{{< /notice >}}

Malware can be used to do all sorts of evil stuff. But within the context of this blog post, we are more interested in the credential-stealing capabilities. Malware can log the victim's keystrokes and send them to the attacker. It can also pull login credentials from web browsers or simply search for files called “passwords.docx”.

The last method to get access to someone’s account is lesser known but is not to be underestimated. I am talking about a method where hackers use password recovery methods to reset the password to a chosen value.

My favorite story regarding this method is the story of how the AOL email account of the CIA director was hacked by a bunch of teenagers. The teens managed to get into the director’s account by resetting his password through the AOL Helpdesk. You can read the whole story over [here](https://www.wired.com/2015/10/hacker-who-broke-into-cia-director-john-brennan-email-tells-how-he-did-it/).

![Password Recovery](password_recovery.jpg)

Now we know how hackers can get into an account, it’s time to take a look at forms of authentication that can make it more difficult for them.

## Passwords
Ah, passwords. Probably one of the oldest ways of authentication. Even used before the age of modern technology. Password authentication relies on something only the rightful account holder knows.

The NIST Special Publication 800-63 version 1.0 published in 2004 ([link](https://csrc.nist.gov/CSRC/media/Publications/sp/800-63/ver-10/archive/2004-06-30/documents/sp800-63-v1-0.pdf)) introduced rules for password complexity. On page 52, the author proposed the following password requirements:

* A minimum length of 8 characters (from an alphabet of 94 printable characters)
* At least one uppercase letter
* At least one lowercase letter
* At least one number
* At least one special character

These requirements became the basis for many authentication systems. The author of the publication did come to regret his advice later on. It turned out that humans are not the best at remembering a supposedly random sequence of letters, numbers and special characters. This gets even worse when they are required to change their password every three months.

It is now recommended to use passphrases instead. Something like ‘Goats Love To Eat Honey’. These are easier to remember and difficult enough to crack. It is however better to leave the creation of strong passwords up to an application known as a Password Manager.

### Password Managers
A Password Manager is the digital equivalent of the notebook some people use to write down their login credentials. Many of them even have browser plugins so they can autofill the credentials for you.

You have some easy-to-use options like [1Password](https://1password.com) or [DashLane](https://www.dashlane.com) but solutions like [KeePass](https://keepass.info) or [KeePassXC](https://keepassxc.org) are also available if you want something with more bells and whistles.

Both KeePass and KeyPassXC are Open Source and use the same format to store passwords. You can synchronize your passwords across devices by dropping your database file in a Google Drive, Onedrive or Dropbox folder (or whatever cloud storage service you may be using).

A Password Manager is a ‘must have’ nowadays. There are so many services that require you to create an account. I even needed to create an account  to be able to easily update my graphics drivers. Password Managers help you to keep track of them all and will generate a random password for each of those service accounts.

The big drawback of these digital vaults is that you have to set them up on all of your devices and ensure everything is synchronized between them. The user experience on mobile platforms is also lacking. This is mainly because there is no proper auto-fill functionality available on these platforms.

Most modern web browsers such as Google Chrome and Mozilla Firefox do offer the option to safe website login credentials. These credentials are then also synchronized to your other devices running the same browser. Sounds like a good solution right? Sadly, no.

The problem is that these browsers store the decryption key for the credential store in a file on your device. This is essentially the equivalent of keeping your house key under the doormat. Firefox does allow you to set a master password for your credential store but you need to configure this on all your devices. You can read more about this problem in [this](https://fractionalciso.com/browser-password-managers-flawed-security-by-design/?utm_source=pocket_reader) article.

I can understand why a lot of people still don’t use password managers. Some solutions can be unreliable or difficult to use. My greatest annoyance is that secrets management is not always well integrated within the operating system. You always need to install a third-party solution to manage and synchronize passwords between your devices.

Apple is one of the view companies that have done a good job when it comes to this stuff. Their systems have a central keychain which is used to store sensitive materials such as passwords or encryption keys.

This keychain is synchronized between all of your Apple devices and can be accessed by certain applications. The Safari web browser does not have its own password store but uses the central keychain to store all website login credentials.

These credentials can then be used by your other devices for logging into websites or apps. I like how the apps pick up the credentials of the website equivalent. If you for example login to the Netflix website from your MacBook, the credentials are also used by the Netflix app on your iPhone.

Access to the keychain is managed with Apple’s authentication system. The operating system will require the user to authenticate with touchID, faceID or a preconfigured password or PIN.

I like Apple’s solution because it provides great security but also provides good usability. An easy to use solution has a greater chance of being adopted by the masses.

## One-time passwords
One-time passwords (OTP) are, just as the name implies, passwords that are only used once. These passwords usually are generated by the authentication system and sent to the authenticating user through a trusted channel. SMS is the most used channel but E-Mail is also used.

The main drawback of one-time passwords is that trusted channels are difficult to set up properly. SMS and E-Mail are popular options but these two channels can hardly be called trusted or secure. There are sadly not many more options to consider.

## Time-based one-time passwords
Time-based one-time password (TOTP) is a type of one-time password where time is used to generate short-living temporal codes which can be used for authentication. This method does not rely on a trusted channel to pass a one-time code from server to client and therefore does not have the shortcomings of regular OTP.

In TOTP, both authenticating parties agree on a shared secret. This secret is then combined with a timestamp of the current time to create a one-time code that is valid for about 30 seconds. The authenticating party presents this code to the authenticator and the authenticator checks if this code matches his own code.

The nice thing about TOTP is that there is no need for a trusted channel and  that there is no need to exchange the secret key when authenticating. The one-time code which is deprived from the secret key can be intercepted but will only be useful for a limited time.

Although TOTP fixes some of the shortcomings of regular OTP, it also introduces new problems. The biggest one is the administrative burden. You need to have an application to keep track of all these TOTP secrets. There are several to choose from like Google Authenticator, Microsoft Authenticator or FreeOTP.

These applications do however not offer the option to synchronize codes between your devices. This means you lose access to them when something happens to your phone. You do get backup codes that you can use in these kinds of situations but where do you keep them?

Luckily, password managers (like [KeePass](https://keepass.info) and [KeePassXC](https://keepassxc.org) ) have the option to keep track of TOTP secrets too. This allows you to keep your TOTP secrets and passwords in one place and synchronized across your devices. Sure, it’s more secure to keep your secrets and passwords in separate places but you can’t have it all.

TOTP and OTP do protect against brute-forcing attacks since an attacker has no way of guessing the right code. Phishing attacks still work though. The attacker just has to add an extra input field for the code to the Phishing page.

## Push prompts
Push prompts are a more easy-to-use alternative for OTP codes. The user who wishes to authenticate simply receives a push notification on their phone and acknowledges the login by pressing a button.

There is no standardized app for receiving push prompts, every platform has its own app. Android phones can receive push prompts for Google account logins and people with a Microsoft account can receive push prompts by installing the Microsoft Authenticator app.

Attackers have found an interesting way to beat push prompts. They simply keep spamming their victims with prompts until one of them gets acknowledged. This type of attack is referred to as ‘Prompt bombing’.

## Single Sign-on
Single Sign-on (SSO) allows you to use a single account for multiple services. The easiest example of this are the ‘Sign in with Google’ or ‘Sign in with Facebook’ buttons which are displayed on the signup page of a service like [IMDB](https://www.imdb.com) or [Feedly](https://feedly.com).

SSO is very useful for companies because it allows them to administer access for all of their employees from a single location. It also allows them to easily revoke all access when an employee leaves the company. This solution is better than having to create multiple accounts for different services for a single employee.

It can also be useful for individual users, allowing them to use a central account to access all of their services. This system can also turn on the user when they get blocked by the authentication provider. You are essentially putting all of your eggs in the same basket. Closing down your Facebook account also means losing access to all the services linked to it.

This is the main reason why I am cautious when using SSO. I generally prefer the use of separate accounts and safe all the credentials in a password manager.

## Hardware tokens
One way of creating a secure authentication solution is by outsourcing the authentication process to a dedicated hardware token. These devices usually look like regular USB-Sticks. They are however specialized in storing secret key material rather than regular files.

But having a hardware device is not enough. You need something to facilitate the communication between the device and the web service that requires authenticating. This role is filled in by FIDO2. FIDO stands for “Fast IDentity Online” and is the name of an alliance whose sole purpose is the total annihilation of the password.

FIDO2 was made in collaboration with the World Wide Web Consortium (W3C) and is made up out of the CTAP protocol and WebAuthn specification. CTAP was developed by FIDO and allows devices like laptops and smartphones to securely communicate with a hardware token through USB, Bluetooth or NFC. WebAuthn was developed by W3C and allows the communication from the hardware token to be relayed from the user's device to the web service.

The actual authentication process involves public and private key cryptography. The hardware token starts with generating a private and public key. The private key never leaves the device but the public key is shared with the web service. The web service then stores the key so it can be used later on.

A challenge is sent to the user when authentication is needed. This challenge has to be signed by the hardware token with the private key. The signed challenge is sent back to the web service. The service then verifies the signature with the earlier stored public key. The user is successfully authenticated when the signature checks out.

Using a hardware token is one of the most secure ways to authenticate. You can’t brute-force a signature. You also can’t steal the private key since it never leaves the token. You can steal the token itself though. It is therefore important to secure the token with a PIN. Hardware tokens are designed to wipe all cryptographic material when the wrong PIN is entered too many times.

## Passkeys
Passkeys follow the same concept as hardware tokens but the private key is not stored on a token but on the user device. These keys can then be synchronized to multiple devices.

Passkeys are a good alternative for those who are not willing or able to use a hardware token. This authentication method provides a better user experience but comes at the cost of security.

It becomes easier for an attacker to obtain the private keys because the keys are not stored on a separate hardware device but on the internal storage of a smartphone, tablet or laptop. There is also the risk of an attacker compromising the account used for synchronization.

## Comparison
Here follows a comparison of all discussed authentication methods against the earlier-mentioned attack factors. The table below compares the different authentication methods against the types of attacks. For each authentication method it will indicate which attacks are ineffective against it. A value of 'no' indicates that the authentication method offers no protection against the given attack method. A value of 'yes' indicates that the authentication method does protect against the given attack method.

|   | Brute-forcing | Credential stuffing | Phishing | Malware | Abusing recovery |
| - | ------------ | ------------------- | -------- | ------- | ---------------- |
| Passwords | no | no | no | no | no |
| OTP | yes | yes | no | no | no |
| TOTP | yes | yes | no | no | no |
| Push prompts | yes | yes | no | no | no |
| Hardware tokens | yes | yes | yes | yes | no |
| Passkeys | yes | yes | yes | no | no |

{{< notice info >}}
Passwords only protect against brute-forcing if they are complex enough. They can also be reused making them vulnerable to credential-stuffing attacks. Passwords can also be entered into a phishing page or stolen from the clipboard by malware.

OTP en TOTP cannot be brute-forced or used in a credential-stuffing attack (because each OTP key is unique per web service). The (T)OTP code can however be entered on a phishing page alongside the username and password and does therefore not protect against phishing attacks.

Getting access to the (T)OTP code is more challenging since these codes are usually kept on a separate device (a smartphone) but these devices can also be infected with malware. There is a possibility to get TOTP codes on a hardware device (Keyfob). These devices have a battery life of about 3 to 5 years.

Push prompts give about the same protections as (T)OTP but provide a better user experience. This method is however susceptible to prompt bombing. Push prompts also provide limited protection against phishing attacks. If a user is persuaded to enter their credentials into a phishing page, then there is no reason to suspect that they won't approve the push prompt.

FIDO2 hardware tokens provide a high level of protection. They protect against just about everything. You can't brute-force the private key and each service has a unique key. Phishing also doesn't work since the authentication process is handled by the token and the FIDO2 protocol.

The protocol will only accept challenges from legitimate servers. Malware attacks are also difficult because the key material resides on a separate device. Options are therefore limited even when an attacker has access to the laptop or smartphone of the victim.

Passkeys have many of the advantages of hardware tokens but the private keys do not reside on a dedicated device. The key material resides on the laptop, tablet, smartphone or smartwatch of the user and cannot be protected the way it can be protected on a hardware token.

None of the authentication methods protects against abuse of recovery attacks because the whole point of account recovery is to bypass the regular authentication method(s).
{{< /notice >}}

## Closing words
Authentication is difficult to do properly. There are many options and it's always going to be a balancing act between security and ease of use. I think it is important to take the tolerance of the end user into account and set realistic expectations.

Too many times a ‘box checking’ mentality is followed. Authentication systems are designed to pass auditing requirements and nothing more. Users are expected to remember complex passwords and change them to something else every 3 months. The human brain is not the best at remembering random sequences of letters, numbers and special characters.

Nobody wants to make weekly trips to IT because they keep forgetting their passwords. So of course users are going to come up with passwords such as ‘JoeCorpWinter2023!@‘. I wouldn’t blame them.

Another thing is the frequency users are asked to authenticate. If a user has to authenticate twice a day and has a five-day work week and works around 48 weeks a year, it would mean that they need to authenticate 2 * 5 * 48 = 480 times a year. That’s a lot.

The human brain is good at automating boring tasks. It won’t take long for these tasks to be outsourced to the subconscious mind. People will start entering their credentials on autopilot as soon as they are presented with a login screen. This is one of the main reasons why phishing attacks are so effective.

I am convinced that companies can greatly improve their security posture and employee productivity by thinking further than the checklist. The people who design the security systems need to be able to place themselves into the feet of those who are going the use these systems. Ideally, you would want ways of authentication that feel more natural than just using passwords.

I have always used passwords for disk encryption and user login in the past but solutions like the Trusted Platform Module (TPM), TouchID, Windows Hello and the Yubikey with FIDO2 have made life so much easier.

The next big challenge will be the prevention of the abuse of recovery methods. It doesn't matter how strong your authentication is, it won't matter much if it is just a phone call away from being compromised.

That will be it for now. The next post will be about Infrastructure As Code (IAC). See you in the next post!

## Putting things into practice

For the practical part of this blog post, I am going to show you how to use a password manager called 'pass'. Pass is not the best or easy-to-use password manager but it builds forth on the previous practical post about [OpenGPG]({{< ref "/posts/opsec_mail">}}/#putting-things-into-practice). Pass relies on OpenGPG and Git version control to get the job done.

Passwords are saved in text files which are encrypted with OpenGPG. All password files are stored in a git repository. This makes it easy to share the passwords between multiple participants and keep a change history of every password.

{{< notice warning >}}
Git is not the easiest application to use. I am making the assumption that you are already using it since git is very popular in the IT world. You might want to follow a tutorial like [this one](https://www.atlassian.com/git/tutorials) or [this one](https://www.w3schools.com/git/) if git is unknown to you.
{{< /notice >}}

### Installation

You can install pass for your system with the appropriate package manager:

```
brew install git pass       # macOS
apt install git pass        # Debian/Ubuntu
dnf install git pass        # Fedora
choco install git pass4win  # Windows
```

{{< notice warning >}}
These instructions assume that you have already installed and setup OpenGPG on your system.
{{< /notice >}}

### Setting up the password store

You can create your first password store with the **init** command:

```bash
pass init 0x12345678

# Optionaly setup git version control
pass git init
pass git remote add origin git@example.org:passwords.git
```

Replace *0x12345678* with the ID of your own GPG key (you can list your key with `gpg -K --keyid-format 0xshort`). Replace `git@example.org:passwords.git` with the url to the remote git repository.

### Inserting passwords

Inserting a new password can be done with the **insert** command:

```bash
pass insert joe@example.org
> Enter password for joe@example.org:
> Retype password for joe@example.org:

pass git push
```

Entry names take on the '<username>@<site>' format. Pass will create the commit for you but you will need to push the changes to the remote server yourself.

### Retrieve passwords

Passwords can be retrieved from the store by using the **show** command:

```bash
pass git pull  # ensure we have the lastest changes

pass show --clip joe@example.org
```

The *--clip* option sends the password to your system's clipboard. You can list all entries with the `pass ls` command.

### Sharing passwords with multiple team members

Pass was not initially designed to work with multiple people, there are however some tricks you can use to make it work.

First, you add the key ids of all of your team members to the *.gpg_id* file which can be found in the root of your password store. Then you reinitialize the store with the new keys:

```bash
pass init $(cat ~/.password-store/.gpg-id)
```
This command will re-encrypt all entries with the keys listed in the *.gpg_id* file.

You might want to look into a modernized version of pass called [gopass](https://www.gopass.pw) if are interested in a solution that works better for a group.

{{< notice warning >}}
The are some security related issues to consider when using solutions like pass or gopass:

- Entry names are not encrypted. An attacker can therefore see on which sites their victim has an account if they manage to gain access to the git repository.
- An attacker can add their own key id to the *.gpg_id* file and wait for someone else re-initialize the store, allowing them to decrypt all entries.

So as you can read, controlling access to the git repository is very important.
{{< /notice >}}
