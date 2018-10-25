+++
title="Repairing Silhouette CAMEO Touchscreen"
date=2017-12-12T21:53:44+03:00
draft=false
tags = ["hardware", "silhouette", "cameo", "resistive touch screen"]
+++

This year my wife got [Silhouette CAMEO® 3](https://www.silhouetteamerica.com/shop/machines/cameo) cutter as her
birthday present. She and our whole family were happily using it to precisely cut various cool things until last month.

## The problem

We store the device in a separate room in order for children not to hurt themselves with sharp parts and carrying it
to main room to actually cut things. After one of these transfers and turning CAMEO on LCD touch screen refused to react
on touch. It was quite frustrating because there are no buttons except power on/off and common actions, loading and
unloading cutting mat, are accessible from touch screen only.

Searching the Internet revealed that we're [not the only ones](https://www.youtube.com/watch?v=NBVaSfX164E)
with [touch screen not reacting](https://www.facebook.com/SilhouetteSchool/posts/948439995262210). So I wrote an email to
Silhouette America and, after a week of waiting, got no response.

## Research

It was time to try fix it myself. I've searched more and found [a video where a guy from Indonesia is replacing a touch
screen](https://www.youtube.com/watch?v=IQRx4BtNvvo). People in the comments were clueless about where to get a spare
part and since it was likely that I'll need one, I've decided to disassemble device as done in the video to get
part ID or manufacturer to search for.

There are three screws holding the control box. Two on the left side of it:

<img src="/img/posts/repair-silhouette/screws_1.jpg" width="100%" />

<img src="/img/posts/repair-silhouette/screws_2.jpg" width="100%" />

And one at the bottom of the device:

<img src="/img/posts/repair-silhouette/screws_3.jpg" width="100%" />

> Warning: If you've decided to do it, do it very carefully not to damage very thin touch screen cable. Likely you
  won't need to detach it at all. 

Unscrewing screws revealed that the control box is mostly there to cover some connections and to hold touch screen.
I've decided to turn on device while it's disassembled just in case and was quite surprised that touch screen worked
perfectly. Puzzled, I've assembled it back and it did not work again. I've repeated it multiple times before realizing
what happens.

## Why?

The touch screen used in Silhouette products is of resistive film type. When pressing it you're basically shorting two
layers of the screen:

<img src="/img/posts/repair-silhouette/resistive-touchscreen-technology.jpg" width="100%" />

There is [detailed description on how it works](http://www.sky-technology.eu/en/displays/touch-screens/how-do-touchscreens-work-a-complete-touch-screen-overview.html)
at the website where I've found the image above. The key points are:

1. A resistive touchscreen responds to pressure and doesn't care what object applies the pressure.
2. This technology only registers one touch point.

So what happened was that while moving device the control box or one of its screws deformed a little bit and the box
started pressing on the edge of the screen itself. Resistive screen was registering that press only ignoring fingers.

## Fixing it

Experimenting a bit I've found a part that was applying the pressure. In my case it was outer frame on the left. So
I've made a small wedge out of a match:


<img src="/img/posts/repair-silhouette/fix_1.jpg" width="100%" />

And then applied it:

<img src="/img/posts/repair-silhouette/fix_2.jpg" width="100%" />

After putting screws back it worked as good as new. The only thing left was cutting the rest of the match. 
