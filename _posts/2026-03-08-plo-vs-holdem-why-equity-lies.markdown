---
layout: post
title: "Equity vs Realisation in PLO"
date: 2026-03-08
---

If you've played any Pot-Limit Omaha games, you've probably said it at least once: *"I had so much equity."* Nut flush draw, maybe a couple backdoors, felt like you couldn't be doing that badly... and then the hand somehow turns into a miserable fold on the turn, or a crying call that feels like lighting your money on fire.

That's the core trap of PLO: **equity is cheap, but realisation is expensive**.

Raw equity tells you how often you'd win **if everyone checked down to showdown**. But this very rarely happens in PLO. Position, stack depth, and the fact that pots go multiway mean your "40%" can behave more like "15%" in practice, because you don't get to see the river, you get paid poorly when you hit, or you get stacked when you hit the wrong way.

The other key lever is SPR (stack-to-pot ratio), in PLO this is basically the "difficulty setting of the hand". At low SPR, equity behaves more predictively because there aren't many decisions left: money goes in, cards run out, someone wins. At high SPR, equity gets distorted by future streets. You can have plenty of raw equity and still lose money because you get pushed off turns, get paid poorly when you hit, or reverse implied odds punish you when the board runs badly.

#### Position: Who Gets to Realise Equity in PLO

In PLO, position isn't a small convenience, almost like a realisation multiplier. The deeper the stacks and the more dynamic the board, the more the game turns into a contest over who gets to see the next card on reasonable terms.

When you're in position, your equity gets to exist. When you're out of position, your equity has to survive contact. What position really buys you is **options**: you can take free cards with draws, control pot size with medium-strength hands, build pots when you have nutted hands, and wait for information before committing money.

If a player checks to you, you decide whether this is a board to stab, check back, or set up favourable turn cards.

Out of position, the flow reverses. **You** become the player **put to the decision**. In PLO, being put to the decision often means facing **pot-sized pressure on the turn**. Your hand may technically still have equity, but continuing becomes unprofitable because the price is too high and the implied odds are fragile. This is where "I have 35--40%" turns into "I'm folding the turn again." Those folds are a hidden tax on raw equity.

A clean example could be the following. Suppose you hold A♠ Q♦ 7♣ 2♥ on the flop K♠ 8♠ 3♦. You have the nut flush draw, but the side cards are weak; your raw equity against many one-pair or set-heavy ranges might look respectable. That's the trick.

In position, if the preflop raiser checks you can take a free card, if they bet you can call with a clearer plan, and scare turns may let you apply pressure with blockers. Out of position you are far more likely to face pot-sized bets, check-raises, and difficult turn decisions. Even when you hit the flush, runouts can become ugly — paired boards, straights completing, action dying on obvious cards — making it harder to value bet safely, control the pot, or avoid paying off when the board turns against you.

#### From Equity to EV: A Simple Realisation Model

To understand why **40% equity can feel like 15%**, it helps to separate two ideas.

- Raw equity $E$: your probability of winning if all remaining cards were dealt with no further betting
- Realisation $R$: the fraction of that equity you actually convert into money given betting, position, and future streets

A useful mental model could be:

$$E_{\text{effective}} = R \cdot E$$

where $R \in [0,1]$. When you are in position, heads-up, and at low SPR, $R$ tends to be higher because you can see more cards and choose pot geometry. When you are out of position, deep, and multiway, $R$ drops because you get denied cards, face expensive bets, or realise your equity poorly.

#### Connecting Equity to Money

Very loosely, EV depends on how often you win, how big the pot is when you win, and how much you must invest along the way. A simple heuristic expression is:

$$EV \approx R \cdot E \cdot W - C$$

where $W$ = average pot won when you win and $C$ = total investment required to realise your equity. This equation isn't solver-perfect, it's just a way to see that **equity alone doesn't determine EV** (at least for me).

#### Numerical Example

Suppose on the flop $E = 0.40$. Now let's compare two environments.

IP, heads-up:

$$R = 0.70$$

$$E_{\text{effective}} = 0.70 \cdot 0.40 = 0.28$$

OOP, deep, multiway:

$$R = 0.35$$

$$E_{\text{effective}} = 0.35 \cdot 0.40 = 0.14$$

Same raw equity, but your usable equity is cut in half.

#### Where Do We Lose Realisation?

In practice, our $R$ gets reduced by three mechanisms.

**1. Denial** — you fold before showdown even though your hand had equity.

**2. Reverse implied odds** — you improve but still lose a large pot. This is common in PLO when flushes run into higher flushes, straights run into redraws, or boards pair after you improve.

**3. Under-realised value** — you hit but cannot extract value, because obvious draws complete, the board pairs, or action dies on scary rivers. Bare nut draws with weak side cards are deceptive for exactly this reason: your raw equity is real, but the path to collecting it is narrow.

#### Multiway Pots: Why Equity Gets Taxed

Multiway pots dramatically change the game. Even if your hand beats one opponent often, beating multiple opponents simultaneously is much harder. As more players enter the pot, the chance someone holds a very strong hand increases, nutted ranges become denser, and dominated draws become more dangerous. The probability of winning therefore falls quickly as the number of opponents increases:

$$P(\text{win}) = P(\text{beat all opponents})$$

which decreases rapidly with each additional player. Just as importantly, multiway pots also reduce realisation because players fold less, large draws collide, and nut hands become more common.

#### Equity Distribution vs Range

Another key difference between PLO and Hold'em is how equity is distributed across ranges. In Hold'em, strong hands often dominate weaker ones — AA vs AK has roughly $E \approx 0.92$. In PLO, equities compress dramatically; many hands share similar equity on the flop: big draws, sets, combo draws, wrap straight draws.

This means that raw equity alone tells you much less about who is ahead. Instead, what matters is equity distribution: who holds the **top of range**, who holds the **nut advantage**, and who has **redraws**. A player may have similar average equity but far more high-equity hands, which translates into much higher EV.

#### Nut Advantage

Because equities run close in PLO, the player who holds the **nuts more often** gains a large strategic advantage. Nut advantage means your range contains more nut straights, nut flushes, top sets or redraws to stronger hands. This matters because large bets in PLO are justified by polarisation around the nuts. If your range contains more nut hands, you can bet larger, apply pressure and force opponents to fold equity. Nut advantage therefore increases realisation by increasing fold equity and allowing larger value bets.

#### Visibility of the Nuts

A subtle but important concept in PLO is visibility of the nuts. Many PLO boards make the nuts obvious: four-straight boards, flush completing boards, paired boards. When the nuts are **obvious**, players usually become cautious. This reduces $R_{\text{showdown}}$ because even when you make a strong hand, opponents may refuse to pay. Conversely, boards where the nuts are less visible allow stronger hands to extract more value. This is another way your realisation gets distorted in PLO.

#### SPR: The Difficulty Setting of Realisation

SPR measures how much leverage remains in a hand:

$$SPR = \dfrac{S}{P}$$

where $S$ = effective stack and $P$ = current pot.

When $SPR \lesssim 2\text{--}3$, stacks go in quickly, fewer decisions remain, so realisation tends to be higher — you commit money and let equity run. When $SPR \gtrsim 6\text{--}10$, the same raw equity can produce very different EV depending on position, nuttiness and redraw potential. More streets mean more opportunities to get pushed off hands, pay off stronger hands or lose value when obvious draws complete. Turn decisions become especially important because pot-sized bets drastically change the pot geometry.

Suppose your flop equity is $E \approx 0.40$. At low SPR with $R = 0.60$: $E_{\text{effective}} = 0.60 \cdot 0.40 = 0.24$. At high SPR, OOP, multiway with $R = 0.30$: $E_{\text{effective}} = 0.30 \cdot 0.40 = 0.12$. Same equity on paper, but your usable equity is halved. That's why deep PLO often feels like you're constantly folding equity: the game gives you theoretical shares (yeah!!), then charges you rent to access them (ouch).

#### Some Practical Takeaways

Our simple model is $E_{\text{effective}} = R \cdot E$. Raw equity only matters if you can **convert it into money**. Some practical heuristics stemming from this:

- **Treat position as a realisation multiplier.** If you are OOP, assume $R$ is lower by default. You will face more spots where continuing becomes unprofitable.
- **High SPR increases denial.** More streets create more opportunities to fold before the river.
- **Plan the turn before calling the flop.** If you call the flop knowing you will fold most blank turns to pot-sized bets, you are effectively investing in the denial term of the equation.
- **Multiway pots compress EV.** More players means stronger ranges, more nutted hands and lower realisation.
- **Prefer equity with structure.** Hands with **nuttiness and redraws** maintain higher $R$; bare nut draws without side cards often have good raw equity but fragile realisation.
- **Pot geometry matters.** When you are in position you can control future investment $C$ and final pot size $W$. Out of position you are more likely to face large bets where $EV \approx R \cdot E \cdot W - C$ turns negative because $C$ grows while $R$ shrinks.
- **Know your good rivers.** If a draw hits but cannot value bet safely, or hits into boards where action dies, its realised value is lower than its raw equity suggests.

#### Closing Thoughts

The core trap of PLO is thinking in raw equity when the real game is **realisation**. Your hand can have plenty of $E$ and still lose money if $R$ is low. Position, SPR, nut advantage, and board structure all determine whether your equity actually turns into EV.

In other words: in PLO you don't just have equity — you have to **earn the right to realise it**.
