+++
date = "2017-08-11T16:06:31+03:00"
draft = false
title = "Flavors of bad code"
tags = ["refactoring", "code", "spaghetti", "lasagna"]
+++

There are many flavors of bad code but let us focus on two prominent ones named after tasty Italian dishes:
spaghetti and lasagna.

## Spaghetti

Spaghetti flavored code is unstructured code where everything is mixed in a single place.

![](/img/posts/spaghetti.jpg)

Usually it is produced by novices who are unaware on how to structure their code and tend to skip
thinking about architecture. Typical reasons for spaghetti:

- Lack of experience.
- Not thinking about structuring code.
- Too tight deadlines.

## Abstraction and layers

What is the solution to make such code better? To refactor introducing abstraction. The only goal of abstraction is
to make things simpler and more manageable than they were.

Our brain has two types of memory, one of it is short term memory. It is similar to a stack data structure and its
capacity is at max of 5 items. That is why we can not deal with too complicated systems. Abstractions are a way of
hiding details so an abstraction becomes a whole item you can put into short term memory. If layering is done properly
there are about 5 components max at each level so you are able to get an overview of the whole system even if it is
complicated.

## Lasagna

Lasagna flavored code is layered code with clean interfaces. There is nothing wrong with it if it is done right.
Unfortunately, doing it right is hard and often we have it structured wrong. A bad lasagna that is too tall.

![](/img/posts/lasagna.jpg)

The goal of lasagna code is to make things simpler by introducing layers and developers are often fanatically following
this goal. They create layer after layer. Each layer becomes too simple while layer interaction becomes complicated.
It makes system overall less manageable than it was before. Reasons for bad lasagna:

- Lack of experience.
- Thinking about re-use case before thinking about use case.
- Unclear requirements.
- Permanently changing project goals.

## What is better?

I think that it is better to have spaghetti than bad lasagna. Both are, of course, evil, and should be refactored but
spaghetti is much easier to refactor. In order to refactor bad lasagna you should de-layer it first making it
almost spaghetti and then re-think and layer it again properly.
