---
layout: post
title: What I Learned from Pair Programming
date: 2014-05-27 19:03:00
---

Six weeks ago I started a new job at a company that does pair programming almost exclusively. I was excited going into it because I knew it was an opportunity to learn a lot, and very rapidly. Some of the lessons I've learned have been surprising to me, and I wanted to share some:

## Learn Shortcuts

<img src="http://imgs.xkcd.com/comics/is_it_worth_the_time.png" alt="Is It Worth The Time" width="100%" />

One of my favorite engineers to work with will sometimes ask me, "How good are you with some_technology?" I'll answer that I'm not bad, and over the next few minutes he'll show me some of the ridiculous shortcuts and tricks he knows. The more mastery you gain over your tools, the faster you'll be at your craft. As Kent Beck said, "I'm not a great programmer, I'm a pretty good programmer with great habits."

## Everyone Gets Frustrated

<img src="/images/research.gif" alt="Research" width="100%" />

I **hated** feeling lost at my last job, because I felt like it meant that I was a bad engineer. It seemed to happen a lot, which made me doubt my own abilities. Now, I'll sometimes pair with more senior engineers - even brilliant people who've been programming for 30 years - and we'll still have situations where we're completely stumped for a long period of time and have to work through it.

I've learned that this is totally fine and normal in software engineering. Everybody has to start largely from the beginning when picking up a new technology. What I've learned from my pairs is to just get up and take a break from things if we've been trying to debug some silent failure for the last hour and are making no progress. There's only so much mental focus you can muster if you're stuck, and sometimes it's better just to come back refreshed and ready to try a new approach.

## Seek Out and Accept Criticism

<img src="/images/wtf.jpg" alt="Code Quality Measurement" width="100%" />

Having a partner with you is awesome. It's like having a constant code-review while you work, so you can be more confident in your approach, and get instant feedback so you can do even better the next time. Some engineers feel uncomfortable with criticism, but software engineering is an incredibly challenging discipline. Your growth will be severely stagnated without input from other people.

## Aggressively Refactor Code

<img src="http://imgs.xkcd.com/comics/good_code.png" alt="How to Write Good Code" width="100%" />

One of my favorite senior engineers that I've worked with showed me that you don't need to be timid about refactoring the codebase (though you may want to clear it with other engineers if it's a big change). If the way something is architected doesn't make sense anymore or is starting to smell, sometimes it's best to just jump in and start changing things. This is where Test Driven Development is great - you have all these tests to fall back on, so you can make fairly radical changes without worrying too much about regressions.