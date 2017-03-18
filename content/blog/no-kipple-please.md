+++
date = "2017-03-05T21:52:28+03:00"
draft = false
title = "No Kipple Please"
+++

> &ldquo;Kipple is useless objects, like junk mail or match folders after you use the last match or gum wrappers or yesterday's
> homeopape. When nobody's around, kipple reproduces itself. For instance, if you go to bed leaving any kipple around
> your apartment, when you wake up the next morning there's twice as much of it. It always gets more and more.&rdquo;
>
> ...
>
> &ldquo;There's the First Law of Kipple,&rdquo; he said. &ldquo;Kipple drives out nonkipple.&rdquo;

*Do Androids Dream of Electric Sheep? by Philip K. Dick*

IT projects are much like the apartments mentioned in Philip K. Dick novel. They tend
to have kipple and, as with apartments, it grows every day.

<img src="/img/posts/kipple.png" width="50%" />

I've reviewed many projects and one mistake that I often see is about kipple. It looks
minor compared to bugs or architectural issues but at the same time it affects both
project and development team significantly.

So kipple exists. Usually it's cryptic unneeded stuff that one hesitates to delete and
it is for quite vague illogical reasons. Examples of kipple is software projects include:
commented out code, files like `main.css_old`, unused methods, five different versions of jQuery,
code comments like `// TODO: `, etc.

That's why kipple is both useless and problematic:

- [Broken Windows Theory](https://en.wikipedia.org/wiki/Broken_windows_theory) applies
  well to software projects. If it's allowed not to clean up it's OK to write code that is
  of doubtful quality.
- Often developers comment out big chunks of CSS, JavaScript and HTML that are still
  served to the end user, thus slowing page loading speed.
- We're actually reading commented out parts of code, and it takes time.
- Large number of unused files can confuse newcomers.
- It is unpleasant to work with such &ldquo;kippled&rdquo; project. It can feel like the
  code is of a bad quality even if architecture and code itself is sound.
- Compile time may be increased.
- Any version control system remembers everything you'll delete. If there's a need
  you can always get it from there. If you fail to remember where it was,
  you can tag the commit.
  
I know that you may say that it's not important and there's no time for it but I highly
recommend trying it for a few months. You'll notice improvements in both the project and
overall quality of the code your team produce.