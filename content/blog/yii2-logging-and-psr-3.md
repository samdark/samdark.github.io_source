+++
date = "2017-03-09T12:39:18+03:00"
title = "Yii 2.0 Logging and PSR-3"
draft = false
tags = ["yii", "log", "psr", "psr-3"]
+++

It is 2017 and major parts of PHP community are all talking about [PSRs: PHP standard recommendations](http://www.php-fig.org/psr/)
that aim is to make parts of frameworks reusable. The recommendation PSR-3 is about logging. Many logging libraries are
following this recommendation, among which [Monolog](https://github.com/Seldaek/monolog) is the most widely used one. 

There are three questions commonly asked about Yii 2.0 with regards to PSR-3:

1. Why isn't Yii 2.0 PSR-3 compatible?
2. How do I use PSR-3 compatible logger in Yii 2.0?
3. Is there a plan to extract a standalone PSR-3 compatible logging library from Yii 2.0?

Let's answer these.

## Why isn't Yii 2.0 PSR-3 compatible?

[Yii 2.0 logger](http://www.yiiframework.com/doc-2.0/guide-runtime-logging.html) is one of the well done parts of
the framework. It's stable, easy to extend, performant and really powerful when it comes to features. It was
implemented at early stages of yet secret pre-alpha development of the framework and was not changed much since then.
The design is very close to what was done in Yii 1.0 so we can think of 2008 as the year when logger design formed.

The year is important because it's way before PHP-FIG group which is responsible for designing PSRs formed. At the time
Yii 2.0 was in alpha stage we had a proven logger design with worked well with Yii 1.0 and Yii 1.1 and PSR-3 wasn't
a thing yet: there were nothing special about loggers implementing it and there was no benefits for Yii framework
adopting it. So then we decided not to.

Now it's time to re-decide it for 2.1 since there are certain pros in being PSR-3 compatible.


## How do I use PSR-3 compatible logger in Yii 2.0?

Yii's logging facility is quite flexible. There's a central dispatcher component which is collecting log messages and
then flushes them to individual [log targets](http://www.yiiframework.com/doc-2.0/guide-runtime-logging.html#log-targets),
such as file target or email target that actually do the job.

Yii's log targets are easy to extend but considering the popularity of PSR-3 and especially
[Monolog](https://github.com/Seldaek/monolog) it is tempting to reuse what's already done. For example, to send logs
to a Slack chat.
 
I've put together [an extension](https://github.com/samdark/yii2-psr-log-target) which allows you to use any PSR-3
compatible logger as Yii log target.

What is does it translating Yii's log levels to alike PSR-3 log levels and actually forwarding logs to PSR-3 compatible
logger configured. Configuration is fairly easy, you can find it [at extension page](https://github.com/samdark/yii2-psr-log-target).

## Is there a plan to extract a standalone PSR-3 compatible logging library from Yii 2.0?

Yii was never meant to be a set of standalone libraries. Independent components are nice but there is a cost of not
reusing what's available in the framework which in some case may result in bloated code and too abstract solutions.

Logger may be an exception since it's not relying on the framework much, it's framework that relies on it. An attempt
to extract logger may succeed and since we have a good design it may even become close in popularity to Monolog. So
overall it is worth trying and, I think, I'll work on it if [Patreon campaign](https://www.patreon.com/samdark)
will bring me enough time for it.
