---
layout: post
title: "CSV Processing (at a glance)"
---

Not until recently did I find out [Ruby's native `CSV.parse`](https://github.com/tilo/smarter_csv#why) is not really performant. C'mon, loading 100_000 rows into memory? As if our beloved Ruby developer cum optimizer has not had enough on her table.

A quick Google search returned [the `smarter_csv` gem](https://github.com/tilo/smarter_csv). One more click led me to [this writeup](https://xjlin0.github.io/tech/2015/05/25/faster-parsing-csv-with-parallel-processing/) that planned out a better way when it comes to dealing with these nasty CSV processings.

I have only two things (which I deem relevant) to add to the above article:

- If you're a Sidekiq Pro user, Sidekiq offers [Batches](https://github.com/mperham/sidekiq/wiki/Batches), whose handies include child jobs (say, you divide 100_000 rows into 100 jobs that take care of 10_000 rows each), callback (a nice email letting customers know his import was done will do) & statuses (how many child jobs are pending or have failed?)
- If you're concerned that each worker establishing a connection of its own will soon blow up your database instance, use [pg_bouncer](https://pgbouncer.github.io). Heroku users can use [this handy buildpack](https://github.com/heroku/heroku-buildpack-pgbouncer) the company has made available.
- While having a direct route to your `users` table is nice and all, decently sized apps will come across cases when you have to do follow-ups when it comes to an import job. Things like: reindex ElasticSearch, spit out troublesome rows and let customers download these lines to perform revisions, generate log events, etc. My approach of preference is it's best to steer away from doing these things. It should be the job of controllers or services, not the import workers. In an ideal environment, your worker(s) should only concern about splitting the file into chunks, put some nice headers to 'em, and ping the relevant API(s) (ie: `POST /api/v1/users`) and let it do its job.

And yes, I ended up listing three things. I'm bad at numbers.