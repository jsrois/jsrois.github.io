---
title: Yatzy Kata on a train (I)
layout: post
date: '2017-08-05'
categories:
- TDD
- katas
- c++
description: First steps with the Yatzy Kata in C++, slow coding
image: https://unsplash.it/2000/1200?image=983
image-sm:
---

The Yatzy Kata is considered one of the simplest ones and yet, we can learn a lot of things from it. Here I'm approaching the Kata taking reeeeally small steps and discussing some very basic ideas. 

Last week I was on my way to Coruña from Vigo. It is a 2-hour train trip. As soon as I seated down, I realized I hadn't brought my headphones (so no music or movie watching) or any books. Yeah, first world problems. But as the caffeine kicks in I really need _something to do_, and then I realize I have a copy of "The Coding Dojo Handbook" by Emily Bache in my laptop. Really good book. So I search in the "Kata Catalog" for a simple one.

And I picked the Yatzy Kata. I remember doing this one a while ago, but still 

> This Kata is quite easy for TDD beginners since the test cases are more or less enumerated in the problem description.
 The order to implement them in is not prescribed, though, so you can practice that aspect of TDD. 
 (Emily Bache, "_The Coding Dojo Handbook_")
 
Given a dice roll and a category, we have to calculate the score. That's it. Well, at least that is the premise. After reading the whole kata description (this is something convenient!) we can start from the first "roll to score" case: "Chance". 

**The shopping list**: as Kent Beck does in "Test-Driven Development by Example", it is useful to keep a list of goals, and keep track of what we have achieved so far; as well as new requirements that may come up. So at this point, the list should look like: 

[ ] Chance
- [ ] Yatzy
- [ ] Ones, Twos, Threes, Fours, Fives and Sixes
- [ ] Pair
-[ ] Two Pairs
-[ ] Three of a Kind
-[ ] Four of a Kind
-[ ] Small Straight
-[ ] Large Straight
-[ ] Full House


### First test, first questions:

The first requirement reads as follows: 

```
Chance: The player scores the sum of all dice, no matter what they read. For example,
• 1,1,3,3,6 placed on “chance” scores 14 (1+1+3+3+6) 
• 4,5,5,6,1 placed on “chance” scores 21 (4+5+5+6+1)
```

We write the first test:

```
TEST_CASE("CHANCE score is the sum of all dice", "[unit]") {
  REQUIRE(Score(15) == Yatzy().chance(Roll{1,2,3,4,5}));
}
```

Just by writing this first test, a few questions came up: _why using "Score" and "Roll" explicitly_ and not just throw in some primitives, something like: 
 
```
REQUIRE(15 == Yatzy().chance({1,2,3,4,5}));
```

You can see, this second version does not say anything explicitly about the "Game Domain", the business we are dealing with. So I choose to talk about the problem _in the test code_ just as the description of the kata does.

**Domain concepts and how to read a kata description:** When it comes to a kata, I always find useful to search for the **nouns** in the description to discover concepts. This is something I have learned from Manuel Rivero (@trikitrok). Antipatterns: usually, when we face a kata (o a new project) from scratch, we tend to introduce external concepts (I tend to use things like `Processing` and `Parameter` too much) or some absurdly ambiguous ones (`do_work` anyone?). 
 
Back to the code. Let's write an skeleton to make this test compile. 


```
typedef unsigned int Score;
typedef std::array<Score, 5> Roll;
class Yatzy {
 public:
  Score chance(const Roll& roll) const {
    return Score();
  }
};
```

_Whoa, whoa... typedef? I thought we were creating new objects here._ Well, `typedef` is the simplest way of making our
explicit declaration of domain things compile. We could introduce new classes for both `Score` and `Roll`, but what for? 
It looks like a lot of code at this point. I actually never spoke about objects :P.

So, the test compiles and fails, but we can easily make it pass with this ugly solution: 

```
Score chance(const Roll& roll) const {
    return roll[0]+roll[1]+roll[2]+roll[3]+roll[4]; 
}
```

Is it ugly? I think so. Why? Well, first of all, it is a bit `C-ish`. Even we assumed there is nothing wrong 
with using `C` stuff, we already opted for a `C++ -all-the-things` solution when we chose `std::array` over using a `C` array.

So, if what we want to calculate _the sum of the elements of this `std::array`_, the proper way to do it is to use the 
standard functions for it. Now that our test passes, let's refactor:

```
Score chance(const Roll& roll) const {
    return std::accumulate(roll.begin(), roll.end(), Score(0)); 
}
```

> At this point, you may argue this is the best implementation. I consider it good enough for now to continue implementing 
the rest of the test cases. At this point, some alternatives occurred to me, but all of them involved adding more code.


### Yatzy!

So, the next requirement in our list is Yatzy, the name of the game. Let's start, again, with 
a test:

```
TEST_CASE("YATZY score is 50 if all dice have the same number", "[unit]") {
  REQUIRE(Score(50) == Yatzy().yatzy(Roll{2,2,2,2,2}));
} 
```

Easy! we can just add a naive implementation of the `Yatzy::yatzy` method:

```
Score yatzy(const Roll& roll) const {
  return 50;
}
```

But this is incomplete, as the score is 0 for the rest of the rolls: 

```
TEST_CASE("YATZY score is 50 if all dice have the same number", "[unit]") {
  REQUIRE(Score(50) == Yatzy().yatzy(Roll{2,2,2,2,2}));
  REQUIRE(Score( 0) == Yatzy().yatzy(Roll{1,2,3,4,5}));
} 
```

This makes us complete the code while staying at the simplest solution path. Now, the solution involves one conditional 
(whether all the dice in the roll have the same or not). We'll jump directly into using the standard library:

```
Score yatzy(const Roll& roll) const {
 if (std::count(roll.begin(),roll.end(),roll.front())==roll.size()) {
   return 50;
 }
 return 0;
}
```

Now, one may argue this is not the best solution at all. In terms of efficiency, we could return 0 as soon as we find 
an element different than the first. But doing so would mess up the implementation and we are doing something else before continuing.

### They see me Rollin' ...

The more I deal with the `roll` object, the less I like it. Seems like continuing the kata in this fashion
will involve more of this `roll.begin()`, `roll.end()` crap. I would prefer the `Yatzy` code to communicate the scoring 
rules and nothing else. With this idea in mind, I will move part of this logic to the `Roll` object. In some sense, this
 is a `Tell, Don't Ask` move, after which we will "tell" the Roll object to do something for us (us being the Yatzy).
 
In her book "99 bottles of OOP", Sandi Metz shows how to refactor code one line at a time using what she calls "The Flocking Rules". 
That one is a wonderful book and I would love to apply those same rules to this case,  ... 

So first we'll create a Roll class which will eventually substitute our Roll type. The idea is to make small moves.

At this point, I see two ways of approaching this refactor: 

- We can _test-drive_ an isolated `Roll` class (e.g. in a separate file) until it mimics what we are doing in the two existing
 test cases, then remove the `Roll` type and use the new `Roll` class instead. 
 
- We can substitute the use of the type `Roll` for the new class, step by step while making sure the existing tests pass.

##### Step by step

First substitute the `Roll` type definition with a new class. In particular, we'll make the new class an _aggregate_, containing
the array of dice:

```
class Roll{
 public:
  const std::array<Score, numberOfDice> values;
};
```

Obviously the code doesn't compile now. The adjustment we have to add to the Yatzy implementation is the new indirection (`roll.values`):

```
class Yatzy {
 public:

  Score chance(const Roll& roll) const {
    return std::accumulate(roll.values.begin(), roll.values.end(), Score(0));
  }

  Score yatzy(const Roll& roll) const {
    if (std::count(roll.values.begin(), roll.values.end(), roll.values.front())==roll.values.size()) {
      return Score(50);
    }
    return Score(0);
  }
};
```

Of course this is far from the code we would like to have, but it is only the means to an end right now. Let's ask something to the 
`Roll` class: 

```
TEST_CASE("Roll computes the sum of the dice") {
  Roll r{1,2,3,4,5};
  REQUIRE(r.sum() == Score(15));
}
```

Sounds reasonably to look to the sum of dice as something `Roll` should take care of, doesn't it? Let's make this test pass by
using this (look familiar?): 

```
Score sum() const {
  return std::accumulate(values.begin(), values.end(), Score(0));
}
```

Guess what's next? Exactly. We are substituting the old implementation of Yatzy::chance with this beautiful line, which 
screams about the game rules (_"The player scores the sum of all dice"_): 

```
Score chance(const Roll& roll) const {
  return roll.sum();
}
```

In the same fashion, let's refactor the `Yatzy::yatzy` method. I'll fast forward a bit:

```
bool Roll::isUniform() const {
  return (std::count(values.begin(), values.end(),
            values.front()) == values.size()); 
}
// ... 
Score Yatzy::yatzy(const Roll& roll) const {
  if (roll.isUniform()) {
    return 50;
  }
  return 0;
}
``` 
##### One step back, two steps forward

We did it! By making these moves, we have decoupled a bit the rules of the game

We could have foreseen the role of "Roll" before starting, but we found ourselves in these kind of 
"better-refactor-before-continuing" situations more often than we get it right in the first place. Stopping and
 refactoring can be something hard to propose, specially when we program under pressure. For the less experienced it is
 a leap of faith, but after generating tons of crap code, it's easy to accept that 5 minutes of "factoring retreat" can 
 be priceless if not essential.
 

#### More rules! And foreseen duplication

The next rule is actually a family of rules: 

> Ones, Twos, Threes, Fours, Fives, Sixes: The player scores the sum of the dice that reads one, two, three, four, five or six, respectively.

Let's start with the "ones" category by writing the (failing) test:

```
TEST_CASE("in ONES, the score is the number of ones") {
    REQUIRE(Yatzy().ones(Roll{1,2,1,3,5}) == Score(2));
}
```

When we faced the previous two test cases, we only had the Yatzy class. Now that we have 
introduced part of the logic into the Roll class, we can analyze the new requirement and
 realize that we have to check the Roll for the number of dice that scored 1. We can lean out a bit to
 the implications of this requirement
 


Now that we have modified `Roll` in advance, we can dive into the new game requirement.

``` 
TEST_CASE("count of number of dice reading one") {
    REQUIRE(Roll{1,3,1,2,1}.howManyOnes() == 3);
}
```

... 
