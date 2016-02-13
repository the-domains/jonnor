---
author: []
related: []
publisher:
  url: 'http://www.jonnor.com'
  name: Jonnor
  favicon: null
  domain: www.jonnor.com
keywords:
  - guv
  - workers
  - queue
  - heroku
  - metrics
  - scaling
  - rabbitmq
  - number
  - jobs
  - configuration
description: 'At The Grid we do a lot of computationally heavy work server-side, in order to produce websites from user-provided content. This includes image analytics (for understanding the content), constraint solving (for page layout) and image processing (optimization and filtering to achieve a particular look).'
inLanguage: en
app_links: []
title: Jon Nordby
datePublished: '2016-02-13T18:12:00.905Z'
dateModified: '2016-02-13T18:04:25.229Z'
sourcePath: _posts/2016-02-13-jon-nordby.md
published: true
inFeed: true
hasPage: true
inNav: false
url: jon-nordby/index.html
_context: 'http://schema.org'
_type: Article

---
# Jon Nordby

At [The Grid][0] we do a lot of computationally heavy work server-side, in order to produce websites from user-provided content. This includes image analytics (for understanding the content), constraint solving (for page layout) and image processing (optimization and filtering to achieve a particular look). Currently we serve some thousand sites, with some hundred thousands sites expected by the time we've completed beta - so scalability is a core concern.

All computationally intensive work is put as jobs in a AMQP/ [RabbitMQ][1] message queue, which are consumed by [Heroku][2] workers. To make it easy to manage many queues and worker roles we also use [MsgFlo][3].  
This provides us with the required flexibility to scale: the queues buffer the in-progress work, broker distributes evenly between available workers, and with Heroku we can change number of workers with one command. But, it still leaves us with the decision on how much compute capacity to provision. And when load is dynamic, it is tedious & inefficient to do it manually - especially as Heroku bills workers used by the second.

If we would instead regulate this every 1-5 minute based on demand, we would reduce costs. Or alternatively, with a fixed budget, provide a better quality-of-service. And most importantly, let developers worry about other things.

Of course, there already exists [a number of solutions][4] for this[.][4] However, some used particular metrics providers which we were not using, some used metrics with unclear relationship to required workers (like number of users), or had unacceptable limitations (only one worker per service, only run as a service with pay-by-number-of-workers).

### guv

[guv][5] 0.1 implements a simple proportional scaling model. Based the current _number of jobs_ in the queue, and an estimate of _job processing time_ - it calculates the number of workers required for all work to be completed within a configured [![](http://www.jonnor.com/wp/files/system-model-whitebg-1024x389.png)][6]

The deadline is the maximum time you allow for your users to wait for a completed job. The job processing time \[average, deviation\] can be calculated [from metrics][7] of previous jobs. And the number of jobs in queue is read directly from RabbitMQ.

    # A simple guv config for one worker role. # One guv instance typically manages many worker roles '*':   app: my-heroku-app analyze:   queue: 'analyze.IN' # RabbitMQ queue name worker: analyzeworker # Heroku dyno role name   process: 20   deadline: 120.0 min: 1 # keep something always running max: 15 # budget limits 

Now there are a couple limitations of this model. Primarily, it is completely reactive; we do not attempt to predict how traffic will develop in the future. Prediction is after all terribly tricky business - better not go there if it can be avoided.  
And since it takes a non-zero amount of time to spin up a new worker (about 45-60 seconds), on a sudden spike in demand may cause some jobs to miss a tight deadline, as the workers can't spin up fast enough. To compensate for this, there is some simple hysteresis: scale up more aggressively, and scale down a bit reluctanctly - we might need the workers next couple of minutes.

As a bonus, guv includes some integration with common metrics services: The [statuspage.io][8] metrics about 'jobs-in-flight' on [status.thegrid.io][9], come directly from guv. And using [New Relic Insights][10], we can analyze how the scaling is performing.

If we had a manual scaling with a constant number over 48 hours period, workers=35 ( _Max_), then we would have paid at least 3-4 times more than we did with autoscaling (difference in size of area under Max versus area under the 10 minute line). Alternatively we could have provisioned a lower number of workers, but then with spikes above that number - our users would have suffered because things would be taking longer than normal.

We've been running this in production since early June. Back then we had 25 users, where as now we have several thousand. Apart from updating the configuration to reflect service changes we do not deal with scaling - the minute to minute decisions are all done by guv. Not much is planned in terms of new features for guv, apart from [some][11][more][12][tools][13] to analyze configuration. For more info on using guv, see the [README][14].
[![](http://www.jonnor.com/wp/wp-content/plugins/flattr/img/flattr-badge-large.png)][15]

[0]: http://thegrid.io/
[1]: https://www.rabbitmq.com/
[2]: http://heroku.com/
[3]: http://www.jonnor.com/2015/06/announcing-msgflo-a-distributed-fbp-runtime
[4]: https://github.com/the-grid/guv/blob/master/doc/braindump.md#prior-art
[5]: https://github.com/the-grid/guv
[6]: http://www.jonnor.com/wp/files/system-model-whitebg.png
[7]: https://github.com/msgflo/msgflo/blob/master/src/utils/newrelic.coffee
[8]: https://www.statuspage.io/
[9]: http://status.thegrid.io/
[10]: http://newrelic.com/insights
[11]: https://github.com/the-grid/guv/issues/43
[12]: https://github.com/the-grid/guv/issues/45
[13]: https://github.com/the-grid/guv/issues/46
[14]: https://github.com/the-grid/guv#best-practices
[15]: http://www.jonnor.com/wp/?flattrss_redirect&id=840&md5=3bbcad7a02e6fc242904ef0c96172fe8