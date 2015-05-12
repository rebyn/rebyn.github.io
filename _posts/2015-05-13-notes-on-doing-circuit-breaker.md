---
layout: post
title: Notes on doing circuit breaker
---

This is [Stoplight](https://github.com/orgsync/stoplight)-specific.

`.with_threshold` excludes the first failure. Let's say you want to retry the failed API call within 1 minute from the first failure, and ping the notifier (Log/Hipchat/Rollbar/etc) upon failing again:

```
begin
  Stoplight('example-1') { fail }
    .with_threshold(1)
    .with_timeout(60)
    .run
rescue Stoplight::Error::RedLight => e
  Rollbar.error(e)
end
```

Circuit breaking makes sense for consecutive failures (and retries off the hook); thus, you need to tackle the first occurrence of the failure properly.

```
begin
  Stoplight('example-1') { fail Api::Wrapper::ServerError }.run
rescue Api::Wrapper::ServerError => e
  'default_value'
end
```

Combine the two examples above, we have something like this:

```
begin
  Stoplight('example-1') { fail Api::Wrapper::ServerError }
    .with_threshold(1)
    .with_timeout(60)
    .run
rescue Api::Wrapper::ServerError, Stoplight::Error::RedLight => e
  Rollbar.error(e) if e.is_a? Stoplight::Error::RedLight
  'default_value'
end
```