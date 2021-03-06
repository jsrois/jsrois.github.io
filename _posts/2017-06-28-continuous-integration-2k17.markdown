---
title: Continuous Integration Values (in 2017)
layout: post
date: '2017-06-28'
categories:
- ContinuousIntegration
- XP
description: Continuous integration is much more than having the latest _automation
  gadget_ in place. What makes a good CI?
image: https://unsplash.it/2000/1200?image=983
image-sm:
---

Continuous Integration is one of the main practices in the Extreme Programming landscape, although through the years it has transcended beyond XP to become one of the most common *cool things* to have in your development team. Due to the availability of numerous and versatile automation  tools ([Jenkins](http://jenkins.io), [Travis](http://travis-ci.org), [Go](http://www.gocd.org), [AppVeyor](http://www.appveyor.com), [Bamboo](http://www.atlassian.com/software/bamboo)...), continuously building and testing your codebase is just one of those things rapidly becoming a *commodity* more than a rare thing or a luxury good in the software development world.

But continuous integration is much more than having the latest _automation gadget_ in place. The concept comes from the idea of constantly releasing internal versions of a whole system, with the aim to discover problems early and reveal design flaws. Kent Beck incorporated this idea, originally formulated by Grady Booch, into his collection of XP _practices_. The definition of continuous integration, as written in _eXtreme Programming eXplained_ (1999) is the following:

>  Integrate and build the system many times a day, every time a task is completed.

While, again, this seems something common in our present day, think about what it could mean twenty years ago. Incorporate the following thought: CruiseControl, the first CI tool, was released years after the [C3 project](https://martinfowler.com/bliki/C3.html), and it probably wasn't nearly as functional as today's automation tools. This means that in the early days of continuous integration it wasn't about the tools... because _there were no tools_ (well, nothing remotely close to Jenkins or GoCD, that's for sure).

<blockquote class="twitter-tweet" data-lang="es"><p lang="en" dir="ltr">I understand XP isn’t perfect, but simply implementing it as described in 1999 would improve so many teams.</p>&mdash; Steve_Hayes (@Steve_Hayes) <a href="https://twitter.com/Steve_Hayes/status/798775631613861888">16 de noviembre de 2016</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

In its essence, CI is more about _integrating ideas and obtaining rapid feedback_. Overwhelmed and amazed by the shiny features of the latest automation product, we sometimes forget this. After all, _Communication_ and _Feedback_ are two of the four values of XP,  and the big sign in your wall says _people and interactions over processes and tools_, right? Unfortunately, values are always **harder to sell** than practices, and it's definitely much easier to sell tools than principles.

#### Start with Version Control and Trunk-Based Development

<blockquote class="twitter-tweet" data-lang="es"><p lang="en" dir="ltr">Good account of Continuous Integration (aka Trunk-Based Development)  <a href="https://t.co/Ay1NmN3Q5q">https://t.co/Ay1NmN3Q5q</a></p>&mdash; Martin Fowler (@martinfowler) <a href="https://twitter.com/martinfowler/status/611297227596820481">17 de junio de 2015</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

Continuous integration does not even begin with the automation provided by tools like Jenkins or Travis. It definitely starts much earlier, when we put version control systems in place and share our changelists with the rest of the team as part of our daily work.

Using version control the right way is the foundation for good continuous integration practice, no doubt about that. Consequently, there has been a lot of effort in discussing and defining the correct workflows or _branching models_ (e.g. when working with git repositories). This is precisely motivated for the need of integrating changes the best way possible.

<blockquote class="twitter-tweet" data-lang="es"><p lang="en" dir="ltr">Anything with this picture isn&#39;t a best practise. Trunk-based development FTW // <a href="https://twitter.com/jezhumble">@jezhumble</a> <a href="https://t.co/Xk2ZmKwZQw">https://t.co/Xk2ZmKwZQw</a></p>&mdash; Dan North (@tastapod) <a href="https://twitter.com/tastapod/status/793520377293049856">1 de noviembre de 2016</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

It is very interesting to see how the experienced XP and continuous integration practicioners advocate for [**trunk-based development**](https://paulhammant.com/2013/04/05/what-is-trunk-based-development/), in which integration is not deferred and conflict is not avoided. This is, again, much **harder to sell** than *branch-a-lot*, Pull Request-based workflows, specially when all these different tools and products are packed with lots of features related to branching models.

<blockquote class="twitter-tweet" data-lang="es"><p lang="en" dir="ltr">after 10 years of giving talks on this, trunk-based development is still the idea that causes most controversy today! <a href="https://t.co/5EK7LQgvkh">pic.twitter.com/5EK7LQgvkh</a></p>&mdash; Jez Humble (@jezhumble) <a href="https://twitter.com/jezhumble/status/787866655598575616">17 de octubre de 2016</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

However, while the trunk-based development stance is generally depicted as an opposition to _gitflow_, it is important to remark that **pull requests and feature branches are perfectly compatible with trunk-based development**. It's only the **frequency** of integration in the mainline what matters. According to this, situations in which days, weeks (or even months) pass until feature branches are merged into master should be avoided.

The key to a good CI foundation is to embrace the **commit early and often** mantra, but also **merging to the mainline as soon as possible**, everyday if we can. Good continuous integration involves implementing _toggle_ mechanisms and making the design abstractions of the system cope with different features or lines of work.


#### Build automation is a team effort

Putting the codebase management aside, it is also fundamental that each and every member in the team accepts maintaining and improving automation as part of their routine. Do not put the whole CI effort over the shoulders of one of two people in the team. Having [Pipeline-As-Code](http://www.thoughtworks.com/radar/techniques/pipelines-as-code) mechanisms is great for that, as it is to include a Jenkinsfile or Travisfile into your repository that anyone in the team can modify. But this makes it part of the codebase now: keep it updated and keep it **clean** at all costs!

Also, avoid creating CI-maintenance "tasks" or "tickets". Maintaining the continuous integration flow should be something implicit, just as writing tests or refactoring your codebase. If it's a task, it can be deferred or procrastinated in favour of other tasks. But if keeping continuous integration up to date is part of the team's culture, it will never be avoided.

#### Visualize! Communicate!

One great thing about CI tools: they provide lots of different ways of notifying a broken build. Use this. You can send emails, Slack messages and all sort of standard notifications. Go beyond this if you can: use a TV monitor to continuously visualize your build dashboard. Put a giant traffic light in your workplace (yes, [there are teams doing that](https://wiki.jenkins.io/display/JENKINS/Traffic+Light+Plugin)). Create specific [_Information Radiators_](http://alistair.cockburn.us/Information+radiator) for CI.

> Optimism is an occupational hazard of programming. Feedback is the treatment. (Kent Beck)

The goal of notifying broken builds loudly is not to shame anyone in the team, but to declare a temporary state of emergency where everyone can help. There should be normal to have several of these _small crises_ everyday, and even if they should be treated with maximum priority, integration can be just put on hold (e.g. `git revert`) if the situation requires it.

So, what makes a good CI? The practice of sharing our ideas and our code with the rest of our team continuously. Of course we have all sorts of tools  to help us, but embracing the true spirit of continuous integration is infinitely more valuable than all the tools in the world.
