---
title: 'Continuous Integration values in 2017: hard to sell?'
layout: post
date: '2017-06-28'
categories:
- ContinuousIntegration
- XP
description: 
image: https://unsplash.it/2000/1200?image=983
image-sm:
---

Continuous Integration is one of the main practices in the Extreme Programming landscape, although through the years it has transcended beyond XP to become one of the most common *cool things* to have in your development team. Due to the availability of numerous and versatile automation  tools ([Jenkins](http://jenkins.io), [Travis](http://travis-ci.org), [Go](http://www.gocd.org), [AppVeyor](http://www.appveyor.com), [Bamboo](http://www.atlassian.com/software/bamboo), ...), continuously building and testing your codebase is just one of those things rapidly becoming a *commodity* more than a rare thing or a luxury good in the software development world.

But continuous integration is much more than having the latest _automation gadget_ in place. The concept comes from the idea of constantly releasing internal versions of a whole system, with the aim to discover problems early and reveal design flaws. Kent Beck incorporated this idea, originally formulated by Grady Booch, into his list of _practices_. The definition of continuous integration, as written in _eXtreme Programming eXplained_ (1999) is the following:

>  Integrate and build the system many times a day, every time a task is completed.

While, again, this seems something common or quotidian in our present day, think about what it could mean twenty years ago. Incorporate the following thought: Cruise, the first CI tool, was released years after the [C3 project](https://martinfowler.com/bliki/C3.html), and it probably wasn't nearly as functional as today's automation tools. This means in the early days of continuous integration it wasn't about the tools... because _there were no tools_ (well, no Jenkins or GoCD, that's for sure).

<blockquote class="twitter-tweet" data-lang="es"><p lang="en" dir="ltr">I understand XP isn’t perfect, but simply implementing it as described in 1999 would improve so many teams.</p>&mdash; Steve_Hayes (@Steve_Hayes) <a href="https://twitter.com/Steve_Hayes/status/798775631613861888">16 de noviembre de 2016</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

In its essence, CI is more about integrating ideas and obtaining feedback. Overwhelmed and amazed by the shiny features of the latest automation product, we sometimes forget this. After all, _Communication_ and _Feedback_ are two of the four values of XP,  and the sign in the wall says _people and interactions over processes and tools_, remember? Unfortunately, values are always harder to sell than practices, and it's definitely much easier to sell tools than principles.

#### Step One: Start with Version Control and Trunk-Based Development

<blockquote class="twitter-tweet" data-lang="es"><p lang="en" dir="ltr">Good account of Continuous Integration (aka Trunk-Based Development)  <a href="https://t.co/Ay1NmN3Q5q">https://t.co/Ay1NmN3Q5q</a></p>&mdash; Martin Fowler (@martinfowler) <a href="https://twitter.com/martinfowler/status/611297227596820481">17 de junio de 2015</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

Even when it comes to the tools, continuous integration does not even begin with the automation provided by tools like Jenkins or Travis. It definitely starts much earlier, when we put version control systems in place and share our changelists with the rest of the team as part of our daily work.

Using version control the right way is the foundation for good continuous integration practice, no doubt about that. Consequently, there has been a lot of effort in discussing and defining the correct workflows or _branching models_ when working with git repositories. This is precisely motivated for the need of integrating changes the best way possible.

It is very interesting how the experienced XP and continuous integration practicioners advocate for [**trunk-based development**](https://paulhammant.com/2013/04/05/what-is-trunk-based-development/), in which integration is not deferred and conflict is not avoided. This is, again, much **harder to sell** than *branch-a-lot*, Pull Request-based workflows, specially when all these different tools and products are packed with lots of features around branching models.

<blockquote class="twitter-tweet" data-lang="es"><p lang="en" dir="ltr">after 10 years of giving talks on this, trunk-based development is still the idea that causes most controversy today! <a href="https://t.co/5EK7LQgvkh">pic.twitter.com/5EK7LQgvkh</a></p>&mdash; Jez Humble (@jezhumble) <a href="https://twitter.com/jezhumble/status/787866655598575616">17 de octubre de 2016</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

While the trunk-based development stance generally is depicted as the opposite of _gitflow_, it is important to remark that pull requests and feature branches are perfectly compatible with trunk-based development. It's only the **frequency** of integration in the mainline what matters. According to this, workflows where weeks (or even months) pass until feature branches merge into master should be avoided.

Embrace the **commit early and often** mantra, but also merge to the mainline as soon as possible, everyday if you can. Implement toggle mechanisms and make the design abstractions of your system cope with different features or lines of work. Checkout the Continuous Integration 


#### Build automation is a team effort

Putting the codebase management aside, it is also fundamental that each and everyone in the team accepts maintaining and improving automation as part of their routine. Do not put the whole CI effort over the shoulders of one of two people in the team. Having [Pipeline-As-Code](http://www.thoughtworks.com/radar/techniques/pipelines-as-code) mechanisms is great for that, as it is to include a Jenkinsfile or Travisfile into your repository that anyone in the team can modify. But this makes it part of the codebase now: keep it updated and keep it **clean** at all costs!

Also, avoid creating CI-maintenance "tasks" or "tickets". Maintaining the continuous integration flow should be something implicit, just as writing tests or refactoring your codebase. If it's a task, it can be deferred or procrastinated in favour of other tasks. But if keeping continuous integration up to date is part of the team's culture, it will never be avoided.

#### Visualize! Communicate!

One great thing about CI tools: they provide lots of different ways of notifying a broken build. Use this. You can send emails, Slack messages and all sort of messages. Go even beyond this if you can: use a TV monitor to continuously visualize your build dashboard. Put a giant traffic light in your workplace (yes, [there are teams doing that](https://wiki.jenkins.io/display/JENKINS/Traffic+Light+Plugin). Create specific [_Information Radiators_](http://alistair.cockburn.us/Information+radiator) for CI.

> Optimism is an occupational hazard of programming. Feedback is the treatment. (Kent Beck)

The goal of notifying broken builds loudly is not to shame anyone in the team, but to declare a temporary state of emergency where everyone can help. Of course, in such an 

##### CI Certification Test

### From CI to CD and Pipelines

In 2013, the CI scene went crazy with all sorts of new CI-As-a-service tools
Today, Continuous Integration tools are going further to become "Continuous Delivery" 
First, get Continuous Integration right

So, what makes it a good continuous integration? The moment we embrace the practice of sharing our ideas and our code with the rest of our team continuously, we are keeping the spirit of continuous integration. And of course we have abanico de herramientas disponibles para ello.
