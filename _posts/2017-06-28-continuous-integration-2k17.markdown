---
layout: post
title: "(Real) Continuous Integration in 2017: hard to sell?"
date: 2017-06-28
categories:
  - Continuous Integration
  - XP
description: 
image: 
image-sm: 
---

Continuous Integration is one of the main practices in the Extreme Programming landscape, although through the years it has transcended beyond XP to become one of the most common *cool things* to have in your development team. Due to the availability of numerous and versatile automation  tools (Jenkins, Travis, Go, AppVeyor, Bamboo ...), continuously building and testing your codebase is just one of those things rapidly becoming a *commodity* more than a rare thing or a luxury good in the software development world.

But continuous integration is much more than having an automation _gadget_ in place. The concept comes from the idea of constantly releasing internal versions of an whole system, with the aim to discover problems early and reveal design flaws. Kent Beck incorporated this idea, originally formulated by Grady Booch, into his list of _practices_. The definition of continuous integration, as written in _eXtreme Programming eXplained_ (1999) is the following:

>  Integrate and build the system many times a day, every time a task is completed.

While, again, this seems something common or quotidian in our present day, think about what it could mean twenty years ago. Incorporate the following thought: Cruise, the first CI tool, was released years after the C3 project, and it probably wasn't nearly as functional as today's automation tools. This means in the early days of continuous integration, it wasn't about the tools... because _there were no tools_ (well, not CI-specific ones).

<blockquote class="twitter-tweet" data-lang="es"><p lang="en" dir="ltr">I understand XP isn’t perfect, but simply implementing it as described in 1999 would improve so many teams.</p>&mdash; Steve_Hayes (@Steve_Hayes) <a href="https://twitter.com/Steve_Hayes/status/798775631613861888">16 de noviembre de 2016</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

In its essence, CI is more about integrating ideas and obtaining feedback. Overwhelmed and amazed by the shiny features of the latest automation _doohickey_, we sometimes forget that. _Communication_ and _Feedback_ are two of the four values of XP. And it is _people and interactions over processes and tools_, remember? Unfortunately, values are always harder to sell than practices, and it's definitely much easier to sell tools.

### So what happens to the tools?

Even when it comes to the tools, continuous integration does not begin with the automation provided by Jenkins or Travis. It definitely starts much earlier, when we put version control systems in place and share our changelists with the rest of the team as part of our daily work.

Using version control the right way is the foundation for good continuous integration practice, and consequently, there has been a lot of effort lately in discussing and defining the correct workflows or _branching models_ when working with git repositories, and this is precisely motivated for the need of integrating changes the best way possible.

It is very interesting how the experienced XP and continuous integration practicioners advocate for trunk-based models, in which integration is not deferred and conflict is not avoided. This is, again, much *harder to sell* than Pull Request -based workflows, specially when all these different tools and products are packed with lots of features around branching models.

<blockquote class="twitter-tweet" data-lang="es"><p lang="en" dir="ltr">after 10 years of giving talks on this, trunk-based development is still the idea that causes most controversy today! <a href="https://t.co/5EK7LQgvkh">pic.twitter.com/5EK7LQgvkh</a></p>&mdash; Jez Humble (@jezhumble) <a href="https://twitter.com/jezhumble/status/787866655598575616">17 de octubre de 2016</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

[caption para el tuit de lunivore y dan north sobre integración continua trunk, etc: while the "gitflow" branching model dominated the scene during the last years, many people advocate for a trunk-based model in which integration is not deferred/procrastinated but it is incentivated].

On the

So, what makes it a good continuous integration? The moment we embrace the practice of sharing our ideas and our code with the rest of our team continuously, we are keeping the spirit of continuous integration. And of course we have abanico de herramientas disponibles para ello.

Martin Fowler proponía su "CI certification test"
