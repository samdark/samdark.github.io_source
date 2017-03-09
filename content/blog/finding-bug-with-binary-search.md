+++
date = "2017-03-04T21:52:28+03:00"
draft = false
title = "Finding Bug with Binary Search"
+++

Once there's a way to reproduce the issue we need to find code which causes it. Sometimes we're getting totally stuck
for day feeling more and more depressed and, in the end, unable to think clear. Luckily, there's a good way to
find bug even if you have no idea what caused it and even where to set a breakpoint for proper debugging. This way is
binary search.

If your code is under version control, you're checking out fairly old commit and see if it works. If it works then you're
checking out commit which is in the middle between commit which works and commit which does not and check again. When
there are no commits left in between you get the commit that broke it. If you're using git you're lucky since it has
built-in way to do it via `git bisect`. It is quite simple. Let's say you're on current `master` commit and you have
a bug.
  
```bash
git bisect # starts the process
git bisect bad # current commit has a bug
git bisect good 3.4.5 # I remember that commit tagged 3.4.5 was OK
```

After that git tells you something like `Bisecting: 10 revisions left to test after this` which means
there are about 10 commits between good and bad revision. Also it is checking out a commit which is in
the middle of these ten.

Now it's your job to launch the browser or other client and check if the bug is still there. If yes, you're issuing
`git bisect bad`. If not &mdash; `git bisect good`.

git chooses either left of right part of these 10 commits and repeats again on that part only.

After a few checks you'll get `1029012930192390 is first bad commit` message which,
if you answered correctly, indicates exact commit introduced the issue.


When everything is done you execute `git bisect reset` to stop bisecting. 

Alike it could be done with HTML markup of a single page when it's not under version control.
If you have weird bug, delete half of the page HTML and see if issue is still there.
If it is then divide that HTML and check parts again. If it's not then take other half for inspection.

Pro is that you'll certainly find what caused the bug for sure. Con is that it's not so fast in
case you're not using a tool like git.

Same method could be applied to anything. For example, it's widely used in electronics.
