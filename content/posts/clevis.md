---
title: "Passwordless LUKS setup with Clevis"
date: 2022-08-02T17:47:51+02:00
author: "Valentijn Harmers"
draft: false
description: "No more typing your LUKS password when booting up your system"
categories: ["Technology"]
tags: ["linux", "ubuntu", "fedora", "opsec"]
---

Typing your password at every system bootup might get you annoyed at times.
Especially when you are used to Windows and macOS systems which store the 
disk decryption password in the TPM.

But what if I told you that you can also achieve this on your Linux setup.
We can use an application called 'Clevis' to get the job done.

I will describe the installation and configuration steps for Ubuntu and Fedora,
but the steps should be about the same for other Linux distro's.

# Installation

Open up a terminal as root user and run the following command to install the
necessary packages.

```bash
# Ubuntu
apt install clevis clevis-tpm2 clevis-initramfs clevis-systemd

# Fedora
dnf install clevis clevis-pin-tpm2 clevis-dracut clevis-systemd
```

# Configuration

Now we configure clevis to unlock a specific partition for us:

```bash
clevis luks bind -d /dev/sda3 tpm2 '{"pcr_ids":"7"}'
```

Replace `/dev/sda3` with the encrypted partition you want to unlock with
clevis. You can list all your partitions with the `lsblk` command.
Repeat the command for every encrypted partition you have.

Now we just enable Clevis on boot:

```bash
systemctl enable clevis-luks-askpass.path
```

Thats it. Now it's just a mater of rebooting your system.

{{< notice warning >}}
It might take some time before Clevis unlocks the disk. The system might
even ask you to input your password. Just be patient!
{{< /notice >}}

{{< notice warning >}}
I had a problem where installing the clevis package didn't
trigger an initramfs rebuild. I solved it by simply running
a `dnf upgrade` which would install a newer kernel version
and trigger a rebuild.

You can also manually rebuild the initramfs by running the following command:

```bash
# Ubuntu
update-initramfs

# Fedora
dracut --regenerate-all
```
{{< /notice >}}
