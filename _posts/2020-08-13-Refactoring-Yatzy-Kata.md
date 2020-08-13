---
layout: post
title: Refactoring Yatzy Kata
---
In this post we're going to go through the process of refactoring a yatzy score calculator provided by the [yatzy kata](https://github.com/emilybache/Yatzy-Refactoring-Kata). We'll be undertaking the process in python, and both the initial, unchanged code, as well as the code we develop throughout this exploration will be available [on my github](https://github.com/andey-robins/yatzy-refactoring). So without further ado, let's jump into the process of refactoring this code!

## Testing
The first thing to examine are the test cases. Luckily, this exercise comes with an already generated `test_yatzy.py` file which will execute automated testing of our code using the pytest framework! Howeever, we need to go through the testing file and make certain that a) the test file is set up and structured well, and b) it makes sure to test all the possible outcomes for our code. If our test aren't exhaustive, then we'll have no way of knowing whether our refactoring breaks everthing or not.

The first thing you notice after reading the test file, is the widely varied naming conventions for test cases:

```python
def test_1s():

def test_threes():

def test_fours_test():

def test_smallStraight():
```

While this is a mostly semantic problem, having inconsistent naming schemes is one of the most easily rectifyable problems in the code base. All we need to do is choose a single code style and go with it throughout. Normally, my prefered style is camelCase, but with Yatzy, the need to represent the phrases "X of a kind" means that snake_case will be more readable than camelCase (i.e. three_of_a_kind instead of threeOfAKind). Also, we can decide that our test cases should follow the naming convention of `test_<NAME OF FUNCTION BEING TESTED>`.

Next, some tests use a simple `assert <INT> == Yatzy.func(x, x, x, x, x)` while others declare an expected value and an actual value and then compare the two. The former, being more readable and taking up less lines of code while still being functionally identical, will be the one we're gonna refactor towards. 

From 

```python
expected = 15
actual = Yatzy.chance(2,3,4,5,1)
assert expected == actual
``` 

to

```python
assert 15 == Yatzy.chance(2,3,4,5,1)
```

Now, all of our tests look the same as far as form. Other issues and required changes will necessitate a change to the Yatzy class itself; however, before we can move over to the refactoring of `yatzy.py`, we need to make sure that all possible test cases are covered by our testing. I will go through and add possible 0 scores to every test, and after that, we can address the structure of Yatzy itself. Easily look at the changes to the code at this point with [this link](https://github.com/andey-robins/yatzy-refactoring/commit/e60e2766186e37455012989a0d743c4922311b29).

## Yatzy.py and "Hands" of Dice
Time to jump into the `yatzy.py` file, and oh boy, is this a mess. We could first start to see how convoluted and inconsistent the style of this code was in the test cases, but now it's all too aparent. Some function calls rely on being passed five arguments, one for each die rolled, some rely on an array being passed, and some are methods of an instance of the Yatzy class meaning we need to instantiate the class before we can calculate that value. Clearly, this needs to be re-organized and standardized.

Starting at the top level of the implementation, the question is: do we need a Yatzy class? For simply scoring the set of 5 dice as specified by the problem, the answer is obviously no; however, let's think a bit further to the point of extending this problem to be a full game. If we keep the class as is, having scoring methods somehow tied to an instance of dice rolling, is that sensical? I would argue no. The scoring behavior will be the same regardless of what numbers are rolled, so the methods should either be static methods or decoupled from a class level implementation. The question then becomes, should these be static methods or standalone methods? Again, I believe the answer is simple: they should be standalone. By making them standalone, we can pass an instance of a class that contains all of our rolls to the method, and then the method is able to reference an instance of a roll. So let's begin by conceptualizing a "roll" class.

In the future, we will want the ability to roll all of the dice (i.e. generate a random number for each die), check how many times that "hand" has been rolled, and lock certain dice to save them. All of these functions could be abstracted into a "hand" class! Then we simply pass a hand of dice to a scoring function, and it will calculate the score for that hand. We can mostly repurpose the initializer for the Yatzy class making the changes below:

```python
class Hand:
    def __init__(self, d1, d2, d3, d4, d5):
        self.dice = [0]*5
        self.dice[0] = d1
        self.dice[1] = d2
        self.dice[2] = d3
        self.dice[3] = d4
        self.dice[4] = d5
```

With this, we now have a class that holds all of our dice rolls, and we can modify our scoring methods to accept a hand and calculate the score based on that hand. For instance, the ones scoring method currently looks like this:

```python
def ones(d1, d2, d3, d4, d5):
    sum = 0
    if d1 == 1:
        sum += 1
    if d2 == 1:
        sum += 1
    if d3 == 1:
        sum += 1
    if d4 == 1:
        sum += 1
    if d5 == 1:
        sum += 1

    return sum
```

but we can change it to be:

```python
def ones(hand):
    sum = 0
    for die in hand.dice:
        if die == 1:
            sum += die
    return sum
```

This quick little change shrinks a 14 line function into only 6 lines and eliminates a long if chain that needlessly takes up space and reduces readability. However, the cool little trick comes when we can use this same format to check for any possible number just by adding a single argument:

```python
def single_number(hand, number):
    sum = 0
    for die in hand.dice:
        if die == number:
            sum += die
    return sum
```

We can now use this functionality to simplify the code for ones, twos, threes, fours, fives, and sixes to simply a call to this function with the correct number represented! We could either change the calls in `test_yatzy.py` (and by extension within the whole project anytime we call this), but that has the potential to be a large undertaking that fundamentally changes other developer's understanding of the communication within the app. Instead, we're going to turn the `ones()`, `twos()`, etc. functions into driver functions that pass to this `single_number()` function. The `ones()` function would now read:

```python
def ones(hand):
    return single_number(hand, 1)
```

Let's migrate the single number functions outside of the Yatzy class and implement this change now. This necessitates jumping back to the `test_yatzy.py` function to fix all the calls to score hands. (For instance the changes to `test_ones()` is below).

```python
def test_ones():
    assert 1 == ones(Hand(1, 2, 3, 4, 5))
    assert 2 == ones(Hand(1, 2, 1, 4, 5))
    assert 0 == ones(Hand(6, 2, 2, 4, 5))
    assert 4 == ones(Hand(1, 2, 1, 1, 1))
```

We've now introduced another interesting problem, these functions aren't really attached to anything! It would be helpful to find somehow structure these functions so that they're all encompased by some sort of prefix. If we put all of these functions in a `Scoring` class and make them static methods, now we can prefix them with `Scoring.` in order to explain everything. (It'll also be easy to migrate them to another file to structurally break up this code later.)

Check out these specific changes [here](https://github.com/andey-robins/yatzy-refactoring/commit/a03c4af50a79299f7e4d9b7517742d8f58d804dd).

## Scoring More Complicated Hands
The chance function (returning the sum of all dice) and yatzy (returning 50 if they're all the same and 0 otherwise) are two simple functions that we will migrate to the `Scoring` class without doing much discussion since their changes will be quite simple to understand. Check the source code for this project if you want to see them.

### Pairs
The methodologies for tracking pairs, namely using some other data structure to count the number of each and then go through that data structure to calculate score, is pretty good. We can reduce some of the long form info to an interative structure, we can rename some variables to be clearer, and then convert it to our Hand paradigm. Finally, we can use a dict instead of an array so that we don't need to do anything funky with indices in order to increase readability. We can go from:

```python
def score_pair(d1, d2, d3, d4, d5):
    counts = [0] * 6
    counts[d1 - 1] += 1
    counts[d2 - 1] += 1
    counts[d3 - 1] += 1
    counts[d4 - 1] += 1
    counts[d5 - 1] += 1
    at = 0
    for at in range(6):
        if counts[6 - at - 1] == 2:
            return (6 - at) * 2
    return 0
```

to this:

```python
def score_pair(hand):
    counts = dict.fromkeys(range(1, 7), 0)
    for die in hand.dice:
        counts[die] += 1

    for location in reversed(range(1, 7)):
        if count[location] >= 2:
            return location * 2
    return 0
```

Now, all that we need to do to calculate the score for two pairs, is take that same code, and only return if there are two pairs!

### Sets
We can pretty easily repurpose our code for scoring pairs to just check if there are 3 or 4 counts of a card! For instance we can repurpose the given four of a kind code:

```python
def four_of_a_kind( _1,  _2,  d3,  d4,  d5):
        tallies = [0]*6
        tallies[_1-1] += 1
        tallies[_2-1] += 1
        tallies[d3-1] += 1
        tallies[d4-1] += 1
        tallies[d5-1] += 1
        for i in range(6):
            if (tallies[i] >= 4):
                return (i+1) * 4
        return 0
```

to:

```python
def four_of_a_kind(hand):
        counts = dict.fromkeys(range(1, 7), 0)
        for die in hand.dice:
            counts[die] += 1

        for location in reversed(range(1, 7)):
            if counts[location] >= 4:
                return location * 4
        return 0
```

### Straights
Now, scoring the straits is incredibly simple! All we need to do is check if the hand is `[1,2,3,4,5]` for a small straight or `[2,3,4,5,6]` for a large straight! The only small consideration to make is the need to make a call to python's `sort()` method before making the comparison so that we know that the comparison will be accurate.

### Full House
A full house is also very easy to calculate. When we count the frequencies of all our dice, if one of them happens three times and the other happens twice, we know that it's a full house. Then, the score is just the sum of all the dice, something easy to calculate with a call to the `sum()` method. This cuts the size of the full house method down remarkably.

Before:

```python
def fullHouse( d1,  d2,  d3,  d4,  d5):
    tallies = []
    _2 = False
    i = 0
    _2_at = 0
    _3 = False
    _3_at = 0

    tallies = [0]*6
    tallies[d1-1] += 1
    tallies[d2-1] += 1
    tallies[d3-1] += 1
    tallies[d4-1] += 1
    tallies[d5-1] += 1

    for i in range(6):
        if (tallies[i] == 2): 
            _2 = True
            _2_at = i+1
        

    for i in range(6):
        if (tallies[i] == 3): 
            _3 = True
            _3_at = i+1
        

    if (_2 and _3):
        return _2_at * 2 + _3_at * 3
    else:
        return 0
```

After:

```python
def full_house(hand):
    counts = dict.fromkeys(range(1, 7), 0)
    for die in hand.dice:
        counts[die] += 1

    if 2 in counts.values() and 3 in counts.values():
        return sum(hand.dice)
    return 0
```

[Here's the changes](https://github.com/andey-robins/yatzy-refactoring/commit/258bfed53a7fd9748173163cd11c7d64c71839ce) that we've managed to do for refactoring in this post!

## Conclusion
We've done a lot for this refactoring so far. Most of what we've done has been modifying the overal structure, fixing inconsistencies, and removing hard coding searches/counting wherever possible. At this point, what are we missing? Well, we could do a little bit more refactoring to get rid of the creation of a counter in several methods by placing it in its own function (something that would decrease our code re-use, but wouldn't let us change counting for each scoring method. It's a trade off relationship and one that I don't see as super necessary right now.) and by putting comments throughout. Perhaps we'll make some time later to break it apart and go through commenting in a blog post. Regardless, this has been an exciting exercise in refactoring. We cut 44% of the code out from the pre-refactored code, and we reduced the run time of the tests to a third of what it was previously. Clearly this was effective and needed for this code.

Until next time.
-andey