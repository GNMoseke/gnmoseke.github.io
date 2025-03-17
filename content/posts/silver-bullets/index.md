+++
date = '2025-03-17T21:00:00+01:00'
draft = false
title = 'Silver Bullets, Dogfood, and Treehouses'
summary = "Making software is hard. Be willing to be flexible."
tags = ['Software Engineering', 'Opinion', 'Tech']
+++

{{< alert "coffee" >}}
Everything in this post is **my opinion**, and anecdotes are, well, anecdotal. I
think it's only fair to encourage you to read with a grain of salt, because
people blindly taking tech articles at face value is what's lead to a lot of the
frustrations I want to talk about in this post.
{{< /alert >}}

## No Silver Bullets

Ever since a senior engineer early in my career said it to me, I've had a phrase
stuck in my head that I've tried to always keep in the back of my mind when I
get frustrated at something or deep into a complex system:

> [In software] There are no Silver Bullets

This comes originally from the [academic paper by Fred Books](https://en.wikipedia.org/wiki/No_Silver_Bullet),
which is a fantastic and a completely worthwhile read. Here's the main point:

> There is no single development, in either technology or management technique,
> which by itself promises even one order of magnitude improvement in
> productivity, in reliability, in simplicity.
>
> — <cite>Frederick Brooks[^1]</cite>

[^1]: https://www.cs.unc.edu/techreports/86-020.pdf

This is something that I think gets swept under the rug too often (especially in
the current LLM coding "assistant" boom, which I've written about
[here](https://purpleshirt.dev/posts/generative-models-and-the-death-of-creativity/#code)).
The problem is that the people I've most often observed doing the sweeping are
the ones that don't understand the point. With very few exceptions, every
*engineer* I've talked to holds the above quote to be pretty much fundamental.
The people who claim that XYZ language/tool/framework/pattern is "the future"
give me this reaction:

{{< figure
  src="/images/techbro.jpg"
  caption="Write it yourself then!"
>}}

Bitterness aside, I understand that these statements are coming from either a
place of passion for the language/tool/framework/pattern (hereafter "LTFP"), or
from a legitimate desire to improve whatever piece of software is being built.
We, being humans, also have plenty of bias towards things that we're familiar
with or particular patterns that our individual brains handle. The problem is
when one of these tools is evangelized as gospel - because ***there are no
silver bullets.***

## My Way Isn't Right Either
A trap that feels easy to fall into (and, self-reflectively, one that I am
absolutely guilty of falling into) is the allure of familiarity. To use myself
as an example: I work professionally mostly in Swift on the server. I am very
comfortable in Swift (ironically, for basically everything except the thing it
was originally created for, iOS apps). I like Swift. It's a great language. It's
also not good at everything. I also like Rust. I've recently started making a
more concerted effort to write small side projects in it, because I think it's
neat (and because I suck ass at using it and want to get better). You know what
I don't like, at all? Dynamically typed languages. I like it when the compiler
tells me I did a stupid thing instead of getting a completely avoidable runtime
crash (obviously, this is a gross oversimplification and these terms have very
wide meanings. Grain of salt).

But you know what I *immediately* reach for when I need to do some sort of
marginally complex (read: annoying to do in bash), repetitive, one-off text
processing? Python. Because it's the right tool for the job. Could I do it in
Swift just as well? You bet. Could I do it in Rust? It would probably take me an
embarrassing amount of time so ask me again in a year, but yes. But I guarantee
that in python, it will:
1. Require precisely one file
2. Be trivially simple to write and read
3. Run virtually anywhere
4. (Bonus) If I have to do some super weird and specific thing, there's a pretty
   high chance that a library for either exactly that thing or close enough to
it already exists that I can leverage.

Now, the opposite of that: I would rather my socks always be marginally damp
than write a large piece of complex software entirely in python[^2]. Could I? You
bet. Do people? All the time. Would I do it if it were my job? Of course. But
given the choice, I will reach for a compiled language every time.

[^2]: This was the most mild annoyance I could think of

My point here is that every single LTFP out there is a *tool*. Just because a
carpenter is more familiar with a table saw than a welding torch doesn't mean
you should use a table saw to patch a hole in a boat (disclaimer: I have no idea
how to actually patch a hole in a boat, please judge this metaphor accordingly).
If nothing else, the fact that there are so many different LTFPs out there, with
so many users of each of them, should indicate that even if you think the one
you like is the secret silver bullet... it definitely isn't.

## You Don't Know You've Built a Shit Treehouse Until it Falls Out of the Tree
I think the other key piece here is that you have to use the software you build.
And you have to use it with the intent of changing it if it doesn't work,
because good software is built iteratively, it doesn't spring forth like Athena
from the skull of Zeus (which is a [crazy myth](https://en.wikipedia.org/wiki/Athena#Birth)
by the way). The term that I've most often heard (and now use) for this is
[dogfooding](https://en.wikipedia.org/wiki/Eating_your_own_dog_food). This gives
you two benefits:
1. If you've built a bad piece of software (a shit treehouse), you will find the
   places it breaks quickly and spectacularly (fall out of the tree), especially
   when integrating with other pieces of software.
2. (Perhaps more importantly but without a funny visual metaphor) You stay
   engaged in what you're building when you use it often and see the
   improvements you made take effect.

One more quote from Dr. Brooks, this time on rapid prototyping:
> The morale effects are startling. Enthusiasm jumps when there is a running
> system, even a simple one. Efforts redouble when the first picture from a new
> graphics software system appears on the screen, even if it is only a
> rectangle. One always has, at every stage in the process, a working system. I
> find that teams can grow much more complex entities in four months than they
> can build.
>
> — <cite>Frederick Brooks[^1]</cite>

Anecdotally (because it's my blog damn it), this has been exactly my experience
with the things I've built for my own use:
* [Peregrine](https://github.com/GNMoseke/peregrine) was born from a want for
more readable CLI output when running large swift test suites. The first
versions didn't even use a RegEx for parsing stdout, but they worked on 90% of
output. I got that working in one day, which meant that I could use the tool
immediately! And then everything beyond that is just iterative tweaks, features,
and fixes that make it a better, more robust tool (like actually parsing with
a RegEx). Not only do I use it regularly at work now, but I could use it even
before it was in a `1.0.0` state, which kept me interested in actually working
on it.
* [Libero](https://github.com/GNMoseke/libero) started because I wanted my
spreadsheet of games to play to have cover art and look prettier. It's still not
a good piece of software, but it was an absolute mess when I started - the
layout was totally unusable, the scaling looked atrocious, and the internal
state handling... didn't. But because I started using it to store my backlog as
I was making it, it made me much more willing and interested in tinkering with
it. Seeing my personal backlog start to look better and better was a morale
booster, and I don't think I would have gotten it to a "stable" state without
that (to be clear it's still pretty bad and I consider it more of a personal toy
than anything, but I do actually still use it for my media backlog).
* [Athenaeum](https://github.com/GNMoseke/Athenaeum) is my latest stab at
getting better at Rust, and exists because I wanted a way to run through a bunch
of Dutch vocabulary flashcards without leaving my terminal (which is my entry
for "most geeky sentence of 2025"). It is bad code. It is littered with
panic-causing parsing code, happy-path assumptions, and `TODO` comments. But it
works, at least at a basic level (and with some help from [a custom fish
script](https://github.com/GNMoseke/dotfiles/blob/main/fish/.config/fish/functions/flashcards.fish)).
And, surprise surprise, that means I actually use the thing, and I write down
what would make it better, and my enthusiasm for adding those things stays.

To link with the first section of this post: I could have chosen a single LTFP
for all 3 of those things and tried to convince myself that it was the silver
bullet I needed for everything. But then I would be using a welding torch to
build a treehouse... or whatever the metaphor was.

## The Pitfalls of Pithyness
There's a million little rules & sayings like my beloved "No Silver Bullet."
Some of my favorites:
* [The 90-90 rule](https://en.wikipedia.org/wiki/Ninety%E2%80%93ninety_rule)
* [Now it's just a simple matter of writing the code](https://en.wikipedia.org/wiki/Small_matter_of_programming)
* [Premature optimization is the root of all evil](https://en.wikiquote.org/wiki/Donald_Knuth#Computer_Programming_as_an_Art_(1974))

I'm basic, I know. The last thing I want to leave you with is to take all of
these things with a grain of salt (if you'll notice, I also like that one). Roll
off the tongue though they do, it can be too easy to repeat them or things like
them ad nauseam as an argument for or against a single LTFP.

If I could add a second clause to the quote at the start of this post, it
would be this:

**[In software] There are no Silver Bullets. If a thing works a certain way,
there is a reason why - you should understand that reason before claiming that
something else is better.**
