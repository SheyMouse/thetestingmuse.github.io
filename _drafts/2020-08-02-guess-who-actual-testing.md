---
layout: post
title: Guess Who! Actual Testing
subtitle: 2nd Aug 2020
description: "... "
date: 2020-08-02 14:46:00 +00:00
author: David
permalink: /blog/guess-who-actual-testing/
featured\_image: /images/posts/GuessWhoTesting.jpg
categories:
  - Testing
---

<img src="/images/posts/GuessWhoTesting.jpg" alt="Guess Who Testing" style="float:right; margin-left: 10px; width:50%;" />

## Guess Who? Part 2

In my previous blog post I documented an example of the Information Model designed by Dan Ashby, and used the childhood game of Guess Who as an example. If you missed that post, please feel free to have a read first, to get an idea on the context for this post.

This post is a continuation of the last one, but I’m going into detail on how my brain interprets the challenge of testing Guess Who. All brains are fallible, miss things and misinterpret things so this is by no means a definitive approach - Have a think about how _you_ might approach testing the game.

I’ll start with the rules for the game itself, and then into my process.

## Game Summary

The idea of the game is simple:
- Two players face each other, with a board each, containing 24 unique character faces.
- They mentally pick a character as "their character" for the opponent to guess.
- They take turns asking simple "yes or no" questions about the characters, to try and isolate their choice, in order to guess correctly and win the game.

The game rules are also simple:
- Each player gets **a single** “yes or no” question **per turn**.
- They can only Guess Who (to try and win the game) **once per game**.
- If a player **successfully guesses** their opponents character, **they win**.
- If their guess is **wrong, they lose**.

## Testing Guess Who

<img src="/images/posts/InformationModel-Stage1.jpg" alt="Information Model Stage 1" style="float:right; margin-left: 10px; width:50%;" />

### Initial Questions
Off the top of my head, the following questions occur:
1. Why are we testing this?
2. What do we expect to achieve from the testing?
3. What’s been tested already?
4. How do we report information gained?
5. How long do we have to test? How can I prioritise my effort?
6. Should I be focusing my effort on functional (for example the physical game, the game mechanics and logic etc) versus non-functional (durability, design, accessibility, usability, ‘fun’)?

### Starting Mindmap
I normally document my testing in a mind map. I tend to find that mind maps fit my thought process well, and allows me to both focus, and defocus to check the detail and scope of my work, plus the coverage of my effort.

All of my testing mind maps follow a similar skeleton framework:

MINDMAP SKELETON

From here I start adding contextual detail:



At the very start of the game, our simplified Information Model has the following bubbles:
- **Investigate** = Blank (but we can ask a single question per turn to add to our Information bubble)
- **Information** = Could be anyone!
- **Verify** = Blank (we can only fill this with a direct guess, and if we're wrong, we lose)

At this point, we _could_ follow the “Verify” path and try to win the game with a guess:
> "I think it's Susan!"

But this early in the game, a guess would have only a 4% chance of success.
It’s therefore in our best interest to ask a single yes/no question, to increase the odds of a correct guess for our next go.

<img src="/images/posts/InformationModel-Stage2.jpg" alt="Information Model Stage 2" style="float:right; margin-left: 10px; width:50%;" />

We decide not to take the risk, and we "Investigate" by asking a question,
> “Do they have glasses?”

The answer is “No”, so we push down all 5 faces that have glasses, which leaves 19 still as potential winning guesses.

Our model then looks like this:
- **Investigate** = Do they have glasses?
- **Information** = NO glasses
- **Verify** = Blank (we have not had the confidence to take a guess, yet. Remember, if we're wrong, we lose instantly!)

On our next turn we have the same choice to make:
1. Take a guess, at the odds we now have of being correct (5%).
2. Investigate some more by asking another question.

Are we confident enough in these odds to take the Verify path?

<img src="/images/posts/InformationModel-Stage3.jpg" alt="Information Model Stage 3" style="float:right; margin-left: 10px; width:50%;" />

We decide that we’re not confident enough yet, so we take the Investigate path again and ask another question:
> “Do they have blonde hair?”

Aha, they do! So we update our model:
- **Investigate** = Do they have glasses? Do they have blonde hair?
- **Information** = Do NOT have glasses, DO have blonde hair!
- **Verify** = Blank (Again, we did not want to take the risk of guessing)

It’s our turn again and our choice is now:
1. Go down the Verify path (take a guess), at the odds we now have of being correct (33%)
2. Investigate some more (ask another question).

Are we confident enough now in these odds to take the Verification path?

And so on...

And so you see that investigation, and analysis, and critical thinking all enable us to make decisions on our next action, until we have enough confidence (acceptance of risk) that we want to follow the next stage of the game - Using our Expectations to Verify that our guess is correct.

## Guess Why?

So, why am I reminding you of this random childhood game? Well, the game is an ideal example of the _Investigation_ part of [Dan Ashby][1]’s [Information Model][2], and a great way to explain the process of Testing, to non-testers.

As a software development team, we should be creating Information Models on our work. We should be investigating and asking questions, to build our understanding of the task in hand. The more knowledge we have, the more confidence in the solution we might have. We might uncover risks, assumptions, information, things we knew, things we didn't know, things that might be beneficial, or a hindrance; there are **many** things we can uncover, which the team can use to create the right solution for the problem.

As information is discovered, we can feed that information back into the "Investigation" to uncover more information, or if information has lead to Expectations, we can feed those into our "Verification" bubble to verify that those expectations are met.

We continue this cycle until we have an **acceptance of the risks** with the feature we are modelling. Or until we feel that the quality of the feature is _good enough_.

## Guess How?

How would you have played Guess Who if you could guess every turn without forfeit?
Would you guess more often?
Would you play the same?

How would you play, or how would your Information Model differ, if the character you had to guess was always changing?
Or if you had multiple characters to guess?

Or how about if the questions asked could be answered with:
- Yes
- No
- Maybe
- I refuse to answer

[1]:	https://mobile.twitter.com/DanAshby04
[2]:	https://danashby.co.uk/2016/03/08/information-and-its-relationship-with-testing-and-checking/