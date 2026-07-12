---
layout: post
title: "Simpson's Paradox: When the Same Data Tells Two Different Stories"
description: An intuitive introduction to Simpson's Paradox — how averages can lie to you without any of the numbers being wrong.
date: 2026-07-12 12:00:00
tags: statistics data
giscus_comments: true
toc:
  sidebar: left
---

> "Sometimes the numbers are correct, but the conclusion is wrong."

This article is inspired by the philosophy of explanation in Michael Nielsen's essay on building intuition rather than merely presenting facts. So instead of jumping straight to the definition, let's start by feeling why Simpson's Paradox is surprising — and only then explain it.

## Have you ever seen this happen?

{% include figure.liquid loading="eager" path="assets/img/simpsons-paradox-classroom.jpg" class="img-fluid rounded z-depth-1" %}
<div class="caption">
  College students appearing for a competitive examination, all preparing for the same kind of exam.
</div>

Imagine two coaching institutes preparing students for the GATE examination.

The newspaper reports the overall pass percentage:

| Institute | Overall pass % |
|---|---|
| Institute A | 76% |
| Institute B | 70% |

Most people would immediately say, "Institute A is clearly better."

Now suppose someone shows another table — this time splitting students by category:

| Student category | Institute A | Institute B |
|---|---|---|
| Students with a strong academic background | 95% | 98% |
| Students needing extra support | 50% | 55% |

Now things get confusing. Institute B performs *better* in both categories. Yet when all students are combined, Institute A still has the higher overall pass percentage.

How can that be? Did someone make a mistake? Did the newspaper calculate the percentages wrongly? Can both tables be correct at the same time?

Take a minute before reading further.

Most people — including many professors the first time they see it — feel that this should be impossible. But it isn't. This is called **Simpson's Paradox**.

## The surprise

Simpson's Paradox is one of those ideas that changes how you look at data forever. It teaches a simple lesson:

The overall average does not always tell the real story. Sometimes the data inside different groups tells one story. When those groups are merged together, the story changes completely.

The mathematics is perfectly correct. Our intuition is what fails.

## Why does this happen?

Imagine there are only two kinds of students: those who are already very strong, and those who need more help.

Now suppose Institute A admits mostly strong students, while Institute B admits many more weaker students. Even if Institute B teaches both groups slightly better, its overall result can still come out lower — because a much larger fraction of its students started out at a disadvantage.

Think of cricket. Suppose two batsmen play on different pitches — one mostly bats on flat, easy batting tracks, the other usually bats on difficult green pitches. Simply comparing their overall batting averages may not tell you who actually bats better under similar conditions. The mix of situations matters. That hidden mix is what creates Simpson's Paradox.

## A simple visual way to think about it

Imagine two baskets of mangoes. Basket A contains mostly ripe mangoes. Basket B contains mostly unripe mangoes.

Now compare two farmers. Farmer B actually grows slightly better mangoes than Farmer A — in *both* baskets. But Farmer B happened to send many more unripe mangoes to the market. Overall, Farmer A's mangoes may appear better.

The problem isn't the quality. The problem is that we mixed together two very different groups.

## Example from an Indian college

{% include figure.liquid loading="eager" path="assets/img/simpsons-paradox-programming-lab.jpg" class="img-fluid rounded z-depth-1" %}
<div class="caption">
  A programming lab — exactly the kind of class in this example.
</div>

Suppose two teachers teach Programming. Teacher A teaches one section, Teacher B teaches another. The final university results are:

| Teacher | Overall pass rate |
|---|---|
| Teacher A | 82% |
| Teacher B | 78% |

So everyone says, "Teacher A is better."

Now the principal separates students based on their Class 12 mathematics marks:

**Students with strong mathematics**

| Teacher | Pass rate |
|---|---|
| A | 92% |
| B | 95% |

**Students with weaker mathematics**

| Teacher | Pass rate |
|---|---|
| A | 60% |
| B | 65% |

Teacher B performs better in *both* groups. So why is Teacher A's overall result higher? Because Teacher A happened to receive many more students who already had strong mathematics backgrounds, while Teacher B had a much larger number of weaker students. The overall percentage is therefore influenced by who entered the class — not only by how well they were taught.

## Another everyday example

Suppose two hospitals perform surgeries. Hospital A mostly receives patients with minor health problems. Hospital B receives many complicated emergency cases.

Even if Hospital B performs better for both easy and difficult surgeries separately, its overall success rate could still look lower — simply because it treats far more difficult cases. Without knowing the type of patients each hospital receives, comparing only the overall success rate would be misleading.

## What is really happening?

A hidden variable changes everything. In our examples, the hidden variable was: academic background, patient condition, exam difficulty, starting ability.

When we ignore these factors and simply average everything together, we may reach the wrong conclusion. Statisticians call these hidden influences **confounding variables**. You don't need to remember the term — just remember the idea:

Always ask whether different kinds of data have been mixed together.

## Does this mean averages are bad?

Not at all. Averages are useful. But averages answer only one question — they do not explain *why* the average looks the way it does.

Whenever you see an average, ask yourself:
- Who is included?
- Are all people similar?
- Are different groups being mixed?
- Would the conclusion change if I looked at each group separately?

These four questions can save you from many wrong conclusions.

## Where does Simpson's Paradox appear?

It appears surprisingly often. Researchers encounter it in medicine, education, economics, sports, machine learning, public policy, and business analytics. Whenever data from different groups is combined, Simpson's Paradox becomes possible.

## What should you learn from this?

After reading this article, here are the ideas to remember.

**1. Bigger numbers do not always tell the complete story.** An overall percentage can hide important details.

**2. Always look inside the groups.** If possible, examine the data separately before combining everything.

**3. Ask what has been mixed together.** Different student backgrounds. Different hospitals. Different departments. Different states. Different years. Mixing different populations can completely change the conclusion.

**4. Statistics is not only about calculation.** It is also about asking good questions. Sometimes the most important question is not "What is the average?" — instead it is "Average of whom?"

## A small thought experiment

Suppose your college announces: "The placement percentage has increased this year." Before celebrating, ask:

- Did all departments improve?
- Or did one department become much larger?
- Did weaker departments shrink?
- Were more students eligible this year?

The overall number may be true. But the complete story may still be hidden. That is exactly the lesson of Simpson's Paradox.

## Conclusion

Simpson's Paradox reminds us that data can be honest while our interpretation is mistaken. It teaches an important habit that every engineer, scientist, economist, and manager should develop: never stop at the overall average. Look inside the data. Understand the groups. Ask what has been combined. Only then can numbers reveal the truth instead of hiding it.

As the famous statistician John Tukey once said, "The greatest value of a picture is when it forces us to notice what we never expected to see." Simpson's Paradox does exactly that — it forces us to question our first impression and think more carefully about what the data is really saying.
