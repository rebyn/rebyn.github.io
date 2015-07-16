---
layout: post
title: "Thoughts on single-purpose services"
---

1.

If you think about it, your simple CRUD Rails app is likely started out with a codebase and a service. People usually refer to MySQL/SQLite/PostgreSQL/etc as `persistence layer`, which in translation is a `service` that does a `single purpose`: persistence.

That is to say whether you like it or not, your app will always have to interact with external layers when it reaches certain complexity level.

2.

I used to determine whether a set of features fit in a problem domain, and thus extracted that set into a service. That worked for a while, until the cost of maintenance went too much for a small development team. Someone said we need decent monitoring infrastructure and deployment toolset before journeying into this land, and I can't agree more. That being set, most of the times you need to sit down and rebuild your existing monolithic app on seperated classes that tie to problem domains, instead of spinning up a new fancy service.

3.

Ruby isn't always the answer to everything. Not for persistence, for sure. And not for many others. Imagine you have to talk to multiple APIs to get the data you want, then process that data in order to make sense out of them. Parralel-ing these requests is possible with Ruby, also processing, but it will rake up your loading time to seconds. And we all know sad pandas will be sadder once they see seconds on the analytics dashboard.