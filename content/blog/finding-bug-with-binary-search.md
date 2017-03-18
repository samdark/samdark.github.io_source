+++
date = "2017-03-04T21:52:28+03:00"
draft = false
title = "Finding Bug with Binary Search"
+++

Once there's a way to reproduce the issue we need to find code which caused it. Sometimes we are totally stuck
for day feeling more and more depressed and, in the end, unable to think clearly. Luckily, there's a systematic approach
to find bug even if you have no idea what caused it and even where to set a breakpoint for proper debugging.
This approach is known as binary search.

If your code is under version control, firstly you check out a fairly old commit and see if it works. If it does work
then you check out a commit that is in the middle between the commit that works and the commit which did not and check
again. When there are no commits remaining in between the working and non-working commits, you arrived at the commit
that broke it. If you're using git, you're lucky since git has built-in tool `git bisect` that will help with this
process. It is quite simple. Let's say you're on current `master` commit and you have a bug.
  
```bash
git bisect # starts the process
git bisect bad # current commit has a bug
git bisect good 3.4.5 # I remember that commit tagged 3.4.5 was OK
```

After that, git informs you with something like `Bisecting: 10 revisions left to test after this`, which means
there are about 10 commits between good and bad revisions. Also it is checking out a commit which is in
the middle of these ten.

<img src="/img/posts/binary_search.png" width="50%" />

Now, it's your job to confirm if the bug is still present or otherwise. If yes, you issue
`git bisect bad`. If not &mdash; `git bisect good`.

git will choose either left or right part of these 10 commits and repeat the process.

After a few checks, you'll get, for example, `1029012930192390 is first bad commit` message.
If you confirmed the presence of the bug correctly, this indicates the exact commit that introduced the issue.


When everything is done you execute `git bisect reset` to end the process. 

Similarly, the binary search approach could be done with HTML markup of a single page when it's not under version control.
If you have a weird bug, delete half of the HTML page code and see if issue is still present.
If it is, then divide that HTML and check parts again. If it's not then take other half for inspection.

The advantage is that you'll certainly find what caused the bug for certain. However, it is a slow process when
you're not using a tool like git bisect.

The same methodology can be applied to anything. For example, this process widely used in electronics.
