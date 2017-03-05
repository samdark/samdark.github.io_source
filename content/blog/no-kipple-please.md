+++
date = "2017-03-05T21:52:28+03:00"
draft = false
title = "No Kipple Please"
+++

> “Kipple is useless objects, like junk mail or match folders after you use the last match or gum wrappers or yesterday's
> homeopape. When nobody's around, kipple reproduces itself. For instance, if you go to bed leaving any kipple around
> your apartment, when you wake up the next morning there's twice as much of it. It always gets more and more."
>
> ...
>
> "There's the First Law of Kipple," he said. "'Kipple drives out nonkipple.'"

*Do Androids Dream of Electric Sheep? by Philip K. Dick*

IT projects are much like the aparments mentioned in Philip K. Dick novel. They tend
to have kipple and, as with apartments, it grows every day.

I've reviewed lots of projects and one of mistakes I often see is about kipple. It looks
minor compared to bugs or architecture mistakes but at the same time it affects both
project and development team significantly.

So kipple exists. Usually it's cryptic unneeded stuff which one hesitates to delete for
quite vague illogical reasons. Commented out code, files like `main.css_old`, unused
methods, five different versions of jQuery, `// TODO: ` etc.

That's why kipple is both useless and bad:

- [Broken Windows Theory](https://en.wikipedia.org/wiki/Broken_windows_theory) applies
  well to IT projects. If it's allowed not to clean up it's OK to write code which is
  of doubtful quality.
- Often developers comment out big chunks of CSS, JavaScript and HTML which are still
  served to end user slowing page loading speed.
- We're actually reading commented out parts of code. It takes time.
- Large number of unused files may and would confuse newcomers.
- It is unpleasant to work with such kippled project. Feels like code is of a bad quality
  even if architecture and code itself is OK.
- Compile time may be increased.
- Any version control systems remembers everything you'll delete. If there's a need
  you can always get it from there. If you fail to remember where was it, tag the commit.
  
I know that you may say that it's not important and there's no time for it but I highly
recommend trying it for a few months. You'll see difference in both the project and
overall quality of the code your team produce.