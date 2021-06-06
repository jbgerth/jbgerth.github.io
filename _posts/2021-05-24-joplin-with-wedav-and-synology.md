---
layout: post
title: "Setting up Jolplin with WebDAV sync on Synology"
description: "Setting up Jolplin with WebDAV sync on Synology"
categories: [privacy]
tags: [joblin, webdav, synology, privacy, self hosted]
lastmod: 2021-06-06
redirect_from:
  - /2021/12/20
---

## Goal

I was searching for a good way to organize my digital notes. There are many options out there for this purpose. My requirements for the app are:

- It should be self hosted for the best possible privacy.
- It should sync between devices so it is accessible everywhere.
- It should support Markdown as it is my preferred way to write notes.
- It should support notebooks and tags for easy searches.

These requirements lead me eventually to use Joplin in combination with WebDAV on my already running Synology NAS.

In this post I want to answer, how to set up Joplin with a working, encrypted WebDAV synchronisation.

### What is Joplin

For anyone who does not know about [Joplin](https://joplinapp.org) yet, here is a short description from the creators:

> Joplin is a free, open source note taking and to-do application, which can handle a large number of notes organised into notebooks. The notes are searchable, can be copied, tagged and modified either from the applications directly or from your own text editor. The notes are in Markdown format.

![Joplin UI picture](https://joplinapp.org/images/AllClients.jpg)

It provides a nice interface to take notes with a lot of options for synchronisation between different clients. Furthermore it has build in encryption and even supports the addition of pictures. The last cool feature for me is the extendability through Javascript, which makes it pretty unique compared to OneNote and the like.

### Component overview

My setup consists of three major components:

1. WebDAV on Synology
2. Joplin on my Windows Desktop
3. Joplin on my Android Phone

## Step by step setup

In the next section I will walk through, how to setup each part and how to connect them.

### WebDAV and storage on a Synology NAS

WebDAV is handling the sync between devices as well as the backup of the data. In my setup I use a Synology DS 218+, but it should work with most models.

After logging into the Web UI, navigate to the **Package Center**. There find and install the **WebDAV Server** provided by Synology. After the installation enable HTTP and HTTPS for the server in the control panel and hit apply. To ensure the connection with you Mobile device you need to add the HTTPS to the your router port forwarding.

Lastly a shared folder needs to be created from the **File Station** view. For this go to **Create** > **Create New Shared Folder**. After the creation give the user you intend to use for Joplin read and write rights. If you would like to add multiple users, you could create separate sub directories for each user.

### Joplin on Desktop

Download and install the desktop client of [Joplin](https://joplinapp.org) from the homepage. After finishing up the installation, open the application and go to **Tools** > **Options** > **Synchronisation** and select *WebDAV* from the *synchronisation target*. As an URL enter your local Synology IP. The protocol needs to be HTTP, the port is the HTTP port for WebDAV and lastly add the newly created directory for you user at the end. So the address should follow this schema: `http://<Synology_IP>:<HTTP_WebDAV_port>/<your_joplin_directory>` i.e. `http://192.168.1.100:5005/joplin`

The next step is to add your user and password. You can check the settings with the `Check configuration button`.

Now the setup on the desktop side is done. For added security you may want to add [encryption](https://joplinapp.org/e2ee/).

### Joplin on Android

The setup on Android is farley straight forward. After installing Joplin from the Playstore go through the *Burger Menu* to the options tab. In the options you will find the **Synchronisation** settings again. The setup here is similar to [Joplin on Desktop](#joplin-on-desktop). Instead of HTTP choose HTTPS as the protocol, choose the external IP or Dyn-DNS and the port. This should look like this `https://<external_Synology_IP>:<HTTPS_WebDAV_port>/<your_joplin_directory>` i.e. `https://my-nas.synology.me:5006/joplin`

Lastly enter your username and password again. If you set up encryption, it should ask you for the passwort to encrypt your data as well.

That is all.

## Final thoughts

Joplin is a really cool and versatile tool to organize notes. It does deserve more recognition in my opinion. If you enjoy there product, please let them know. 
