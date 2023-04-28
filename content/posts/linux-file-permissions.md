---
title: "Linux File Permissions"
date: "2023-04-27T17:52:26-04:00"
author: "Tom Villegas"
cover: ""
tags: ["", ""]
keywords: ["", ""]
description: ""
showFullContent: false
readingTime: true
draft: false
---

## Backstory

Each student of the Computer Science's department is assigned a user on the server. That way we can have from printing quotas to Wi-Fi credentials. However, the thing I like the most it's the ssh access and that the [Apache's per-user web directories module](https://httpd.apache.org/docs/2.4/howto/public_html.html) is enabled. That's right, this website is sponsored by Universidad de Chile.

I have had experience setting up websites with `nginx`, I learnt the best practices from Debian and keep everything tidy at all times. However, on the department's server there's neither nginx nor superuser privileges. That's the first time I truly witnessed the power of linux file permissions.

The instructions where pretty straightforward.

* Create a directory named `public_www`:
```
$ mkdir public_www
```

* Using a text editor, create a file named `index.html` with the following content:
```
$ nano public_www/index.html
--------------
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title> Hello world! </title>
</head>
<body>
Hello world!
</body>
</html> 
```

* Allow Apache to cross the home directory:
```
$ chmod o+x ~
```

* Allow Apache to read the directory and the file:
```
$ chmod o+x public_www
$ chmod go+r public_www/index.html 
```

> Small fun fact. The instructions were originaly different, but when I followed them they didn't work. I went to the help deskto ask the system administrator about it and indeed the instructions were wrong. It seemed that the Apache's requirement have changed compared to last year and I was the first 2023's freshman to claim their free web directory.

## Things go wrong

Everything went smoothly and I succesfuly set up my pure html website. And it was ugly. I started with something useful: templates of the configuration files for the university's Wi-Fi connections. I didn't know that code blocks rendered so bad on mobile. I really like to write on pure html but good lord that looked awful.

Learning CSS just to change the code blocks seemed great, but since I have to actually keep the website updated it seemeded like a heavy load on the long term. Therefore, I started searching for website templates. Nothing too fancy, just a static html made by someone else. That's when chaos began.

I just `wget`'ed the tar file, untar'ed it and put it on a path inside `public_www`. It didn't load, so I just slammed `chmod 755` and saw my irresponsibility bear fruit. Then I remembered the system administrator and I told to myself: *"Hey! My sysadmin always uses the other thing, the one with the `+/-`. Let's revert the unnecesary permissions with that!"*. That's when I got the message that freaked me out:
```
tvillega@servername ~/public_www $ ls -lha theslant
ls: cannot access 'theslant/.': Permission denied
ls: cannot access 'theslant/..': Permission denied
total 0
d????????? ? ? ? ?            ? .
d????????? ? ? ? ?            ? ..

```

I always fix this with `sudo chmod 755`, but I don't have superuser access. So the directory `theslant` sat there on my web directory for a month until this week I could find the time to go give a visit to the help desk. And I have to admit it, it was a really good life lesson.

## File Permissions (revisited)

The following permissions are available on Linux:

|   |4  |2  |1  |   |
|---|---|---|---|---|
|0  |-  |-  |-  |no permissions  |
|1  |-  |-  |x  |only execute   |
|2  |-  |w  |-  |only write   |
|3  |-  |w  |x  |write and execute   |
|4  |r  |-  |-  |only read   |
|5  |r  |-  |x  |read and execute   |
|6  |r  |w  |-  |read and write   |
|7  |r  |w  |x  |read, write and execute   |
---------------------

This are different for the `user`, `group` and `others`, in that order, as seen on the following snippet:

```
tvillega@servername /var/lib ls -lha
total 60K
drwxr-xr-x 1 root         root         316 Feb  9 21:46 .
drwxr-xr-x 1 root         root         116 Apr 26 23:29 ..
drwxr-xr-x 1 root         root          24 Apr 27 00:41 alsa
drwxr-xr-x 1 root         root           0 May 27  2022 arpd
drwxr-xr-x 1 root         root          26 Jun 18  2022 blueman
drwx------ 1 root         root          34 Jun 18  2022 bluetooth
drwxr-xr-x 1 colord       colord        58 Jun 18  2022 colord
drwxr-xr-x 1 root         root          20 Jun 17  2022 dbus
drwxr-x--- 1 root         root         566 Apr 21 13:23 dhcpcd
drwxrwxrwt 1 root         root           0 May 10  2021 ex
drwx------ 1 root         root         242 Apr 27 19:55 iwd
```

## My (very much needed) lesson

At the help desk I tried to explain my situation been as concise as possible. My mind it's like a spiderweb when it comes to system administration, it's easier for me to open a command line rather than using words to describe the situation. But I succeded, because the sysadmin opened a shell on my `~` and checked the directory. *"I can't see inside `theslant` directory, I can't erase it either. It just lives there and I need an elevated command prompt to give myself **read** permission back"*

Here comes the funny part, I diagnosed wrong my issue. The sysadmin told me *Look here, at the bottom left corner. You have read permissions, what you don't have it's **execute permissions**. That's why you couldn't `ls` or `rm` the directory*.

He also told me that as long as I am the *owner* of a file or directory, I can add or remove permissions with `chmod`. In other words, I don't lose control over my files just because I remove permissions from them. I never thought of that, I never studied it either. I just *used* the permissions, I never saw the significance about their innerworks.

That day I learned two things:

1. Ownership it's more important than permissions, at least without messing with ACL.
2. `chmod [u|g|o][+|-][rwx]` uses symbolic notations and it's more readable.
3. Octals for chmod are `4|2|1` for `read|write|execute`

There's also `umask`, something that I always forget and it breaks my `texlive` from time to time.
But hey! That's for another story!
