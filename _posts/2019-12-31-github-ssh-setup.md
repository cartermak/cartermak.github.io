---
layout: post
title: Using SSH Authentication with GitHub
categories: Procedures
thumbnail_file: github-ssh-setup.png
---

# Overview

Git is a fantastic tool, but here's the issue---I'm lazy. Cloning and pushing to a git repository using standard HTTPS generally requires you to authenticate in the command line, but that's a lot of work. Instead, I use SSH authentication unless I'm working in an environment where someone could physically access my computer or otherwise get my private key. It's secure, and more importantly, it's fast and easy.

These instructions will focus on setting up local git authentication for GitHub on Debian Linux. Specifically, I use Pop!_OS (based on Ubuntu) as my Linux desktop environment, and Ubuntu on WSL in Windows. The procedures are just about identical for both. Here, we'll set up a local user with SSH authentication using a 4096-bit RSA key pair. 

[Here](https://help.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh) is a tutorial from GitHub covering these steps.

# Procedure

To begin, make sure Git is installed:

```bash
$ git --version
git version 2.17.1
```

 If you aren't returned a version, install it from apt:

 ```bash
 $ sudo apt-get install git
 ```

Next, initialize your user:

```bash
$ git config --global user.name "<Your Name>"
$ git config --global user.email "<you@domain.com>"
```

Now, the authentication. To begin, check whether you already have an SSH key pair:

```bash
$ cd ~/.ssh
```

If the directory `.ssh` doesn't exist, you can create it:

```bash
$ mkdir ~/.ssh
```

If the directory does exist, look for files `id_rsa` and `id_rsa.pub` (you may also see `id_ecdsa` or `id_ed25519`):

```bash
$ ls -a
.  ..  id_rsa  id_rsa.pub  known_hosts
```

If you don't see any of these files, you can create a key-pair using `ssh-keygen`:

```bash
$ ssh-keygen -t rsa -b 4096 -C "<you@domain.com>"
```

*The `-C` tag is optional and just adds a comment to the key. I like to use my email so it's easy to identify my public key.*

Now, just add the public key to GitHub. Navigate to GitHub Settings and select `SSH and GPG keys`. Create a new SSH key with an easily identifiable title, and copy the full contents of `id_rsa.pub` to the page. 

# Usage

The last step to using SSH for GitHub is to use the correct remote URL. When setting a remote, use a URL of the form:

```
git@github.com:user/repo.git
```

There you go! You're all set to leave entering credentials behind and start using Git with SSH.