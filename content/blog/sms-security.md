+++
date = "2017-07-03T00:17:03+03:00"
title = "SMS Security"
draft = false
tags = ["security", "sms", "password recovery", "login", "2fa", "password reset"]
+++

Nowadays SMS is often used as a channel for secure data such as various tokens, payment confirmation,
or two factor authentication. SMS has certain advantages. There is no need to install any special applications
or being connected to the Internet. It works even on legendary Nokia 3310.

![](/img/posts/nokia-3310-sms.jpg)

Everything is great, right? Well, no. Depending on the usage it could be a bad idea.

## What is wrong with SMS?

The problem is that SMS is insecure channel. 2016 clearly proved that. Details are summed well in Fortune's
&ldquo;[Time Is Running Out For This Popular Online Security Technique](http://fortune.com/2016/07/26/nist-sms-two-factor/)&rdquo;
article.

Moreover, phone numbers are often reused after canceling a contract and, in some cases, it is
possible to “restore lost SIM-card” without providing papers.

## Should SMS still be used?

As already was mentioned, it depends on how SMS is used. Let us review three common cases.

### Single factor authentication

Single factor authentication is when a single channel is used to confirm the user via sending a secret
such as password or a token.

If a code from SMS is enough to authenticate a user without entering any additional info then it means
SMS is used as a single factor of authentication. Since we already know that SMS as a channel is insecure,
it is a pretty bad idea.

### Two factor authentication

The idea of two factor authentication is simple. One may get a password by fiddling with a network
connection or another channel but that should not give attacker access to the system because login process
asks for additional confirmation from another channel. This confirmation, a second factor, is a short token that
is sent via another channel. The chance that multiple channels are compromised is slightly less.

![](/img/posts/2fa.png)

Having SMS as a second factor channel is not particularly bad and definitely is better than not using second
factor for authentication at all.

### Password reset

Resetting a password usually requires a user access to a communication channel linked with that account.
Two factor authentication is rarely used for it so resetting a password is effectively a single
factor authentication.

Of course, the difference is that if attacker is resetting a password, user can no longer log in so
covert surveillance is not possible. Still, the data and/or identity might be bad enough to lose even
for a short time span.

Traditionally a single channel for resetting a password was an email but in recent years many
projects started restoring passwords via SMS only. Knowing the nature of SMS it should be
considered a bad practice.

## TL;DR

- Do not use SMS to restore password or authenticate.
- It is OK to use SMS as a second authentication factor. 
