# Technical Debt

Continuous refactoring is an essential part of agile development. Agile teams are maintaining and extending their code a lot from iteration to iteration. Without continuous refactoring, this is hard to do. This is because un-refactored code tends to rot. Rot takes several forms: unhealthy dependencies between classes or packages, bad allocation of class responsibilities, way too many responsibilities per method or class, duplicate code, and many other varieties of confusion and clutter.

Every time we change code without refactoring it, code rot worsens and spreads just like cancer. Code rot frustrates us and costs us time. Refactoring code ruthlessly prevents rot, keeping the code easy to maintain and extend.

## Basic Rules

Actually it's quite easy to avoid Technical Debt (TD) during development:

- **No TD policy for new components:**</br>
  New components must not contain any TD. As long as TD exists, the **definition of done** is not reached. When it becomes apparent, that a new component was built with TD, a Quality Bug must be created. The Quality Bug has to be tackled either immediately or at least within the upcoming timebox.
- **Changes to existing code:**</br>
  When you have to change existing code, always ask yourself, if it's possible to do it without increasing the TD. Usually you will feel the need to build some kind of **workaround** (which would increase the TD). In these cases a refactoring will be necessary.</br>
  **Boy scout rule**: "Always leave the code behind in a better state than you found it."</br>
  So, code must not deteriorate. Decrease the TD, don't increase it!
- **Refactorings must not be charged against each other:**</br>
  It's not acceptable to increase TD in one component, because it was reduced it in another one. No matter how much you refactored in the past, it doesn't release you from the obligation of clean coding in the future.

## Over-Engineering

![It's a trap!](img/ItsATrap.jpg)

Even good developers stumble in that pitfall, when you had to work with smelly legacy code for years tend to become anxious and overprotective, which can lead to over-engineering (OE). But more often it's caused by lack of knowledge or by a misunderstanding of design patterns. This topic is tricky, because OE programmers usually want to do something especially good: "I'm using design patterns and architecture, therefore I'm writing good code."

So, what is OE? It simply means "too much". But what is too much? When does under-engineering become over-engineering? There is no easy answer to that question. On the first glance, OE can look clean and tidy, but in the end it simply bloats your code without bringing any benefit. So in one small sentence, what is OE: **Code that solves problems you don't have.**

The common culprits:

**Feature creep**:
Developers tend to be overenthusiastic about cluttering a component with functionality or an overdosed architecture, that is not really needed to solve the problem. Don't ever make assumptions about the future. Never write code features only because you assume, that it could be useful some day in the future. When you implement something, you should be absolutely sure it's gonna be needed. If not, don't do it. Behold of the following platitude (or variations of it): **"... maybe someone could some day ..."**

**Code bloaters**:
Always write the simplest code you can. The less code you write to solve a task (without breaking clean code principles), the better. Anything can be bloated: methods, classes, architecture. You don't need to build a death star to destroy an ant hill. I know, death stars are really cool, but it (a) costs too much (b) takes too much time and (c) is a maintenance nightmare. I mean, somebody’s going to have to go up there and fix it when it breaks.

To sum it up:
- **KISS**: Keep it Simple, Stupid.
- **YAGNI**: You Ain't Gonna Need It.

## Dead Code

There is a good and a bad news about dead code.

The bad news: It bloats up your code and the complexity of your project (and the whole system) without providing any benefit. At best it simply draws away your attention and increases compile time. But most likely it will hamper the development of new features and the maintenance of living code.

The good news: There is absolutely no reason not to delete the code immediately as soon as it comes to your attention. It's dead, it has no mourning relatives.

## Parallel Worlds

Quite often it's easier to re-implement a component shiny and new, rather than refactoring existing legacy code. But please note, your not done until you completely replaced the old component with your new one. You're done, when the old component is deleted.

By the way: Marking the legacy code with `[Obsolete]`, is just another way of saying that your too lazy to pay back your technical debt. It's not OK to shift debts to somebody else.

## Never reinvent the Wheel

This company has a rich tradition of implementing stuff, instead of using existing frameworks and libraries. E.g.: THORSerializer, AML, ObservationLog

There are almost always free, great solutions for common problems in software development, designed and created by people with a much deeper understanding and knowledge of the matter. Reimplementing the stuff is a wasted effort and highly prone to bugs and unforeseen issues.

## Great links

[Opportunistic Refactoring - Martin Fowler](http://martinfowler.com/bliki/OpportunisticRefactoring.html)</br>
[Technical Debt - Martin Fowler](http://martinfowler.com/bliki/TechnicalDebt.html)</br>
