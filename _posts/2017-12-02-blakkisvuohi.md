---
layout: post
title: Bläkkisvuohi
category: Code
tags: [code]
date: 2017-12-02
---

Yesterday I released my Telegram bot Bläkkisvuohi into the open and made it open source. Bläkkisvuohi is a bot that helps to monitor your estimated blood alcohol concentration. There are 245 users who have used it during the past 2 weeks, so it's starting to be pretty popular (compared to most of the bots). You can find it at [github](https://github.com/ultsi/blakkisvuohi). 

Making the source code public included a lot of cleaning up. I spent 8 effective hours refactoring the code for the public eye and it certainly was a learning process for me. This post describes few of the hiccups I encountered.

### Even with private projects, don't commit secrets to the repo

One could guess that committing secrets to the repo is ok when it's meant for your private use only. It's not. Secrets should always be handled with care and not caring about secrets in your own projects is a habit that can trickle down into the work life. I spent half an hour removing all the commits that had the secrets in them. If you ever end up in the same situation, I recommend using the [BFG repo cleaner tool](https://rtyley.github.io/bfg-repo-cleaner/). It made dealing with git easy.

### Use a formatter and a linter with Javascript

My code wasn't that horrible, but there were little inconsistencies in every file. The code quality in my eyes increased a lot when I formatted the code with a formatter plugin in Sublime Text 3 to look the same in every file. The code turned out to be a lot more readable and it only took 5 minutes!

### Abstain from using Heroku as a dev environment

At first I was too lazy to set up PostgreSQL to my computer, so I just used a free Heroku dyno as my dev environment. Using Heroku as a dev environment meant, however, that every little change had to be committed so that it could be pushed to the Heroku remote. As a result, the project's commit history consists of a lot of commits with the message "Fix" containing only one line change.

If you want to dev against Heroku, I suggest the following tricks:

* Don't develop in master branch. Developing in another branch grants you the option to squash a lot of little commits when merging to master.
* When doing little changes, use the commands `git commit --amend` and `git push --force heroku yourbranch:master` to not generate lots of new commits.

<hr>

That's all folks!