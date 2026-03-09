---
layout: post
title: "Seeing the Hand: How Reports Reprice Beliefs"
date: 2026-03-09
---

I recently read (admittedly late) a Kevin Mak tweet, where he talks about how a short seller's report is an additional piece of information, akin to getting to see someone else's hand in poker. That framing stuck with me. If you spend enough time in markets, it's almost inevitable that a short report or activist campaign will land on one of your positions. When it happens, the experience feels a bit like someone at the table suddenly flashing a card you weren't supposed to see.

This article is my attempt to formalise that intuition, markets are collective beliefs, prices are weighted expectations, and reports are pieces of evidence that changes the information set. You don't need to accept every claim for the game to change: credible details shift the odds, and force everyone to play the next street differently.

#### Why would someone reveal their hand?

In poker, showing your cards early is usually a mistake, unless you're getting paid for it (you're usually not). That's the key to why short sellers and activists publish: they're not volunteering information out of charity, they're trying to turn private work into a public catalyst. A short seller wants the table to notice the weak hand now, not at some distant showdown in the accounts. An activist wants everyone to see a better line of play, and, ideally, to help force it. Either way, the report is a strategic move: disclose evidence, shift beliefs, move the odds, and make the next actions by other players more predictable.

#### The game you're actually playing: ranges, not certainty

In poker, you almost never know what the other player has, so instead you form a view over a range of hands, and you update that view as new public information arrives, the flop, the turn, the river, plus the betting. Betting matters because it's a signal, but it's noisy: players bluff, players slowplay, players misclick; you're constantly trying to infer a hidden state from imperfect clues.

Markets work in a similar way, the "true state" of a company (durable economics vs fragile economics; clean accounting vs aggressive accounting; fair valuation vs major impairment; etc.) is never fully observable in real time. Investors carry priors, they watch public "cards" get dealt (earnings, filings, product launches, etc.), and they interpret everyone else's behaviour (flows, positioning, management tone, analyst upgrades/downgrades). Price is the running consensus that falls out of all of those partial signals.

A short report or activist letter is different from most market noise because it tries to add structured evidence to the information set: documents, reconciliations, channel checks, comparisons, a causal story. In poker terms, it's closer to seeing a card than watching a bet size. It doesn't end the hand, but it can collapse uncertainty in a way that changes optimal play immediately.

#### A minimal model: price as an expectation over states

To make that precise, let's pretend the world has only two states for a given company:

- $G$: "Good" (economics are real; accounts are broadly clean; no existential issue)
- $B$: "Bad" (economics overstated, or accounting/gov risk large enough to matter)

Let the value of the stock at eventual resolution be:

- $V_G$ if the company is in state $G$
- $V_B$ if it's in state $B$, with $V_G > V_B$

Let the market's prior probability that the company is bad be $p = \Pr(B)$. Then, ignoring discounting and risk premia (i.e., treating price as the risk-neutral expectation of terminal value), the price before any report arrives is simply the expected value:

$$P_0 = (1-p)V_G + pV_B$$

Those are our poker ranges: the market isn't choosing between "fraud" and "not fraud" as binary labels, it's weighting outcomes.

#### Reports as evidence: updating the probability, not declaring the truth

Now let's introduce a report $R$, the report is not a magical truth machine; it's evidence with some reliability. We can model that reliability with two numbers:

- $\alpha = \Pr(R \mid B)$ (how likely we are to see a report like this when the company is actually bad)
- $\beta = \Pr(R \mid G)$ (how likely we are to see a similar report even when the company is good, false positives, mistakes, weak cases, incentives)

Bayes' rule gives us the posterior probability that the company is bad after the report:

$$\Pr(B \mid R) = \frac{\Pr(R\mid B)\Pr(B)}{\Pr(R\mid B)\Pr(B)+\Pr(R\mid G)\Pr(G)} = \frac{\alpha p}{\alpha p + \beta (1-p)}$$

And the updated price becomes:

$$P_1 = (1-\Pr(B\mid R))V_G + \Pr(B\mid R)V_B$$

So the repricing caused by the report is

$$\Delta P = P_1 - P_0 = (\Pr(B\mid R)-p)(V_B - V_G)$$

Because $V_B - V_G < 0$, any increase in the probability of "bad" pushes price down, and the magnitude would depend on two levers:

1. **Belief shift:** how much the report moves $p$ to $\Pr(B\mid R)$
2. **Asymmetry:** how large the gap $V_G - V_B$ is

This is why the same style of report can move one stock 5% and another stock 50%. If the downside state is catastrophic (huge gap) and the prior was complacent (small $p$ that jumps), the move can be enormous even if nobody has proven anything yet.

#### The poker-friendly version

Poker players think naturally in odds, and quite conveniently Bayes looks quite nice in odds form.

Let's define prior odds that the company is bad: $O_0 = \frac{p}{1-p}$

Define the report's likelihood ratio (a compact way to talk about credibility): $LR = \frac{\Pr(R\mid B)}{\Pr(R\mid G)} = \frac{\alpha}{\beta}$

Then posterior odds are simply: $O_1 = O_0 \cdot LR$

The report multiplies the odds by a factor that depends on perceived credibility; if the market thinks a report is detailed, falsifiable, and hard to fake, $LR$ is high and the update is violent. However, if the market thinks it's thin, hand-wavy, or reputationally weak, $LR$ is closer to 1 and the update is muted.

#### Why the move is often bigger than the information alone

If the story ended with belief updates, market reactions would look quite a bit calmer: the report arrives, investors revise their probabilities, the stock reprices to the new expected value, and everyone goes back to work. In practice, the first-day move is often larger than what you'd predict from the report's "fair" informational content. That's not because markets suddenly forgot how to do math, it's because a report changes more than beliefs. So what are we missing? It's quite intuitive to infer that reports also change constraints, incentives, and the set of forced actions.

Poker has a similar dynamic, even if you see a card that makes your opponent more likely to be strong, the size of your next decision depends on stack sizes, position, risk tolerance, and whether you're already pot-committed.

**1) Belief updates happen on a thin slice of liquidity**

A report is a coordination event: everyone reads the same document at roughly the same time (comes up on your Bloomberg/Cap IQ/FactSet!), and everyone knows everyone else is reading it. That creates a rush to reprice in the same direction. But the order book at any instant is not the market, it's just the next few layers of marginal buyers and sellers. When the first wave of selling hits, the stock falls until it finds a buyer who is both willing and allowed to step in. This means the initial print can reflect temporary scarcity of risk-bearing capacity, not the final consensus view.

A simple way to write that in the same expectation framework would be to separate value from impact costs. Think of the traded price as:

$$P_{\text{trade}} = P^* - \lambda Q$$

where $P^*$ is the updated "fundamental" price from beliefs, $Q$ is net sell pressure (shares that must be sold quickly), and $\lambda$ is a liquidity/impact parameter (how steep the book is / how risk-averse liquidity providers are). Even if $P^*$ only moved modestly, a large $Q$ can push $P_{\text{trade}}$ far below it in the short run.

**2) Forced selling turns an information event into a positioning event**

Reports often trigger mechanical selling that has nothing to do with a fresh read of the evidence:

- risk limits get hit (VaR, drawdown, concentration),
- margin requirements increase as volatility spikes,
- long-only mandates forbid holding positions under investigation or with certain governance flags,
- some funds can't hold stocks below a market cap, price, or liquidity threshold

This creates a feedback loop (reflexivity): the report lowers price, volatility rises, constraints tighten, more selling.

In a stripped-down form, we can think of sell pressure itself as increasing when price falls:

$$Q = Q_0 + k(P_{\text{ref}} - P)$$

Substituting into the impact equation gives us

$$P = P^* - \lambda(Q_0 + k(P_{\text{ref}} - P))$$

Solving yields

$$P = \frac{P^* - \lambda Q_0 - \lambda k P_{\text{ref}}}{1-\lambda k}$$

When $\lambda k$ is large, feedback between price declines and forced selling can amplify the move.

**3) Uncertainty can rise even while information improves**

This sounds paradoxical but shows up constantly in markets, a credible report can reduce uncertainty about one dimension (there may be a serious issue here) while increasing uncertainty about resolution (how bad, how fast, what's the legal/regulatory path, what does the board do, etc.).

In option terms, implied volatility often jumps because the distribution of outcomes gets fatter in the tails, in poker terms, you may have learned your opponent's range is stronger than you thought, but you also realize you're heading toward a massive pot with future action you can't fully model.

A useful mean-variance shorthand is to think of price as decreasing in both expected value and the dispersion of outcomes:

$$P \approx \mathbb{E}[V] - \phi\,\mathrm{Var}(V)$$

where $\phi>0$ is a reduced-form way to capture risk aversion, leverage constraints, or limited risk-bearing capacity. This is not a structural asset-pricing identity, just a convenient way to express why greater uncertainty can push prices lower.

**4) Everyone updates, and everyone knows everyone updated**

A report not only changes your belief, it changes your belief about everyone else's belief. That matters because so much short-term pricing is about second-order effects: flows, hedges, and what the marginal buyer will do next.

In plain English: markets care about the posterior and about the speed and synchronization of the update, i.e. report is a synchronization shock.

**5) Management's next move is part of the hand**

After the reveal, the game is about the next streets. Management can rebut with facts, disclose more, hire advisors, change guidance, announce governance or capital allocation moves, or threaten litigation (sometimes credible, sometimes not).

Investors aren't only pricing "is the report true"; they're pricing "what happens next." In the earlier two-state setup, we can extend the model by allowing the report to affect the probability of different resolution paths. For example, let $C$ be a catalyst/resolution event (audit, regulator action, covenant breach, etc.). Then price is really:

$$P = \mathbb{E}[V \mid \text{info}] = \sum_{s \in \{G,B\}} \Pr(s \mid \text{info}) \cdot \mathbb{E}[V \mid s, \text{info}]$$

and $\mathbb{E}[V \mid s, \text{info}]$ can shift because the report changes timelines, financing terms, and strategic options.

#### Credibility is the likelihood ratio

In poker terms, not every reveal is equal, sometimes you literally see a hole card. Sometimes you catch a reflection in someone's sunglasses and convince yourself you saw a hole card. The market treats reports the same way: it's constantly asking "is this real evidence, or table talk?" A clean way to express that is with the likelihood ratio, basically the report's "credibility multiplier."

Let's start with the prior probability the company is in the bad state: $p = \Pr(B)$. Prior odds (bad vs good) are: $O_0 = \frac{p}{1-p}$

A report arrives: call it again $R$. The market's key question is: how much more likely is a report like this if the company is actually bad than if it's good? That quantity is the likelihood ratio:

$$LR = \frac{\Pr(R\mid B)}{\Pr(R\mid G)}$$

And the update in odds form is delightfully simple: $O_1 = O_0 \cdot LR$

So when people say "the market didn't buy it" or "this one hit different," what they're really describing is a low or high $LR$. Same document format, same PDF energy but wildly different credibility multipliers.

#### What makes $LR$ feel big?

We can translate credibility into a handful of very human heuristics, the market tends to assign a larger $LR$ when the report has:

**1) Falsifiable claims**
The strongest reports commit to their numbers and claims. They say "here is the number, here is the source, here is the reconciliation." Falsifiability matters because it reduces the chance the report exists in the good state (it lowers $\Pr(R\mid G)$), which pushes $LR$ up.

**2) Receipts that don't depend on vibes**
Screenshots of filings, contracts, invoices, regulatory docs, customer lists with methodology, shipping records, audit trails. Evidence that can be independently checked tends to raise $\Pr(R\mid B)$ and reduce $\Pr(R\mid G)$.

**3) A mechanism, not just a conclusion**
"Overvalued" is a take. "Here's the exact mechanism that makes the reported numbers impossible" is evidence. Mechanisms make it easier for others to verify, which markets love.

**4) A track record (reputational collateral)**
A reporter with past hits is implicitly staking something. You can think of this as the market believing their false positive rate is lower. In our earlier notation, that's a smaller $\beta=\Pr(R\mid G)$, and smaller $\beta$ means larger $LR=\alpha/\beta$.

**5) Third-party corroboration**
When independent parties confirm pieces, suppliers, customers, regulators, journalists, other analysts, the "good state" becomes harder to reconcile with the presence of the report. Again: $\Pr(R\mid G)$ shrinks, $LR$ grows.

#### And what makes $LR$ feel small?

**1) Claims that are basically untestable**
If the report reads like "trust me bro, my channel checks are spicy," markets usually translate that into a higher false positive probability.

**2) Sloppy errors**
One wrong chart doesn't invalidate everything, but it increases the perceived chance we'd see this report even when the company is fine, i.e., it raises $\Pr(R\mid G)$, shrinking $LR$.

**3) Motivated reasoning with thin evidence**
Markets already know the author has a position. That's fine. What gets punished is when the argument looks reverse-engineered from the position (looks pumped or the short equivalent basically).

#### The funny part: markets often trade the expected $LR$, not the truth

Right after a report drops, most participants haven't verified the whole thing. They're trading what they think the market will decide about credibility.

We can model that by admitting the market is uncertain about $LR$ itself. Let's suppose there are two credibility regimes:

- $H$: high-credibility report (big $LR_H$)
- $L$: low-credibility report (small $LR_L$)

Let $q=\Pr(H)$ be the market's probability that this report is the "real card reveal" kind. Strictly speaking, Bayesian updating requires combining the underlying conditional probabilities rather than averaging likelihood ratios. But as a practical market heuristic for us, participants often behave as if the effective multiplier were roughly

$$LR_{\text{eff}} \approx q\,LR_H + (1-q)\,LR_L$$

Early trading frequently reflects rapid changes in $q$ as investors skim the report, experts weigh in, and the company responds.

#### A couple thoughts on activism reports

Here's the neat part: once you see the "reveal-a-card" framing, activism letters rhyme a bit with short reports, but they are not exactly the same type of signal. A short report is trying to change your view of what the company is, while an activism letter is trying to change your view of what the company could become.

In poker language: a short report is closer to, "I think your hand is weaker than you think, and here's a card that proves it." An activism report is closer to, "Your hand might be fine, but you're playing it badly, and I can change how the hand gets played."

#### Two hidden variables, not one

For short reports we implicitly had a hidden state like $B$ vs $G$ (bad vs good). Activism is usually aimed at a different hidden variable:

- $A$: "activist outcome happens" (strategy changes, board changes, capital return, asset sale, governance fix)
- $S$: "status quo persists"

The market already has some baseline probability that the activist path actually materializes. Let's call it $\pi = \Pr(A)$. Then the simplest "activism pricing" version of our earlier model is:

$$P_0 = (1-\pi)V_S + \pi V_A$$

where $V_S$ is the value under the status quo and $V_A$ is the value if the activist plan succeeds (often $V_A > V_S$). An activism deck or letter is, in this setup, evidence that updates $\pi$. Not "is the company real?", but "is change likely, and is it feasible?"

#### Activism is an odds update on feasibility

Just like we've been doing, let the activism report be an event $R$ (a public campaign, a detailed presentation, a letter, or something else). The market asks: how likely is a campaign like this if success is genuinely plausible versus if it's mostly noise?

Define $\alpha = \Pr(R\mid A)$ and $\beta = \Pr(R\mid S)$. Then Bayes gives us:

$$\Pr(A\mid R) = \frac{\alpha \pi}{\alpha \pi + \beta (1-\pi)}$$

...and the updated price becomes:

$$P_1 = (1-\Pr(A\mid R))V_S + \Pr(A\mid R)V_A$$

Markets don't treat "someone wrote a spicy letter" as equal to "someone can actually force the issue." The $LR$ logic still runs the show:

$$LR = \frac{\Pr(R\mid A)}{\Pr(R\mid S)} = \frac{\alpha}{\beta}$$

A campaign feels like a high-$LR$ reveal when it comes with things that change the odds of success, not just the quality of the PowerPoint:

- a meaningful stake (and the willingness to add)
- credible coalition-building (other holders, proxy advisors)
- board-level leverage (vote math, governance structure, credible nominees)
- a realistic mechanism (asset sale is possible, buyback is fundable, strategy change is coherent)
- timing/catalysts (upcoming vote, earnings pressure, debt maturities, strategic review window)

In poker terms: it's not "I'm telling you I have aces", but more like "I put chips in, I have position, and you can see the ace."

#### The symmetry is useful (and a little funny)

Short reports and activism reports often get treated like totally different genres, one is "attack," one is "unlock value." But mechanically, they rhyme:

- Both are **information events**.
- Both try to **move the market's odds**.
- Both have an implied **credibility multiplier**.
- Both can create **second-order effects** (flows, forced selling/buying, volatility, management responses)

#### Management's response is a second reveal

After a report drops, the market is pricing the next move. In poker terms, the PDF is one revealed card... and then everyone immediately starts watching how the other player reacts. Do they snap-call? Tank? shove? quietly reach for more chips? Those behaviours contain information too.

In markets, management's response (or lack of one) is the next card.

#### A rebuttal is counter-evidence, not a verdict

Call the initial report event $R$. Now add a response signal $D$ (for "defence"): a press release, an 8-K, a call, a detailed point-by-point rebuttal, an internal investigation, hiring a top-tier auditor, announcing a strategic review, etc.

The market updates again:

$$\Pr(B\mid R, D) = \frac{\Pr(D\mid B, R)\Pr(B\mid R)}{\Pr(D\mid B, R)\Pr(B\mid R) + \Pr(D\mid G, R)\Pr(G\mid R)}$$

If you're more into poker than finance, we can define posterior odds after the report as $O_R = \frac{\Pr(B\mid R)}{1-\Pr(B\mid R)}$. Then the response multiplies those odds by another likelihood ratio:

$$LR_D = \frac{\Pr(D\mid B, R)}{\Pr(D\mid G, R)}$$

So: $O_{R,D} = O_R \cdot LR_D$

But, what counts as a strong response? That would be one with a high information content; strong here, doesn't mean loud, it means diagnostic, so the best response would be the one that makes one world more plausible than the other, something like concrete, checkable refutations, third-party validations, or one which narrows uncertainty ("Here are the exact claims that are wrong, here's why, and here's what we'll disclose next").

In the model, those are responses with a low probability under the "bad" world: they push $\Pr(D\mid B, R)$ down relative to $\Pr(D\mid G, R)$, making $LR_D$ small, which pulls bad-odds down.

Some responses are basically table talk, they can even backfire because they're more likely in the bad world than the good world; things such as vague denials with little substance, attacking motives instead of facts, immediately threatening lawsuits, etc. None of these prove wrongdoing, but they often make the "good world" less distinctive, which keeps $LR_D$ from helping.

Poker translation: if you truly saw the other guy flash a card, and he responds by giving a speech about how unfair poker is... you update.

#### Timing is part of the signal

Speed matters because it changes what the response can plausibly be.

- A detailed rebuttal in 2 hours can be impressive or suspicious (depending on the claim set)
- A careful response in 48-72 hours can read as "we actually checked"
- No real response for weeks, while the claims are concrete, tends to be interpreted as "they can't cleanly refute it"

If you want a simple way to write that: the market conditions on both the content and the lag $t$: $\Pr(B\mid R, D, t)$

For activism, the response signal is often an action that changes feasibility, such as management announcing a strategic review, replacing directors or refreshing the board, starting negotiations (or refusing to engage), or adopting defensive measures such as a poison pill.

If the activism success event is $A$, we can mirror the same update:

$$\Pr(A\mid R, D) = \frac{\Pr(D\mid A, R)\Pr(A\mid R)}{\Pr(D\mid A, R)\Pr(A\mid R) + \Pr(D\mid S, R)\Pr(S\mid R)}$$

#### Conclusion: the hand isn't over, but the odds just moved

The easiest way to stay sane around short reports and activism campaigns (to me, I'm just a newbie to the industry...) is to remember the poker version of what's happening. Most of the time, markets are playing ranges: imperfect information, noisy signals, lots of people pretending they're certain. Then a report drops and, if it's any good, it feels like someone just flashed a card you weren't supposed to see.

That doesn't mean the report is true in some courtroom sense, but it means the information set changed, and the table updates. In math terms, everyone is adjusting a probability and reweighting outcomes: $p$ moves, or $\pi$ moves, and price moves with it. The volatility, the gap, the chaos on day one? That's often the game's plumbing showing through, positioning, liquidity, constraints, and second-order reactions, not just a pure read of fundamentals.

Short reports and activism letters are also closer cousins than they look, one usually argues about what the company is (downside state). The other argues about what the company could be (upside path). Mechanically, they both try to do the same thing: change the market's odds with evidence, then let everyone scramble to play the next street.

So when the next PDF detonates one of your positions, the best mental posture is neither outrage nor blind faith. It's: what exactly was revealed, how credible is it, what would I expect to see next if it's right, and what would I expect to see next if it's wrong? Because the real showdown, regulators, audits, board actions, filings, cash flows, still comes later.

In other words: you don't have to know the whole hand to make better decisions... but you should probably stop pretending you didn't just see a card.
