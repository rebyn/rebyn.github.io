---
layout: post
title: Let's Get That Merged
---

I took a quick detour from the Ruby land early this year, to [venture](https://twitter.com/rebyn/status/571872624470458371) into Goland. As a novice programmer, my first impression of Go is that it looks a lot like Javascript:

```
func main() {
  // nasty stuff here
}
```

One can argue that this looks like every other language in the C family. I jumped straight out of college after a year or so being exposed to only C, Ruby came upon me at my first job a few months after that, and I've only tried out Objective-C and Javascript in between. So, yeah, I'm not experienced and look at code without much foundation.

That said, while I struggled with Go, I figure let's kickstart this blog with something I'm a little bit more experienced in: Ruby. And what can be more mind numbling than having your code merged into one of the most renowned projects in the community: Ruby on Rails.

I aimed for this right from my first Rails internship at an agency in Berlin. The way the Ruby & Rails community has always been beginner-friendly and supportive of each other makes me feel deeply connected to the cause. However, it took me 2 sweet years for my first [pull request](https://github.com/rails/rails/pull/17267).

- First year: shut down computer after 5 minutes reading through Rails codebase. 
- Second year: closed Sublime Text after 30 minutes reading through Rails codebase & going over issues.
- End of second year: someone filed a bug & I was like *"Hey I can totally fix that"*.

Don't back off (just yet). After this, I've learned a few things that help taking a lot less time to [be more productive](http://contributors.rubyonrails.org/contributors/tu-hoang/commits) with contributions :-).

## Can someone tell me how to fix a Rails bug?


First off, stop what you are doing right now and read the [contribution guide](http://guides.rubyonrails.org/contributing_to_ruby_on_rails.html). I mean it. I did a few embarassing things in my first PR and all of them could have been saved if I had read the guide more carefully. Side notes:

- You should let people know you're working on a fix, by replying to the issue
- You should validate the bug, by creating a reproduction script ([sample](https://gist.github.com/why-el/5010105c9c2b74a3d1db))
- If you're not sure if it's a bug or an intended behavior, [Rails Mailing List](http://groups.google.com/group/rubyonrails-talk) is the place.

## After it's confirmed to be a bug:

- Find out why tests are not catching that. Most of the times, the case can be missing scenarios, so add tests first
- Fug the bix ;-)
- Revise Changelog if needs be
- Commit and submit PR.

Everything looks really easy with bullet points. In reality, it might not be as simple. Here are a few **tactics and tools that will help you along**:

- Read through to get a hold of various Railtie test suites: each suite uses different test techniques & setups, make sure you learn how to get started writing tests as soon as possible
- Understand the Rails way of doing things: it can be a bit different from your Ruby/Rails land, ie: prefer hash rockets, what cosmetic changes are and why PRs about them are not accepted, etc
- `git blame` & the PR workflow: find out where this bug was introduced, what caused it, read more on the discussion around the original PR to get more context.

## There are [400+ PRs](https://github.com/rails/rails/pulls) on the Rails repo right now. How to get yours merged soon-ish?

I know the momentum has to be kept. Everyone wants to keep moving on to other PRs. That's definitely a good thing, and there are certain things you can do on your side to speed up the process:

- Provide context. Reference the original issue of this PR, relevant mailing thread or Campfire chat
- `[ci skip]` for commits that should not take another 40 minutes away from Travis's build time
- Squash minor/WIP/dev/debug commits into a condensed one (or a few)
- Revise Changelog & write doco

And with all those, why are you still here :-)?