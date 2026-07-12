---
layout: distill
title: "Visual Information Theory, Part 2: Joint Entropy, Mutual Information, and Stochastic Processes"
description: Extending entropy to two or more variables — joint entropy, conditional entropy, mutual information, fractional bits, and the entropy rate of a stochastic process.
tags: information-theory entropy tutorial
giscus_comments: true
date: 2026-07-12
featured: true

chart:
  chartjs: true

authors:
  - name: Ameenudeen P E
    url: "/"
    affiliations:
      name: Indian Institute of Science, Bangalore

bibliography: 2026-07-11-visual-information-theory.bib

toc:
  - name: Recap
  - name: Joint entropy
  - name: Conditional entropy
  - name: Mutual information
    subsections:
      - name: Pointwise mutual information
      - name: How the pieces fit together
  - name: Variation of information
  - name: Fractional bits, revisited
  - name: Entropy rate of a stochastic process
    subsections:
      - name: Two equivalent definitions
      - name: Redundancy of a stochastic process
  - name: Conclusion
---

## Recap

[Part 1]({% post_url 2026-07-11-visual-information-theory-part-1 %}) built up the vocabulary for a single random variable: the information content $$\log_2 \frac{1}{p(x)}$$ of an outcome, entropy $$H(X)$$ as its probability-weighted average, redundancy, cross-entropy, and KL divergence. All of it concerned one variable at a time. Most interesting questions, though, involve *relationships* between variables: how much does today's weather tell us about tomorrow's? How much do two random variables share? This post extends entropy to two (or more) variables, following the same two sources as Part 1 — Olah's essay <d-cite key="olah2015visual"></d-cite> and Pinkard & Waller's tutorial <d-cite key="pinkard2022visual"></d-cite> — and ends with the entropy rate, which generalizes entropy to sequences that are not independent and identically distributed.

## Joint entropy

The simplest extension is to ask how much information is needed to communicate the outcome of *two* variables together. If we flatten the joint distribution $$p(x,y)$$ over the product space $$\mathcal{X} \times \mathcal{Y}$$ and treat it as a distribution over a single combined variable, entropy applies unchanged:

$$
H(X,Y) = \sum_{x \in \mathcal{X}} \sum_{y \in \mathcal{Y}} p(x,y) \log_2 \frac{1}{p(x,y)} \, .
$$

This is the **joint entropy** — the average number of bits needed to communicate both $$X$$ and $$Y$$ using a code built for their joint distribution <d-cite key="pinkard2022visual"></d-cite><d-cite key="olah2015visual"></d-cite>. When $$X$$ and $$Y$$ are independent, $$p(x,y) = p(x)p(y)$$, and substituting this in shows $$H(X,Y) = H(X) + H(Y)$$: independent information simply adds. When they are dependent, the joint entropy is *less* than the sum of the individual entropies — some information is shared, and we shouldn't have to pay for it twice. Quantifying exactly how much is shared is the job of mutual information, below.

## Conditional entropy

Suppose you already know $$Y$$. How much *more* information do you need, on average, to also learn $$X$$? This is the **conditional entropy** $$H(X \mid Y)$$: the uncertainty remaining in $$X$$ once $$Y$$ is known.

Start at a single point: if we already know $$Y = y$$, the information needed to learn $$X$$ is the entropy of the conditional distribution $$p(x \mid y)$$,

$$
H(X \mid y) = \sum_{x \in \mathcal{X}} p(x \mid y) \log_2 \frac{1}{p(x \mid y)} \, .
$$

Averaging over all possible values of $$y$$, weighted by how likely each is, gives the conditional entropy in its usual form:

$$
H(X \mid Y) = \sum_{y \in \mathcal{Y}} p(y) \sum_{x \in \mathcal{X}} p(x \mid y) \log_2 \frac{1}{p(x \mid y)} = \sum_{x,y} p(x,y) \log_2 \frac{1}{p(x \mid y)} \, .
$$

A concrete example makes this tangible. Pinkard and Waller consider drawing objects with both a color ($$X$$) and a shape ($$Y$$) at random <d-cite key="pinkard2022visual"></d-cite>. Suppose that, conditioned on the shape being a particular one (say $$\bullet$$), the color is equally likely to be green, yellow, or blue. Then $$H(X \mid Y = \bullet) = \log_2 3 \approx 1.58$$ bits: three equally probable outcomes remain even after learning the shape. If instead conditioning on a different shape narrows the color down to a single possibility, the conditional entropy for that value of $$Y$$ is exactly zero — no uncertainty is left.

Conditional entropy can never exceed the unconditional entropy: $$H(X \mid Y) \le H(X)$$, with equality iff $$X$$ and $$Y$$ are independent. Combined with joint entropy, this gives a clean chain of inequalities,

$$
H(X,Y) \ge H(X) \ge H(X \mid Y) \ge 0 \, ,
$$

and an identity that will anchor the next section: $$H(X,Y) = H(Y) + H(X \mid Y)$$ — the information in both variables is the information in one, plus whatever's left in the other after conditioning on it.

## Mutual information

Joint entropy measures the total information in $$X$$ and $$Y$$ together; conditional entropy measures what's left in one after learning the other. The information they have *in common* — how much observing $$Y$$ reduces our uncertainty about $$X$$ — is the **mutual information**:

$$
I(X;Y) = H(X) + H(Y) - H(X,Y) \, .
$$

The intuition is a counting argument: $$H(X) + H(Y)$$ counts the shared information twice (once as part of $$X$$, once as part of $$Y$$), while $$H(X,Y)$$ counts it once. The difference is exactly one copy of what's shared <d-cite key="olah2015visual"></d-cite>.

### Pointwise mutual information

Just as entropy has a pointwise predecessor (information content), mutual information has a pointwise version. For a specific pair of outcomes $$(x,y)$$, the **pointwise mutual information** is

$$
\log_2 \frac{p(x,y)}{p(x)p(y)} = \log_2\frac{1}{p(x)} - \log_2\frac{1}{p(x\mid y)} \, ,
$$

the surprise of $$x$$ on its own, minus the (typically smaller) surprise of $$x$$ once $$y$$ is already known <d-cite key="pinkard2022visual"></d-cite>. Averaging this quantity over the joint distribution recovers the usual definition,

$$
I(X;Y) = \sum_{x \in \mathcal{X}} \sum_{y \in \mathcal{Y}} p(x,y) \log_2 \frac{p(x,y)}{p(x)\,p(y)} \, .
$$

This expression is worth pausing on, because it is *exactly* the KL divergence from Part 1 — specifically, the KL divergence between the true joint distribution $$p(x,y)$$ and the "naive" product-of-marginals distribution $$p(x)p(y)$$ that we'd get by (incorrectly) assuming independence <d-cite key="olah2015visual"></d-cite>. Mutual information is the number of bits you save by understanding the real relationship between $$X$$ and $$Y$$, instead of assuming they're independent. Two useful properties follow immediately: mutual information is symmetric, $$I(X;Y) = I(Y;X)$$, and it is always non-negative (since KL divergence is), with $$I(X;Y) = 0$$ exactly when $$X$$ and $$Y$$ are independent.

### How the pieces fit together

Joint entropy, conditional entropy, and mutual information are not independent concepts — they are different ways of partitioning the same total information, and it helps to see all four quantities laid out together, with area representing bits.

<div class="l-body">
<svg viewBox="0 0 520 210" xmlns="http://www.w3.org/2000/svg" style="max-width:100%; height:auto;">
  <style>
    .box { stroke: currentColor; stroke-width: 1.5; }
    .lbl { font-family: sans-serif; font-size: 13px; fill: currentColor; text-anchor: middle; }
    .side { font-family: sans-serif; font-size: 12px; fill: currentColor; text-anchor: start; }
  </style>

  <!-- Row 1: Joint entropy H(X,Y) = 3 bits, full width 480px = 3 bits -->
  <rect x="20" y="15" width="480" height="34" class="box" fill="#5470C6" fill-opacity="0.12"/>
  <text x="260" y="36" class="lbl">Joint entropy &#160; H(X,Y) = 3 bits</text>

  <!-- Row 2: H(X) = 2 bits (320px) + H(Y|X) = 1 bit (160px) -->
  <rect x="20" y="65" width="320" height="34" class="box" fill="#91CC75" fill-opacity="0.18"/>
  <text x="180" y="86" class="lbl">Entropy &#160; H(X) = 2 bits</text>
  <rect x="340" y="65" width="160" height="34" class="box" fill="#EE6666" fill-opacity="0.18"/>
  <text x="420" y="86" class="lbl" font-size="12">H(Y|X) = 1</text>

  <!-- Row 3: H(X|Y) = 1 bit (160px) + H(Y) = 2 bits (320px) -->
  <rect x="20" y="115" width="160" height="34" class="box" fill="#EE6666" fill-opacity="0.18"/>
  <text x="100" y="136" class="lbl" font-size="12">H(X|Y) = 1</text>
  <rect x="180" y="115" width="320" height="34" class="box" fill="#91CC75" fill-opacity="0.18"/>
  <text x="340" y="136" class="lbl">Entropy &#160; H(Y) = 2 bits</text>

  <!-- Row 4: I(X;Y), centered on overlap of H(X) and H(Y) -->
  <rect x="180" y="165" width="160" height="34" class="box" fill="#FAC858" fill-opacity="0.35"/>
  <text x="260" y="186" class="lbl">I(X;Y) = 1 bit</text>

  <text x="20" y="209" class="side" font-size="11">Width is proportional to bits, in a worked example with H(X) = H(Y) = 2, I(X;Y) = 1.</text>
</svg>
</div>
<div class="caption">
  The relationships between joint entropy, entropy, conditional entropy, and mutual information, for a worked example with H(X) = H(Y) = 2 bits and I(X;Y) = 1 bit. Note how the H(X) bar (row 2) and H(Y) bar (row 3) overlap exactly over the mutual information region. Redrawn after the summary figures in <d-cite key="pinkard2022visual"></d-cite> (Fig. 7) and <d-cite key="olah2015visual"></d-cite>.
</div>

Reading the diagram: $$H(X,Y) = H(X) + H(Y\mid X) = H(Y) + H(X \mid Y)$$, and the mutual information is exactly the amount by which $$H(X)$$ and $$H(Y)$$ overlap. All three of the following are algebraically equivalent expressions for mutual information, and each has its own reading:

$$
I(X;Y) = H(X) - H(X\mid Y) = H(Y) - H(Y \mid X) = H(X) + H(Y) - H(X,Y) \, .
$$

The first says mutual information is how much $$Y$$ shrinks our uncertainty about $$X$$; the second is the same statement with the roles reversed (consistent with symmetry); the third is the counting argument from before.

## Variation of information

If mutual information measures what two variables *share*, its complement measures what they *don't*: the **variation of information**,

$$
V(X,Y) = H(X,Y) - I(X;Y) \, .
$$

Variation of information is a genuine metric — symmetric, non-negative, and satisfying the triangle inequality — on the space of jointly distributed variables <d-cite key="olah2015visual"></d-cite>. It is zero exactly when knowing one variable tells you the other completely, and it grows as the variables become more independent. It's worth contrasting this with KL divergence from Part 1: KL divergence measures distance *between two distributions* over the same variable(s); variation of information measures distance *between two jointly distributed variables*, within a single distribution.

## Fractional bits, revisited

Part 1 flagged something odd: optimal codeword lengths are frequently fractional, which seems meaningless for a single message. Consider a distribution with two outcomes, $$a$$ (probability 71%) and $$b$$ (probability 29%). The ideal codeword lengths are $$\log_2\frac{1}{0.71}\approx 0.49$$ bits for $$a$$ and $$\log_2\frac{1}{0.29}\approx 1.79$$ bits for $$b$$ — neither a whole number <d-cite key="olah2015visual"></d-cite>.

If we must send a single symbol, we're forced to round, giving an average length of 1 bit (using codewords `0` and `1`) rather than the entropy $$H \approx 0.87$$ bits. But if we encode *two* draws jointly, something better happens. The four two-symbol outcomes have probabilities $$p(aa) = 0.504$$, $$p(ab) = p(ba) = 0.206$$, and $$p(bb) = 0.084$$; assigning shorter codewords to the more probable pairs and rounding gives an average of about 1.8 bits for *two* symbols — 0.9 bits per symbol, already better than sending them independently (2 bits for two symbols) <d-cite key="olah2015visual"></d-cite>. As the number of jointly-encoded symbols $$N \to \infty$$, the rounding overhead per symbol vanishes and the achievable rate approaches the entropy exactly. This is a special case of the AEP from Part 1: block-encoding the typical set of a large-$$N$$ sequence gets arbitrarily close to the entropy bound.

(In practice, Huffman coding — essentially the scheme sketched here — needs this kind of symbol-grouping to approach the entropy limit gracefully; arithmetic coding handles fractional bits natively and is asymptotically optimal without grouping <d-cite key="olah2015visual"></d-cite>.)

## Entropy rate of a stochastic process

Everything so far has assumed a sequence of *independent and identically distributed* random variables. Real sequences — text, weather, stock prices — are rarely independent: today's value constrains tomorrow's. An ordered sequence of random variables $$\mathbf{X} = X_1, X_2, \ldots$$, without an independence assumption, is called a **stochastic process** <d-cite key="pinkard2022visual"></d-cite>.

### Two equivalent definitions

In the i.i.d. case, entropy is additive: $$H(X_1, \ldots, X_N) = N \cdot H(X)$$, so the **entropy rate** — entropy per symbol — is just $$H(X)$$. For a general stochastic process, we need a definition that doesn't assume this factorization. There are two natural candidates.

The first treats entropy rate as the average uncertainty per draw, over all $$N$$ draws jointly:

$$
\frac{1}{N} H(X_1, X_2, \ldots, X_N) \, .
$$

The second treats it as the uncertainty about the *next* draw, given everything before it:

$$
H(X_{N+1} \mid X_N, X_{N-1}, \ldots, X_1) \, .
$$

For a **stationary** process — one whose joint distribution is shift-invariant, $$p_{X_1,\ldots,X_N} = p_{X_{1+k},\ldots,X_{N+k}}$$ for any $$k$$ — both definitions converge to the same value as $$N \to \infty$$ <d-cite key="pinkard2022visual"></d-cite>.

Consider a "magical urn" version of our marble example: the first draw is uniform over four colors ($$H(X_1) = 2$$ bits), but every draw after that is more likely to repeat the previous color — $$p(\text{same color}) = \tfrac58$$, and $$\tfrac18$$ for each of the other three colors, independent of $$N$$ (a first-order **Markov chain**). Because each color is still marginally uniform, $$H(X_k) = 2$$ bits for every $$k$$ in isolation — but the *joint* entropy of consecutive draws is less than the sum of their individual entropies, because knowing $$X_N$$ substantially reduces uncertainty about $$X_{N+1}$$ <d-cite key="pinkard2022visual"></d-cite>. Concretely,

$$
H(X_{N+1} \mid X_N) = -\left(\tfrac58 \log_2 \tfrac58 + 3 \cdot \tfrac18 \log_2 \tfrac18\right) \approx 1.549 \text{ bits} \, ,
$$

constant for every $$N \ge 1$$, well below the unconditional 2 bits of the first draw. The two definitions of entropy rate — averaging the joint entropy, and the conditional entropy of the next draw given the past — both converge to this same $$\approx 1.549$$ bits as $$N$$ grows, exactly as stationarity predicts:

<div class="l-body">
<canvas id="entropyRateChart"></canvas>
</div>
<div class="caption">
  The two definitions of entropy rate for the marble Markov chain, computed exactly. The conditional definition drops immediately to ≈1.549 bits (the first draw aside, every subsequent conditional entropy is identical by stationarity); the averaged-joint-entropy definition decreases more gradually toward the same limit, since the high-entropy first draw is diluted over more terms as N grows. Reproduces the qualitative behavior of Fig. 8d in <d-cite key="pinkard2022visual"></d-cite> with values computed directly from the stated transition probabilities.
</div>

```chartjs
{
  "type": "line",
  "data": {
    "labels": [1,2,3,4,5,6,7,8,9,10],
    "datasets": [
      {
        "label": "Average entropy: H(X₁,...,Xₙ)/N",
        "data": [2.0, 1.7744, 1.6992, 1.6616, 1.639, 1.624, 1.6133, 1.6052, 1.5989, 1.5939],
        "borderColor": "#5470C6",
        "backgroundColor": "#5470C6",
        "fill": false,
        "tension": 0.15
      },
      {
        "label": "Conditional entropy: H(Xₙ₊₁ | Xₙ, ..., X₁)",
        "data": [2.0, 1.5488, 1.5488, 1.5488, 1.5488, 1.5488, 1.5488, 1.5488, 1.5488, 1.5488],
        "borderColor": "#EE6666",
        "backgroundColor": "#EE6666",
        "fill": false,
        "tension": 0.15
      }
    ]
  },
  "options": {
    "scales": {
      "x": { "title": { "display": true, "text": "N" } },
      "y": { "title": { "display": true, "text": "Entropy rate (bits)" }, "min": 1.4, "max": 2.05 }
    }
  }
}
```

### Redundancy of a stochastic process

Moving from an i.i.d. sequence to a general stochastic process also forces us to revisit redundancy from Part 1, since it can no longer be defined variable-by-variable. The general definition accounts for the *joint* entropy against the maximum entropy of the full product space <d-cite key="pinkard2022visual"></d-cite>:

$$
W(\mathbf{X}) = H_{\max}(\mathcal{X} \times \mathcal{X} \times \cdots) - H(X_1, X_2, \ldots) \, .
$$

In the marble-urn example, every individual draw is marginally uniform, so $$H(X_k) = H_{\max}(\mathcal{X})$$ for each $$k$$ in isolation — there is no redundancy variable-by-variable. But the *joint* distribution is far from the maximum-entropy (independent, uniform) joint distribution, because the outcome of one draw is highly informative about its neighbor. This is exactly why we can guess the next color far better than chance, given the previous one: the redundancy lives in the higher-order dependencies between draws, not in any single draw's marginal distribution.

## Conclusion

We've now built, from first principles, the core quantities of information theory: information content and entropy (Part 1); cross-entropy and KL divergence (Part 1); joint entropy, conditional entropy, and mutual information (this post); and the entropy rate of a stochastic process (this post). Two threads run through all of it. First, every one of these quantities has a coding interpretation — the expected length of some code under some scenario — which is what makes entropy feel inevitable rather than an arbitrary formula. Second, KL divergence quietly underlies more than it first appears to: cross-entropy is entropy plus a KL term, and mutual information *is* a KL divergence, between a joint distribution and the product of its marginals.

This is deliberately not the whole of information theory. Both source texts continue well beyond what we've covered here: Pinkard and Waller extend these ideas to continuous random variables and differential entropy, and go on to channel capacity and lossy compression — the second of the "two key problems" their tutorial sets out to address <d-cite key="pinkard2022visual"></d-cite>. Olah's essay closes with pointers to error-correcting codes and the surprising appearances of entropy in quantum information, thermodynamics, and gambling <d-cite key="olah2015visual"></d-cite>. For those directions, Shannon's original paper <d-cite key="shannon1948mathematical"></d-cite> and Cover & Thomas's *Elements of Information Theory* <d-cite key="cover2006elements"></d-cite> — the standard reference recommended by both of our sources — are the natural next stop.
