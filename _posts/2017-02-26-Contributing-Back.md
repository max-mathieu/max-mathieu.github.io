---
layout: post
title: Contributing back to open-source projects
tags:
  - meta
---

It took me a while, but I am getting on the path to be able to contribute back to open-source projects.
Even after more than 10 years in the industry, most of the software I wrote lies in private repos (from private SVN/mercurial repos, to private git repos on bitbucket or github).

But, this code still relies much on open source code, from `node` of course, to npm libraries used in code (`lodash`, `config`, `request`, DB drivers) to devops tools (`pm2`), build tools (`webpack`, `grunt`/`gulp`) and front-end frameworks (yay `vue`).

I think "contributing back" can take many forms, all mapping to otherwise closed-source practices:

| Instead of... | Do... |
|---------------|-------|
| Writing your code that is tightly coupled to your business logic | Split the logic with a more generic core that could be open-sourced, and use that to build your business logic |
| Giving up on an issue/bug project X has | Report the issue/bug, so project X gets better |
| Keeping private a work around for an issue/bug project X has | Propose a patch or a PR, so people facing the same problem gets it solved too |
| etc... | |

But it is easier said than done.

## Why it can be hard

For starters, there are legal matters around the IP you produce as an employee/contractor.
You don't technically own it, so if your employer is not much into it or worried that your code could contain IP they paid for, it can be hard to do so.

Then come all the valid reasons to not do so:

- you suffer from the impostor syndrome (welcome to the club) and think what you do is not that interesting
  - fix: every open source project started with a way to solve a single problem. No-one expects you to write a new Unix OS in 1 commit
  - snarky fix: do something interesting
- you are scared people are going to judge you through your code
  - fix: look at some other projects and you'll see no project is perfect
  - snarky fix: write better code
- you think your code is worth a patent and/or millions
  - fix: forget about open-source, make a company out of it and get rich
  - snarky fix: no, it's not
- you think it'll take too much of your own time to maintain
  - fix: if it's something your company uses, talk to your manager: there are benefits in having other people contribute back. It can make your product better
  - snarky fix: sleep less
- you have a vision for your code and don't want other people requesting features that don't align with this vision
  - fix: listen to feedback, and decide if something is worth integrating or not. If possible, lay down your vision, and what is fine as PR or what should be a fork. State you prefer PR over "feature request" issues
  - snarky fix: include "opinionated" in your project description. Better, in the npm-published package name

## My current status

- created/maintaining the [WordPress plugin for heatmap](https://github.com/heatmap/heatmap-for-wp)
- contributed to [WordPress plugin for SparkPost](https://github.com/SparkPost/wordpress-sparkpost)
- reported issues without PR, because impostor syndrome. Like [here](https://github.com/SparkPost/php-sparkpost/issues/75) or [there](https://github.com/lodash/lodash-webpack-plugin/issues/81)
- open sourced the [setup of this blog](https://github.com/max-mathieu/myblog.github.io), which forces me to maintain 2 repos for this blog, but in a good way
- [submitted a PR](https://github.com/Unitech/pm2/pull/2707) to a major project, that was accepted! :champagne:

## What next?

I am looking up to [this guy](https://github.com/colestrode) and do more open-source stuff [like this](https://github.com/max-mathieu/pipestore), but with a real readme and doc.
It's just too hard to find extra time with 2 young kids
