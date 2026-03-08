---
layout: post
title: "Diffusion, Decay and Antimemes"
date: 2026-02-24
---

Antimemetics is the study of ideas that don't spread; the opposite of
the internet's favourite pastime of turning every stray thought into a
viral screenshot :). In Nadia Asparouhova's book Antimemetics, the focus
is on **real-world good ideas that die quietly:** truths that bounce off
incentives, status games and coordination problems until they vanish
into the void. In qntm's fiction work "There is no Antimemetics
Division", qntm explores ideas that actively resist being known or even
remembered, in a sci-fi horror context.

This article is my personal attempt to put those two meanings in the
same room, and build a mental model for why some information fails to
propagate, and when that failure is a bug (i.e. we're missing something
important) versus a feature (we're better off not amplifying it). If
memes are the mind-viruses of the modern world, antimemes are the ones
that come with a warning label... or worse, erase the label the moment
you look at it.

#### The two meanings of antimemetics

Before jumping into graphs and equations, it helps to be annoyingly
clear about terms, because "antimemetics" is doing double duty in these
two books. In the everyday Dawkins/internet sense, a meme is just an
idea that replicates: it hops from mind to mind, tweet to tweet, group
chat to group chat. Antimemetics then, is the study of the opposite
phenomenon: **ideas that fail to replicate**, or replicate only under
weird conditions.

**Antimemetics‑A (Asparouhova):** she gives us an explicit description
of why some ideas, often true, and important, don't become widely shared
because they collide with incentive gradients, status games, legibility
constraints, and coordination problems. The framing of the book is
explicitly about ideas "resisting" being seen despite their importance.

**Antimemetics‑B (qntm):** an antimeme as an informational object
with **self‑censoring properties**---an idea which, by its nature,
discourages or prevents people from spreading it. qntm's own framing
uses exactly this definition and the novel gives examples like
passwords, taboos, and hard‑to‑remember blobs of information.

Both are about transmission dynamics, not necessarily truth conditions.
qntm explicitly noted that "mimetic or antimemetic doesn't mean true or
false," and framed anti‑memes as ideas that aren't contagious or are
hard to share for multiple reasons. A helpful stepping stone (at least
for me) is to distinguish private knowledge, shared knowledge, and
common knowledge (everyone knows that everyone knows). Antimemetic
failure appears to show up in the gap between "some people know" and "it
becomes common knowledge," because that gap is governed by network
structure and thresholds rather than by correctness alone (an
implication of threshold models).

#### The share decision: the missing layer between heard and spread

A network model is blunt but useful, as each connection is a potential
transmission channel. A meme spreads when two things are true:

1.  it reaches someone, and

2.  that someone passes it on

Everything else, persuasion, taboo, jargon, clout (etc.) just changes
how likely (2) is, or how many exposures are needed before adoption. I
like to make (2) explicit with a minimal share utility:

$$ U_{\text{share}} = B - C - H. $$

Or in plain English: you share when perceived benefits (B) outweigh
friction costs (C) and expected harm (H). High (C) gives you frictional
antimemes (good ideas that stall because transmission is expensive);
high (H) gives you hazard-selected antimemes (ideas that stall because
spreading them is net harmful).

- (B): status, reciprocity, "I look smart," monetization, coalition glue.

- (C): time/effort to explain, verification cost, cognitive load, social awkwardness, reputation risk.

- (H): expected downside from dissemination, misuse, backlash, regulatory problems, or (in markets) crowding that destroys the edge.

A clean non-trading example where (H) is obviously real: vulnerability
disclosure; people often don't blast a working exploit to the whole
internet immediately, not because it's hard to explain (high (C)), but
because dissemination can cause immediate damage (high (H)) before
patches exist. That's antimemetics as a policy choice, not a mystery
imho.

#### Topology: why good ideas get stuck inside bubbles

Once you start treating an idea like a contagion, it becomes apparent
that whether an idea becomes common knowledge is often less about its
inherent quality, but more about whether the network can carry it. This
is not cynicism; it's literally what epidemic/cascade models are built
to study. A clean abstraction would be the graph:

$$ G = (V, E). $$

Here $V$ is the set of nodes (people, desks, funds) and $E$ is the
set of edges (channels where information can travel).

Let $p$ be an effective per‑edge success probability (whatever
combination of "I chose to share" and "you actually adopt/retain what I
shared" you want to bundle into one number). If an infected node has
degree $k$ (i.e., $k$ neighbours), then a rough early‑growth
heuristic is:

$$ R \approx p k. $$

This $R$ is basically how many successful new infections one infected
node generates on average, early on. If $R>1$, the idea is
supercritical and tends to grow; if $R<1$, it tends to fizzle. This
already hints at why where the leak starts matters; if we start at a
node with degree $d_0$, the expected size of the first wave is:

$$ \mathbb{E}[\text{first-wave transmissions}] \approx p \cdot d_0. $$

So hubs don't just spread faster in expectation; they're also less
likely to die out from bad early luck. Intuition for zero successful
transmissions in first wave:

$$ P(\text{no first-wave spread}) \approx (1-p)^{d_0}. $$

We can see that as $d_0$ grows, that "nothing happens at all" outcome
becomes much less likely.

Topology becomes most apparent when networks are modular (clusters with
a few cross‑links): buy‑side pods, asset‑class circles, etc. If an idea
is spreading inside community $A$, the chance it escapes into
community $B$ depends on how many bridge edges connect infected nodes
in $A$ to susceptible nodes in $B$. If $E_{\text{frontier}}$ is
the number of "active" cross‑community edges along that boundary, a
simple approximation is:

$$ P(\text{escape}) \approx 1 - (1-p)^{E_{\text{frontier}}}. $$

That's the probability that at least one of those boundary edges
successfully transmits. When $E_{\text{frontier}}$ is small, you can
get something that is locally viral but globally invisible, an
antimemetic idea not because it's wrong, but because the graph has
memetic borders!

Quite interestingly, not all central nodes are central in the same way;
high-degree nodes increase that local reproduction factor $R \approx
pk$. High-betweenness nodes sit on many shortest paths and are
disproportionately likely to be bridges between communities. So: degree
helps you spread within a silo; betweenness helps you hop between silos.

If you want a slightly more matrix-y handle on this: let $A$ be the
adjacency matrix of the graph, and let $x_t$ be a vector describing
"who is infected" (or infection probabilities, or expected infected
mass, depending on how you like your handwaving). An early linearized
diffusion would look like:

$$ \mathbb{E}[x_{t+1}] \approx p \cdot A \cdot \mathbb{E}[x_t]. $$

This says the expected next state comes from pushing the current state
through the network, scaled by $p$. Iterating gives us:

$$ \mathbb{E}[x_t] \approx (pA)^t x_0. $$

So the initial seed matters because $x_0$ that aligns with the
network's fastest growing direction (the top eigenvector of $A$) gets
amplified the most. That's basically the eigenvector-centrality
intuition!

Finally, there's the difference between simple and complex contagion. In
a threshold model, node $i$ adopts only when a large enough fraction
of its neighbours have adopted:

$$ \frac{\#\{\text{adopted neighbours of } i\}}{\deg(i)} \ge \theta_i. $$

Small $\theta_i$ means "one exposure is enough" (simple contagion).
Large $\theta_i$ means you need coordination, trust, repetition,
social proof (complex contagion). The compressed, meme-able layer of an
idea often behaves like a simple contagion, while the useful nuance
behaves like a complex one: harder to transmit, easier to lose at the
boundary.

#### Trading strategies are weird memes: the alpha kernel and implementation shell

A trading strategy leak is a good stress test for all this, because what
spreads is rarely the "strategy" as a single object. It's usually two
different contagions riding the same network:

**The alpha kernel:** a compressed, copyable rule-of-thumb ("buy $x$
when $y$ happens"), which behaves like a simple contagion. Model it as
an independent cascade: each informed node contacts $k$ peers and each
contact adopts with probability $p$. Early on, expected growth is same
as we saw before:

$$ R \approx pk. $$

And if $N_t$ is the number of adopters at "time" $t$ (think discrete
waves), then:

$$ N_{t+1} \approx R \cdot N_t, $$

which implies

$$ N_t \approx N_0 R^t. $$

This is just exponential growth when $R>1$, and decay when $R<1$.
The point is not that markets are literally a perfect branching process
(lol), it's that shareable kernels can go supercritical very easily.

**The implementation shell:** the unsexy but decisive part (execution,
sizing, regime filters, etc.). A simple way to capture needs trust /
repetition / context is literally the same threshold rule:

$$ \frac{\#\{\text{adopted neighbours of } i\}}{\deg(i)} \ge \theta_i. $$

In practice, the kernel often has low effective $\theta$ (easy to
imitate), while the shell has high $\theta$ (hard to internalise). So
the thing that matters most is the thing that spreads least. Classic.

Now for the part that makes trading strategies especially antimemetic:
diffusion changes payoffs. In markets, adoption can destroy the edge via
crowding and adversarial response, so alpha decays with the number of
adopters $N$. A toy crowding curve that captures more adopters → less
juice could be:

$$ \alpha(N) = \alpha_0 \exp\left(-\frac{N}{K}\right). $$

Here $\alpha_0$ is the "private" alpha and $K$ is a capacity scale
(how many similar adopters before returns compress a lot). If you
combine this with the diffusion curve $N_t \approx N_0 R^t$, you
get:

$$ \alpha_t \approx \alpha_0 \exp\left(-\frac{N_0 R^t}{K}\right). $$

Once diffusion takes off ($R>1$), alpha can fall extremely fast after
you cross capacity, because you're exponentiating an exponentially
growing thing. That turns "should I share this?" into an expected value
decision, not a vibes decision.

Reusing the same minimal sharing utility:

$$ U_{\text{share}} = B - C - H. $$

Same story, $B$ is the benefit (status, reciprocity, monetization,
whatever), $C$ is friction (time, effort, verification), and $H$ is
the hazard, now something you could (very crudely) price as the alpha
loss from accelerating adoption:

$$ H \approx V \cdot \mathbb{E}\left[\alpha(N) - \alpha(N+\Delta N)\right]. $$

$V$ here is your deployed capital (or the strategy's PV to your firm),
and $\Delta N$ is "additional adopters caused by you pushing this
into the graph" (including the uncomfortable fact that if you seed a
supercritical cascade, $\Delta N$ might be... not small). The kernel
spreads because it's simple, but rational actors suppress it because
diffusion has a measurable cost, while the shell doesn't spread because
it's cognitively expensive.

#### Some takeaways

If a strategy (or idea) doesn't spread, it's usually worth asking
whether it's frictional or hazardous:

- High $C$: hard to explain, hard to implement, high status/effort costs mean the implementation shell stalls (high $\theta$, low effective $p$).

- High $H$: sharing destroys value (crowding, adversarial adaptation, regulatory risk), meaning the alpha kernel is rationally suppressed even if it's easy to repeat.

Leaks also tend to make the wrong layer go viral: the kernel behaves
like simple contagion ($R \approx pk$), while the shell behaves like
complex contagion (thresholds). So most people learn a degraded meme,
not a true process (basic intuition would also say that, duh...).

And "it didn't go viral" isn't a verdict on truth. It can mean either:

- the network couldn't carry it (subcritical because of topology / thresholds / friction), or

- the network shouldn't carry it (negative EV because the hazard term is real).

If memes are ideas that replicate, then profitable trading edges are
often the opposite: they either can't be spread because the shell is too
costly ($C$), or must not be spread because diffusion kills them ($H$).

The best antimeme might be the one you almost remember... right before
it gets arbitraged away.


*PS: Shoutout to my friend Marc for revising my "Business School math" and confirming it is indeed, math. He's doing fantastic work at the [Eric and Wendy Schmidt Center](https://marcfm.com/), check it out!*
