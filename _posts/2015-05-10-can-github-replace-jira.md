---
layout: post
title: Can Github replace JIRA?
---

*Note: this post's title is more like a personal challenge. I'm not questioning just another choice from management here.*

So, it's that time of the year when we decide which would be our next project management tool. I've "been through" Kanbanery, Trello and most recently JIRA. Though I understand the rationales behind picking one of these, I can't help posing this question upon hearing the name of that new shiny tool: *Can we work around Github (which is my main workplace) to better suit our need(s)?*

Let's talk about JIRA, because I'm most annoyed at this tool (urgh, the inline edits). JIRA introduces things that current github.com's issue/milestone schema has yet to fit in:

1. Issue Type (Task, Epic, Story)
2. Priority (Major, Critical, Minor, Trivial)
3. Linked Issues (is blocked by, relates to, clones)
4. Story Points

Let's also not forget how github.com can do the rest of what JIRA does:

| JIRA                                    | GITHUB                                  |
|---------------------------------------  |---------------------------------------  |
| Sprints                                 | Milestones                              |
| Issues, Assignee, Labels, Description   | Issues, Assignee, Labels, Description   |
| Fix Version                             | `Fixes/Resolves #12345`                 |

For 1 - 4, I don't think Github will likely add any feature that somehow supports this kind of extra data, nor do I believe they should. So I resort to a simple hack: how about an API that persists data for 1 - 4, and a browser extension that does all the talking to this API (that, of course, is triggered whenever you're on a Github issue page) and displays relevant pieces of info right on your Github issue page?

OK, not so simple. This simple flow might bump more sense:

![](https://s3.amazonaws.com/f.cl.ly/items/3d0y022E1k1y3y1G423z/Untitled.png)

Together with a quick mockup I put together:

![](https://s3.amazonaws.com/f.cl.ly/items/380x0406412T2x3V2V2H/Screen%20Shot%202015-05-10%20at%204.31.21%20AM.png)

_____

Now, what else you want from this JIRA replacement project?