
---
title: "Conventional Commits"
date: "2023-05-08T23:58:50-04:00"
author: "Tom Villegas"
cover: ""
tags: ["", ""]
keywords: ["", ""]
description: ""
showFullContent: false
readingTime: true
---

There's a really nice project made by one of the students of my department [1], it aims to show graphically all the requirements between courses of a selected career. The commit history shows that he started it on [January 7 of 2022](https://github.com/tvillega/malla-fcfm/commit/43bed600ffee448bf731dee72f7e730cc958759f) and currently only supports the coursers of the Computer Science career.

While he does have a functional version on a subdomains of his, there are no instructions on how to deploy it. Since I really believe this project could have a strong impact on my university, I decided to poke around the source code to see if I could figure it out. And I did! Well, kinda. The deployment it's successful, but the redirection links are broken.

Nonetheless, my main goal here it's not to deploy the website again on my own server (although I did it anyways just for the sake of it) but to contribute back to upstream with new data. I know the developer tries to automatize it by building a web scrapper, but that's when his contributions stopped last year. Since his subdomain works perfectly fine, I thought I could make a pull request with hand-filled data.

The data input wasn't documented either, so I also figured that out by myself. I selected the courses from the Electrical department and filled all the crossed requirements between courses, and once deployed it worked pretty darn good! Here comes the thing. I'm realtively new to git. I've seen projects in git for ages, but I've never been in a position of contributing or even writing code.

[Nyveon](https://github.com/Nyveon/malla-fcfm)'s repo follows Conventional Commits [2], but that's not something I'm familiarized with. I know my commits can just be squashed and that's the end of the deal, but that puts load on the developer and my contribution would be so small I'd prefer to do it the right way from the beginning. Since I made my own instructions to deploy it, I could made a pull request for that too.

I have lots of projects going on, but all of them require that I develop a workflow and get sutck on that part. Currently none of my courses require the use of git or an organization scheme, I just dump code on a folder and pray for the computer to not die overnight. I do put the effort on using git whenever possible, specially with this website, but it all gets pushed on an hypothetical future where I have time. As a matter of fact I should be sleeping.

That's my thought of the day. I want to contribute on this wonderful project, but first I need to get more familiarized with Conventional Commits so I get the hang of it from the beginning. I'm also working on a separated project of my own, but time it's tight and it is sleep or code. So I chose none and opened a blog entry instead.

[1] https://github.com/Nyveon/malla-fcfm

[2] https://www.conventionalcommits.org/en/v1.0.0/
