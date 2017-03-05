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
built-in way to do it via `git bisect`. 

Alike it could be done with HTML markup. If you have weird bug, delete half of the page HTML and see if issue is still there.
If it is then divide that HTML and check parts again. If it's not then take other half for inspection.

Pro is that you'll certainly find what caused the bug for sure. Con is that it's not so fast.

Same method could be applied to anything. For example, it's widely used in electronics.
