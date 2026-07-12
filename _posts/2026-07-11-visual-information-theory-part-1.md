---
layout: distill
title: "Visual Information Theory, Part 1: Probability, Codes, and Entropy"
description: A visual and mathematically rigorous introduction to information content, entropy, cross-entropy, and KL divergence — for readers who want the intuition and the derivations.
tags: information-theory entropy tutorial
giscus_comments: true
date: 2026-07-11
featured: true

authors:
  - name: Ameenudeen P E
    url: "/"
    affiliations:
      name: Indian Institute of Science, Bangalore

bibliography: 2026-07-11-visual-information-theory.bib

toc:
  - name: Why information theory
  - name: "Information: reducing uncertainty"
  - name: Visualizing joint distributions
  - name: "Entropy: the cost of encoding"
    subsections:
      - name: Prefix codes and the space of codewords
      - name: The optimal codeword length
      - name: Putting it together
  - name: Redundancy and maximum entropy
  - name: Typical sequences and the AEP
  - name: Cross-entropy
  - name: KL divergence
  - name: What's next
---

## Why information theory

In the 1940s, Claude Shannon gave the informal idea of "information" a precise mathematical footing<d-cite key="shannon1948mathematical"></d-cite>. The resulting theory answers questions that feel intuitive but are hard to pin down without it: How uncertain am I about an outcome? How much does knowing one thing tell me about another? How different are two beliefs about the world?

This two-part post builds up the core machinery of information theory — entropy, cross-entropy, KL divergence, joint and conditional entropy, mutual information, and the entropy rate of a stochastic process — visually and rigorously at the same time. It closely follows two sources. The first is Christopher Olah's essay *Visual Information Theory*, which builds intuition for entropy and related quantities through codes and areas rather than through the sums directly <d-cite key="olah2015visual"></d-cite>. The second is Pinkard and Waller's *A visual introduction to information theory*, a more recent, notation-careful tutorial that formalizes many of the same ideas with figures grounded in a simple marble-drawing experiment <d-cite key="pinkard2022visual"></d-cite>. Part 1 (this post) covers single-variable quantities: information content, entropy, redundancy, typical sequences, cross-entropy, and KL divergence. [Part 2]({% post_url 2026-07-12-visual-information-theory-part-2 %}) covers quantities involving two or more variables — joint entropy, conditional entropy, mutual information — and closes with the entropy rate of a stochastic process.

Throughout, we assume only familiarity with basic probability: random variables, joint and conditional distributions, and expectation.

## Information: reducing uncertainty

Gaining information means having your uncertainty about something reduced. If I tell you the outcome of a coin flip you haven't seen, I've resolved all your uncertainty about it. If I tell you something you already knew for certain, I've given you no information at all.

Consider drawing a marble at random from an urn containing marbles of four colors, with replacement, where

$$
p(\texttt{blue}) = \tfrac{1}{2}, \quad p(\texttt{gray}) = \tfrac{1}{4}, \quad p(\texttt{yellow}) = \tfrac{1}{8}, \quad p(\texttt{green}) = \tfrac{1}{8}.
$$

Suppose you learn that the marble drawn is *not* blue. That single fact rules out half of the probability mass, leaving a distribution renormalized over the remaining three colors. Learning a fact that was less likely to be true rules out *more* probability mass, and hence carries more information — this is precisely why rare events are more informative than common ones <d-cite key="pinkard2022visual"></d-cite>.

We can make this quantitative. If ruling out half the probability mass corresponds to one unit of information, then the information content of an outcome $$x$$ with probability $$p(x)$$ is

$$
I(x) = \log_2 \frac{1}{p(x)} \, ,
$$

measured in **bits**. An outcome with probability $$\tfrac12$$ carries exactly 1 bit; an outcome with probability $$\tfrac18$$ carries 3 bits, because learning it happened is equivalent to eliminating three successive halvings of the probability mass. The **entropy** of a random variable $$X$$ is the probability-weighted average information content of its outcomes:

$$
H(X) = \sum_{x \in \mathcal{X}} p(x) \log_2 \frac{1}{p(x)} \, .
$$

Entropy is the expected number of bits of surprise you get, on average, from observing $$X$$. It is maximized when probability is spread as evenly as possible across outcomes, and it is zero exactly when the outcome is certain in advance ($$p(x) = 1$$ for some $$x$$) <d-cite key="pinkard2022visual"></d-cite>.

<div class="l-body">
<svg viewBox="0 0 620 320" xmlns="http://www.w3.org/2000/svg" style="max-width:100%; height:auto; font-family: sans-serif;">
<style>.axis{stroke:currentColor;stroke-width:1;opacity:0.4;} .grid{stroke:currentColor;stroke-width:1;opacity:0.12;} .lbl{font-size:12px;fill:currentColor;} .lbl2{font-size:11px;fill:currentColor;} .legend{font-size:12px;fill:currentColor;}</style>
<line x1="55" y1="270.0" x2="565" y2="270.0" class="grid"/>
<text x="45" y="274.0" text-anchor="end" class="lbl2">0.00</text>
<line x1="55" y1="210.0" x2="565" y2="210.0" class="grid"/>
<text x="45" y="214.0" text-anchor="end" class="lbl2">0.25</text>
<line x1="55" y1="150.0" x2="565" y2="150.0" class="grid"/>
<text x="45" y="154.0" text-anchor="end" class="lbl2">0.50</text>
<line x1="55" y1="90.0" x2="565" y2="90.0" class="grid"/>
<text x="45" y="94.0" text-anchor="end" class="lbl2">0.75</text>
<line x1="55" y1="30.0" x2="565" y2="30.0" class="grid"/>
<text x="45" y="34.0" text-anchor="end" class="lbl2">1.00</text>
<text x="575" y="274.0" text-anchor="start" class="lbl2">0</text>
<text x="575" y="214.0" text-anchor="start" class="lbl2">1</text>
<text x="575" y="154.0" text-anchor="start" class="lbl2">2</text>
<text x="575" y="94.0" text-anchor="start" class="lbl2">3</text>
<text x="575" y="34.0" text-anchor="start" class="lbl2">4</text>
<line x1="55" y1="30" x2="55" y2="270" class="axis"/>
<line x1="565" y1="30" x2="565" y2="270" class="axis"/>
<line x1="55" y1="270" x2="565" y2="270" class="axis"/>
<text x="18" y="150.0" text-anchor="middle" class="lbl" transform="rotate(-90 18 150.0)">Probability</text>
<text x="606" y="150.0" text-anchor="middle" class="lbl" transform="rotate(-90 606 150.0)">Codeword length (bits)</text>
<rect x="74.1" y="150.0" width="40.8" height="120.0" fill="#5470C6" fill-opacity="0.75"/>
<rect x="122.6" y="210.0" width="40.8" height="60.0" fill="#EE6666" fill-opacity="0.75"/>
<text x="118.8" y="288" text-anchor="middle" class="lbl">dog (p=0.5)</text>
<rect x="201.6" y="210.0" width="40.8" height="60.0" fill="#5470C6" fill-opacity="0.75"/>
<rect x="250.1" y="150.0" width="40.8" height="120.0" fill="#EE6666" fill-opacity="0.75"/>
<text x="246.2" y="288" text-anchor="middle" class="lbl">cat (p=0.25)</text>
<rect x="329.1" y="240.0" width="40.8" height="30.0" fill="#5470C6" fill-opacity="0.75"/>
<rect x="377.6" y="90.0" width="40.8" height="180.0" fill="#EE6666" fill-opacity="0.75"/>
<text x="373.8" y="288" text-anchor="middle" class="lbl">fish (p=0.125)</text>
<rect x="456.6" y="240.0" width="40.8" height="30.0" fill="#5470C6" fill-opacity="0.75"/>
<rect x="505.1" y="90.0" width="40.8" height="180.0" fill="#EE6666" fill-opacity="0.75"/>
<text x="501.2" y="288" text-anchor="middle" class="lbl">bird (p=0.125)</text>
<rect x="55" y="6" width="12" height="12" fill="#5470C6" fill-opacity="0.75"/>
<text x="73" y="16" class="legend">Probability</text>
<rect x="185" y="6" width="12" height="12" fill="#EE6666" fill-opacity="0.75"/>
<text x="203" y="16" class="legend">Optimal codeword length (bits)</text>
</svg>
</div>
<div class="caption">
  Probability and optimal codeword length for four events. The area of each bar (probability × length) is that event's contribution to the entropy; the total area is the entropy itself, 1.75 bits. Data from Olah's dog/cat/fish/bird example <d-cite key="olah2015visual"></d-cite>.
</div>

## Visualizing joint distributions

Before going further, it helps to have a way of picturing distributions over *two* variables at once <d-cite key="olah2015visual"></d-cite>. Suppose we track the weather (sunny 75% of the time, raining 25%) and clothing (t-shirt 62% of the time, coat 38%). If the two are independent — knowing the weather tells us nothing about clothing choice — the joint distribution factors as $$p(x,y) = p(x)\,p(y)$$, and a grid of the joint probabilities looks like a simple product of the two marginals: every row is a scaled copy of every other row.

<div class="l-body">
<svg viewBox="0 0 460 230" xmlns="http://www.w3.org/2000/svg" style="max-width:100%; height:auto;">
  <style>
    .gridlabel { font-family: sans-serif; font-size: 12px; fill: currentColor; }
    .gridtitle { font-family: sans-serif; font-size: 14px; font-weight: 600; fill: currentColor; }
  </style>
  <text x="120" y="18" text-anchor="middle" class="gridtitle">Independent</text>
  <rect x="20" y="30" width="124" height="120" fill="#5470C6" fill-opacity="0.55" stroke="currentColor"/>
  <rect x="144" y="30" width="76" height="120" fill="#5470C6" fill-opacity="0.30" stroke="currentColor"/>
  <rect x="20" y="150" width="124" height="40" fill="#5470C6" fill-opacity="0.30" stroke="currentColor"/>
  <rect x="144" y="150" width="76" height="40" fill="#5470C6" fill-opacity="0.15" stroke="currentColor"/>
  <text x="82" y="95" text-anchor="middle" class="gridlabel">sun, t-shirt</text>
  <text x="182" y="95" text-anchor="middle" class="gridlabel">sun, coat</text>
  <text x="82" y="174" text-anchor="middle" class="gridlabel">rain, t-shirt</text>
  <text x="182" y="174" text-anchor="middle" class="gridlabel">rain, coat</text>
  <text x="120" y="210" text-anchor="middle" class="gridlabel">p(x,y) = p(x)&#183;p(y)</text>

  <text x="350" y="18" text-anchor="middle" class="gridtitle">Correlated</text>
  <rect x="250" y="30" width="149.3" height="120" fill="#91CC75" fill-opacity="0.5" stroke="currentColor"/>
  <rect x="399.3" y="30" width="50.7" height="120" fill="#91CC75" fill-opacity="0.15" stroke="currentColor"/>
  <rect x="250" y="150" width="48.0" height="40" fill="#91CC75" fill-opacity="0.15" stroke="currentColor"/>
  <rect x="298.0" y="150" width="152.0" height="40" fill="#91CC75" fill-opacity="0.65" stroke="currentColor"/>
  <text x="324" y="95" text-anchor="middle" class="gridlabel">sun, t-shirt</text>
  <text x="424" y="95" text-anchor="middle" class="gridlabel" font-size="10">sun, coat</text>
  <text x="274" y="174" text-anchor="middle" class="gridlabel" font-size="10">rain, t-shirt</text>
  <text x="374" y="174" text-anchor="middle" class="gridlabel">rain, coat</text>
  <text x="350" y="210" text-anchor="middle" class="gridlabel">boundary shifts per row</text>
</svg>
</div>
<div class="caption">
  Left: independent variables produce a grid where the t-shirt/coat boundary sits at the same place in every row — a single straight line top to bottom, since the split doesn't depend on the weather. Right: correlated variables (it's more likely to be a coat on a rainy day) shift that boundary row by row — the "rain, coat" cell swells at the expense of "sun, coat", and the split is no longer a single straight line.
</div>

When the variables interact, some cells of the grid swell with extra probability (it's more likely to wear a coat when it's raining) at the expense of others. The fundamental identity connecting joint and conditional probability, $$p(x,y) = p(x)\cdot p(y\mid x)$$, lets us factor any joint distribution one variable at a time — and it is the seed from which joint entropy and conditional entropy (Part 2) will grow.

## Entropy: the cost of encoding

Entropy has a second, equally important interpretation: it is the *shortest possible average length*, in bits, of a code for a sequence of outcomes from a distribution <d-cite key="pinkard2022visual"></d-cite><d-cite key="olah2015visual"></d-cite>. This is worth deriving carefully, because the derivation is what makes the formula feel inevitable rather than arbitrary.

Suppose we want to communicate a sequence of words drawn from a small vocabulary — say, an imaginary friend who only ever says "dog," "cat," "fish," or "bird," with probabilities $$\tfrac12, \tfrac14, \tfrac18, \tfrac18$$ <d-cite key="olah2015visual"></d-cite>. A **code** assigns each word a binary codeword; to send a message we concatenate the codewords for each word in sequence.

### Prefix codes and the space of codewords

If every codeword has the same length, decoding is trivial — split the bitstream every $$k$$ bits. But we'd like common words (like "dog") to get *short* codewords, so the average message is short. This creates a subtlety: with variable-length codewords, how does the receiver know where one codeword ends and the next begins?

The answer is the **prefix property**: no codeword may be a prefix of another. A code with this property is called a **prefix code**, and it is always uniquely decodable — you can read a bitstream left to right and unambiguously identify each codeword as soon as its pattern is complete.

The prefix property has a cost. Choosing the codeword `01` forbids every longer codeword that starts with `01` — `010`, `0110101`, and so on — because they would be ambiguous with it. A quarter of all possible bitstrings begin with `01`, so choosing it as a codeword "spends" a quarter of the total space of possible codewords. In general, a codeword of length $$L$$ costs $$2^{-L}$$ of the total space <d-cite key="olah2015visual"></d-cite>.

The following binary tree shows one valid prefix code for the four-word vocabulary: `0` for dog, `10` for cat, `110` for fish, `111` for bird. Every codeword is a leaf, and no codeword is an ancestor of another — that's the prefix property, drawn as a tree.

<div class="l-body">
<svg viewBox="0 0 500 220" xmlns="http://www.w3.org/2000/svg" style="max-width:100%; height:auto;">
  <style>
    .node { fill: none; stroke: currentColor; stroke-width: 1.5; }
    .leaf { fill: #5470C6; fill-opacity: 0.15; stroke: currentColor; stroke-width: 1.5; }
    .lbl { font-family: sans-serif; font-size: 13px; fill: currentColor; text-anchor: middle; }
    .elbl { font-family: sans-serif; font-size: 12px; fill: currentColor; text-anchor: middle; }
  </style>
  <!-- root -->
  <circle cx="60" cy="20" r="4" fill="currentColor"/>
  <!-- edges -->
  <line x1="60" y1="20" x2="60" y2="90" class="node"/>
  <line x1="60" y1="20" x2="320" y2="90" class="node"/>
  <line x1="320" y1="90" x2="230" y2="150" class="node"/>
  <line x1="320" y1="90" x2="410" y2="150" class="node"/>
  <line x1="410" y1="150" x2="350" y2="200" class="node"/>
  <line x1="410" y1="150" x2="450" y2="200" class="node"/>

  <text x="35" y="58" class="elbl">0</text>
  <text x="185" y="50" class="elbl">1</text>
  <text x="265" y="118" class="elbl">0</text>
  <text x="375" y="118" class="elbl">1</text>
  <text x="368" y="175" class="elbl">0</text>
  <text x="442" y="175" class="elbl">1</text>

  <rect x="30" y="90" width="60" height="34" rx="6" class="leaf"/>
  <text x="60" y="111" class="lbl">dog: 0</text>

  <rect x="195" y="150" width="70" height="34" rx="6" class="leaf"/>
  <text x="230" y="171" class="lbl">cat: 10</text>

  <rect x="310" y="192" width="80" height="26" rx="6" class="leaf"/>
  <text x="350" y="209" class="lbl" font-size="12">fish: 110</text>

  <rect x="410" y="192" width="80" height="26" rx="6" class="leaf"/>
  <text x="450" y="209" class="lbl" font-size="12">bird: 111</text>
</svg>
</div>
<div class="caption">
  A prefix code for {dog, cat, fish, bird}. Each word sits at a leaf; the path from the root spells out its codeword. Because every codeword is a leaf, none is a prefix of another.
</div>

### The optimal codeword length

Think of building a code as spending a fixed budget: buying a codeword of length $$L$$ costs $$2^{-L}$$ of the total space of codewords, and using it costs us $$p(x) \cdot L$$ extra bits in our average message length, since it's used a $$p(x)$$ fraction of the time. The natural strategy — spend a fraction $$p(x)$$ of the budget on the codeword for $$x$$ — turns out to be *optimal*, not merely reasonable <d-cite key="olah2015visual"></d-cite>. Olah proves this with a marginal argument: at the natural allocation, the benefit-to-cost ratio of shortening any single codeword is exactly 1, the same for every codeword; perturbing away from it (spending $$\epsilon$$ more on one codeword and $$\epsilon$$ less on another) unbalances the ratios and creates an incentive to shift back. Since this holds for every pair of codewords, the natural allocation cannot be improved.

If we spend $$p(x)$$ of the budget on the codeword for $$x$$, and a codeword of length $$L$$ costs $$2^{-L}$$, then solving $$2^{-L} = p(x)$$ for $$L$$ gives the optimal codeword length:

$$
L(x) = \log_2 \frac{1}{p(x)} \, .
$$

This is exactly the information content of $$x$$ from the previous section — no coincidence. The optimal code assigns each outcome a codeword whose length equals its information content in bits.

### Putting it together

The average codeword length under the optimal code is, by definition, the entropy:

$$
H(X) = \sum_{x} p(x)\, L(x) = \sum_{x} p(x) \log_2 \frac{1}{p(x)} \, .
$$

For our dog/cat/fish/bird example this works out to $$\tfrac12(1) + \tfrac14(2) + \tfrac18(3) + \tfrac18(3) = 1.75$$ bits — and no code, however clever, can do better on average <d-cite key="olah2015visual"></d-cite>. This is a genuine lower bound: **entropy is the shortest possible average encoding length for a sequence of outcomes from a given distribution**, a fact known as the source coding theorem.

One wrinkle: optimal codeword lengths are frequently *fractional* (e.g. $$\log_2 \tfrac{1}{0.71} \approx 0.49$$ bits), which is meaningless for a single codeword — you can't send half a bit. But if you encode *several* draws jointly, ideal lengths add, and the rounding overhead per event shrinks toward zero as the number of jointly-encoded events grows <d-cite key="olah2015visual"></d-cite>. There is a real sense in which fractional bits are achievable on average, even though no single message can have a fractional length; we will use this idea again in Part 2.

## Redundancy and maximum entropy

Entropy is maximized when probability is spread as evenly as possible over the outcome space $$\mathcal{X}$$. In that case,

$$
H_{\max}(\mathcal{X}) = \log_2 |\mathcal{X}| \, ,
$$

where $$|\mathcal{X}|$$ is the number of possible outcomes <d-cite key="pinkard2022visual"></d-cite>. The gap between this ceiling and the actual entropy of a variable is its **redundancy**:

$$
W(X) = H_{\max}(\mathcal{X}) - H(X) \, .
$$

Redundancy quantifies how much shorter our messages become because the distribution is *not* uniform — the more concentrated the probability mass, the larger the redundancy, and the more compressible the source. A deterministic variable ($$p(x)=1$$ for one outcome) has zero entropy and maximum possible redundancy; a uniform variable has zero redundancy, because there is nothing left to exploit.

## Typical sequences and the AEP

Entropy governs a length-$$N$$ i.i.d. sequence too: the total information content of $$N$$ independent draws is $$N \cdot H(X)$$ on average. But individual sequences vary enormously in *actual* information content — an all-`blue` sequence (the single most probable outcome) can be far cheaper to encode than a "typical" one, and far more expensive than a maximally rare one <d-cite key="pinkard2022visual"></d-cite>.

A **typical sequence** is one whose information content is close to this average: for small $$\epsilon > 0$$,

$$
H(X) - \epsilon \ \le\ -\frac{1}{N}\log p(x_1, \ldots, x_N) \ \le\ H(X) + \epsilon \, .
$$

As $$N \to \infty$$, the **asymptotic equipartition property (AEP)** kicks in: almost all of the probability mass concentrates onto the typical set, regardless of how small $$\epsilon$$ is, and every typical sequence has probability $$\approx 2^{-NH(X)}$$. Since probabilities sum to 1, there must be $$\approx 2^{NH(X)}$$ typical sequences. This is precisely what makes lossless compression at rate $$H(X)$$ achievable: a scheme that assigns a unique length-$$NH(X)$$ binary string to every typical sequence, and ignores the (vanishingly probable) rest, is lossless in the limit — and no scheme can reliably do better <d-cite key="pinkard2022visual"></d-cite>.

## Cross-entropy

Now suppose two people communicate using the *same* words but *different* frequencies. Bob mostly talks about dogs; his wife Alice mostly talks about cats. Bob's code — optimized for his own distribution $$p$$ — is suboptimal when Alice uses it to encode her distribution $$q$$, because it assigns short codewords to words Alice rarely uses <d-cite key="olah2015visual"></d-cite>.

The average message length when encoding events from $$q$$ using the code optimized for $$p$$ is the **cross-entropy**:

$$
H_p(q) = \sum_x q(x) \log_2 \frac{1}{p(x)} \, .
$$

Cross-entropy is not symmetric — $$H_p(q) \neq H_q(p)$$ in general — and this asymmetry is not a technicality; it is the whole point. $$H_q(p)$$ is large exactly when there's an outcome common under $$p$$ but rare under $$q$$: that outcome gets an unnecessarily long codeword, which hurts badly because $$p$$ uses it often. Whether the "large" direction is $$H_p(q)$$ or $$H_q(p)$$ depends on which distribution is doing the frequent using and which one built the code.

Cross-entropy is always at least the entropy of the distribution being encoded, $$H_p(q) \ge H(q)$$, with equality iff $$p = q$$. This makes it a natural, if asymmetric, measure of how different two distributions are — and it is why cross-entropy is the workhorse loss function for classification in machine learning: minimizing $$H_p(q)$$ where $$q$$ is the true label distribution and $$p$$ is the model's predicted distribution directly penalizes the model for being confidently wrong <d-cite key="olah2015visual"></d-cite>.

## KL divergence

The excess length caused by using the wrong code — the gap between cross-entropy and entropy — is the **Kullback–Leibler (KL) divergence**:

$$
D_q(p) = H_q(p) - H(p) = \sum_x p(x) \log_2 \frac{p(x)}{q(x)} \, .
$$

KL divergence is zero exactly when $$p = q$$ and grows as the two distributions diverge, which is why it behaves like a "distance" between distributions (though it is not symmetric and does not satisfy the triangle inequality, so it is not a metric in the strict sense) <d-cite key="olah2015visual"></d-cite>. It shows up constantly whenever we want one distribution to be close to another — variational inference, information geometry, and, again, machine learning, where minimizing $$D_q(p)$$ between a predicted and target distribution is equivalent to minimizing cross-entropy alone (since $$H(p)$$ doesn't depend on the model).

## What's next

We now have the vocabulary for a single random variable: information content, entropy, redundancy, cross-entropy, and KL divergence. [Part 2]({% post_url 2026-07-12-visual-information-theory-part-2 %}) extends all of this to **two or more variables** — joint entropy, conditional entropy, and mutual information — and finishes with the **entropy rate** of a stochastic process, the natural generalization of entropy to sequences that aren't independent and identically distributed.

For a fuller treatment than either source attempts, Shannon's original paper remains remarkably readable <d-cite key="shannon1948mathematical"></d-cite>, and Cover & Thomas's *Elements of Information Theory* is the standard graduate reference <d-cite key="cover2006elements"></d-cite>.
