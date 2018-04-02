+++
date = "2018-04-02T23:02:47+03:00"
title = "YouTube's 500 error page"
draft = false
tags = ["yii", "youtube", "error"]
+++

Just caught [500-error at YouTube](https://www.youtube.com/user/AquaVEVO). No one is safe from that, even the best
projects but that's not the point of the post. The thing is that the error page is more useful than majority of other
error pages. Here's why...

![](/img/posts/youtube_error.png)

What is different here is a long wall of "information". You can not display anything useful in production since it would
allow hackers to crack your project easier. But it would have been great because searching for particular user-reported
error is, sometimes, a big pain. So the block of text in the screenshot is securely encoded debug information. Most likely,
there is a special micro-service used by YouTube developers where they paste information to decrypt it. Quite smart.

Using Yii you can implement similar feature 
[adjusting error handler](https://www.yiiframework.com/doc/guide/2.0/en/runtime-handling-errors#customizing-error-display)
to encode any useful information with [Security::encryptByKey()](https://www.yiiframework.com/doc/api/2.0/yii-base-security#encryptByKey()-detail).
And then implement a form for decoding purposes.
