# What is Xtinguish?

Xtinguish is a browser tool for deleting all your tweets from X (formerly known as Twitter).

Since Elon Musk bought Twitter, and particularly since he renamed it to X, I've observed a steady exodus of people I know and people I follow from the platform. Most, if not all, of these people have simply deleted their accounts. If you go this route you get around 30 days to undo, or recover, your account, after which it will be permanently deleted and your X handle can be reused.

But, whilst I can understand wanting to leave the platform, do you actually want to free up your X handle so it can be reused?

I'd argue not, and especially not if you used a handle based on your real name as many early users of Twitter did, or if you use that handle for other services. I can't even remember exactly when I signed up, although I seemed to start tweeting around August 2008.

Because the problem is that anyone could reuse your handle, and they could post anything they like with that handle, including views that you don't agree with, and that could be a problem if they're using that handle to impersonate you, or if (for example) potential employers or background check companies attribute undesirable activity on that account to you because it uses a handle that you also use elsewhere.

So maybe keeping the handle and removing all the content is the way to go?

There are a handful ways you can do this:

1. [Change your X handle](https://help.x.com/en/managing-your-account/change-x-handle) then register a new X account with your original handle, and then delete your original X account. This will get you an empty X account with your original handle, but none of your followers, followees, DMs, or favourites will be carried across (how valuable you think these are nowadays may be up for debate, but it's worth bearing in mind). The key point is that you still have your handle and nobody else can take it and impersonate you using that handle.


2. "Soft leave" by deleting all your content from your existing X account, but keeping the X account itself. This means you'll keep followers, followees, DMs, and favourites, but your account will otherwise be empty. Again, the key point is you still have your handle, so no-one else can use it.


3. Simply stop using X but keep your account. All your content will remain and you'll obviously keep your handle so that no-one else can use it.

Xtinguish is aimed at people who want to go with option (2).

> [!IMPORTANT]
> Elon Musk has made much of removing bot and other "illegitimate" accounts from X. There is of course no guarantee that, with any of the above, your inactive account might not be subject to automated removal which would most likely free up your handle for reuse, so you will need to remain vigilant to warning emails from X about your account activity at the very least.

# How does Xtinguish work?

Xtinguish is a Violentmonkey script, also known as a Greasemonkey script (but I recommend Violentmonkey), that uses DOM automation to delete all the tweets from your X/Twitter profile.

When you visit your profile page in X it will use X's advanced search to time travel back through all your tweets, month by month, including archived tweets (if you have more than about 3200 tweets), and it will go through each of them in turn, click the ellipsis menu for that tweet, click the option to delete the tweet, and then click the delete option in the confirmation dialog. After a short delay it will do the same thing for the next tweet. And so on, and so on, and so on, until there are no more tweets left to delete from your profile.

It will go all the way back to July 2006, when twitter was launched. However, you can tweak the script to set the earliest month from which it will delete tweets if you created your twitter account more recently. Here's an example of the kind of search syntax Xtinguish uses:

```
(from:bart_read) until:2008-09-30 since:2008-07-01
```

If your profile includes many thousands of tweets, as is likely to be the case if you have had an X/Twitter account for a long time, it may take several hours or perhaps even days to delete all your tweets, so keep your browser tab open!


# How do I install Xtinguish?

TODO: installation instructions


# How do I use Xtinguish?

TODO: usage instructions


# FAQ

## Why a Violentmonkey script rather than a browser extension?

Honestly, I built this for myself and I wanted to do the simplest thing that could possibly work without a lot of extraneous distraction. A browser add-in would have been more work that wouldn't have made sense for something that I'm likely only to use once (albeit that I have thousands of tweets for it to delete so there's a solid value-add to automating!).

That being said, I'm happy to accept PRs so if you feel inspired to submit one that turns this into a browser extension that would be much appreciated.

## Why Violentmonkey rather than Greasemonkey?

Violentmonkey is more capable and more actively maintained than Greasemonkey. For example, it's easier to install and manage scripts in Violentmonkey. As another example, Violentmonkey can also work on pages embedded in iframes, which Greasmonkey can no longer do.

I switched over to Violentmonkey some time ago because of this, hence it's the extension I recommend.

## Will this work in any browser that supports Violentmonkey?

In theory it should. In practice I've only tested in Firefox so YMMV.

## Why do you use DOM automation rather than X's API, which would surely be easier and more efficient?

Back in the day, before Elon Musk bought Twitter, using the API to do this would absolutely have been the sensible option (albeit that I'm sure the service I previously used to delete tweets did this and, apparently, it didn't work - see below!).

And you'd better believe I'd have vastly preferred to put together a command line script using Python, or similar, to automate deletion of tweets via Twitter's API. It would have been clean, and simple, and I could have had it done in maybe an hour.

Whereas DOM automation is (relatively) complex and finicky. If you look at the code, I'm not just simulating mouse clicks, but also - for example - mouse enter and mouse hover events over UI elements because typical anti-automation measures used on some sites include blocking or ignoring clicks that occur without falling within the correct sequence of expected mouse events. I'm also having to use timeouts to trigger actions on a delay, and persist state into isolated storage so that I can keep track of which tweets have been deleted already across page loads and refreshes. It's a ballache: lots more complexity than I'd have to contend with by simply using the API.

But, since buying Twitter and rebranding it as X, Elon Musk also introduced changes to pricing for X's API in early 2023 that would make it cost prohibitive to individuals to use it for bulk deleting many thousands of tweets, and I obviously don't want (nor could I afford) to bear those costs on behalf of those individuals.

So I'm pushed down the path of DOM automation, even though it does kind of suck, and is inherently more fragile and requires a lot more work to ensure that it functions reliably.

## But aren't there services to do delete all my tweets already?

Yes, and I used one many, many years ago when I'd considered getting rid of Twitter, but I couldn't remember what that service was called, and all the services I could find nowadays are paid for and/or seemed shady.

The paid for bit I can understand given the costs associated with using the X API nowadays, but the fact I didn't entirely trust these services meant I couldn't get on board with using them.

Similarly I didn't trust any of the browser extensions I found.

> [!NOTE]
> I mentioned that I'd used a service to delete all my tweets once before many years ago (more than 11 years ago I think - when I was still working for Redgate Software). This is true. However, what I discovered, in developing Xtinguish, is that it doesn't look like that service actually worked, because I was able to find tweets of mine going all the way back to August 2008. This ties up with my recollection of when I started using Twitter, when I was leading development in Redgate's .NET division and we were promoting early access builds of ANTS Profiler 4, which was in development at the time.

## Why the AGPL license?

I guess I've sort of hinted at this already but, as I already mentioned, there are a bunch of paid services that do what Xtinguish does. Some at least of these appear slightly shady. Maybe there will be more of them in future.

I don't want any of those services to be able to take code from Xtinguish and profit from work **I've** done by integrating that work into their service to provide mass tweet deletion functionality and especially if, on top of this, their service appears to be a bit shady.

AGPL is the best license to ensure that's the case - and offers options for enforcement where it isn't - and if people want to use my code for their business they're going to have to get in touch with me, we'll have a conversation, and they'll have to pay me to use the code under a different license that allows their commercial use.

And even if I do have that kind of conversation that results in licensing the code, Xtinguish itself will remain free and freely available forever under the terms of the AGPL.

## Yeah, OK, but why the AGPL rather than the GPL?

In theory at least somebody could use and modify code from Xtinguish on the back end of their application without distributing that code. The AGPL covers that use case, but the GPL doesn't. The AGPL also covers all the use cases that the GPL covers.

## I have a feature request - what should I do?

Please [add your feature request here](https://github.com/bartread/xtinguish/issues/new) including as much detail as possible.

You're welcome to submit a PR as well, although I'd suggest getting in touch by adding a feature request first so we can discuss and at least agree on the best approach.

## It didn't work, or I found a bug - what should I do?

I'm really sorry you're having problems. If you [tell me about the problem here](https://github.com/bartread/xtinguish/issues/new), again including as much detail as possible (see below), I'd be happy to try and help you if I can.

By detail I mean:

- What browser and operating system were you using (including version numbers)?

- What twitter handle were you trying to delete tweets for?

- What went wrong? What steps did you take that led up to the problem or error?

- Anything that appears in the browser console - for example, error messages or stack traces, that might provide more information

- Anything else you can think of that might be relevant

As I say, I'll be happy to try and help you.

You are also welcome to submit a PR that fixes the issue.
