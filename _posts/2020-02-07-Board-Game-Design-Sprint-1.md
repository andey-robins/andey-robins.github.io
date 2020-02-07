---
layout: post
title: Board Game Design Sprint 1
---

Welcome to the new decade! To start this new year (even though it's February already) off right, I'm doing a new series on this blog; Board Game Design Sprints! In this series, I'll be tackling design challenges from the book "Challenges for Game Designers: non-digital exercises for video game designers." This week, we're working on a bare bones challenge meant to get the design juices flowing and to try to create a quick game using nothing but a simple little challenge.

## The Challenge
So what is the challenge? We need to construct a "race-to-the-end" game. That's basically it! CfGD provides a few more qualifiers to the game such as the need for the game to support 2-4 players, it must be about progressing on some form of a path, it has to be a race from point A to point B, and the first person to point B is the winner. Overall, not an incredibly difficult challenge, and certainly something that we could put together pretty quickly.

Not specifying any form of materials, I could simply have put together some form of a board game in this vein. That idea certainly occurred to me, but I wanted to add another challenge on top of this one. At one point, the challenge to get into the grad schools I've been eyeing is to create a game that can be explained in only one page and that utilizes nothing more than a standard deck of playing cards. As such, this seems like an excellent additional constraint to put on our design for this game.

## Beginning the Process
Deconstructing the parts of a regular deck of playing cards, you have two colors, four suits, and thirteen different face cards. Somehow, these combinations have to come together to be a race of some sort. And they need to form some sort of path.

Well, cards laid out end to end form a sort of a path. What if we took an entire suit and made that the path? A-2-3-4-5-6-7-8-9-10-J-Q-K forms a natural progression, and an even more natural path. So what if players need to progress from the Ace to the King, and the first person to the King space wins? That's a pretty easily understandable concept, and that progression is something that seems as though it will be easy to instill within players.

Now, how do players move along the path? We have three other full suits of cards at our disposal. At this point, I began trying to figure out what the best driving mechanic would be. The list was pretty short.

## Mechanic Ideas
  * Some form of bluffing mechanic
  * A trick taking mechanic
  * Something to do with high cards?
  * ?????

## Moving to a Theme
As you can see, quite the short list. I continued turning around the common playing card game mechanics in my mind, searching for the mechanic that fit with the race elements of the game, and then I began trying to understand what the theme of this game would be.

With the run from Ace to King, it seemed natural to associate the game with trying to take the crown! Yes, the cards themselves, as well as the race, built quite naturally into this idea. And so the theme of racing for the crown had arisen.

Alright, now that we had a theme, how can that knowledge of theme be used to help us select from our possible list of mechanics? Do any of them seem to naturally support the idea of taking the monarchy? Of stealing the crown?

Well, trick taking has the phrase 'take' in its name. Let's explore that idea. If we had some sort of push your luck, trick taking game, players could play cards from the three suits not currently used for the path and use them to try to count up to some value in order to win a step on the pathway to taking the monarchy.

While we're on the subject of theme though, if we're trying to count up by playing cards, well, that sounds a lot like blackjack. So let's take out the Ace from the path and give it the 1/11 value flexible position that it accounts for in that game. Then, since we're trying to build up the idea of you taking the crown faster than others, what if you could play other royal cards in order to exert your influence over the court?

## First Rule Set
This set of questions and answers led naturally into the first set of rules for the game. They are as follows:

Setup - Remove all spades from the deck of cards. Place the cards 2 through 10 in order in the center of the playing area and place a player marker for each player onto the 2 of spades. Then shuffle the remaining spades and all of the other cards together. Deal each player a hand of 7 cards.

Gameplay - Choose a player to go first. That player will play a card onto the table. Proceeding clockwise, each player will play a card from their hand onto the pile. A player immediately wins the pile and advances their piece one space if they play a card that forces the total of the pile to be 21. Each numerical card counts for the depicted value, Jacks and Queens both count 10, and the Ace counts either 11 or 1 (and it may switch in the middle of a round). If a player cannot play a card that either makes 21 or keeps the pile below 21, they "bust" and the previous player wins the round. After a round is won, all players draw back up to 7 cards in hand and the cards played this round are discarded. If the draw pile is empty, shuffle the discard pile and place it face down to form a new draw pile. Play would then continue with the next player in turn order.

Face Cards - Face cards also have special abilities when played. When the Jack is played, you may remove another card from the round. For instance, if the pile contained a 2, 8, and 9, the active player could play a Jack and remove the 8. The new total of the pile is now 21, and the active player would win the round. When the Queen is played the active player exerts their influence over the round. If the round ends in a "bust," the player who most recently played a queen will win the round, even if they weren't the last player to play a card. Finally, if a player plays a king, the round immediately ends and they win the round.

Advancing Through the Board - If a player is the final player to leave a space on the game board, such as when three players are on the 3 of Clubs and they win a hand to move off of the 2 of Clubs, they pick up the card they moved off of.

And those are the rules! It's a relatively simple game to explain verbally, and so I gathered a few of my friends, and we sat down to play-test it.

## Play-Testing
The iterative nature of board game design is a common theme in every design book I've ever read. You sit down, play through the game, figure out what works and what doesn't, and then adjust the game to fit. This game was the first time I had progressed a play-test to the point of gathering other people, and it was certainly a nerve wracking experience.

That said, my friends were excellent. They spoke about their thoughts as we played, they offered suggestions for rule changes as we went, and overall provided an excellent group of people to play with. The first game illustrated the most glaring and frustrating issue with the game: you have too many cards. 7 cards in hand is way too many. Players would spend a noticeably long amount of time on their turns trying to search for the optimal play, and the game felt slow and reserved as a result. This game, in the ideal platonic sense of the game, wants to be a quick, take-that, barroom style game. It should be something you can plow through a game or two while waiting for your foot at a restaurant or over drinks in a pub.

So for the second game, we cut the number of cards in half. Now you have a maximum hand size of 4 cards.

We also noticed that the distribution of face cards was frustrating. Some players were able to gain a very early lead simply because they were dealt two of the kings in the starting hand. So we made a new rule for dealing starting hands. Before dealing starting hands, but after preparing the game board, remove all of the face cards from the deck. Deal starting hands from the numeral pile, and then shuffle the remaining number cards with the face cards. This made face card distributions much more even throughout the game, and it prevented any one player from running away with an early lead.

Then we played a second game. And it was noticeably more fun. People were laughing far more, turns took much less time, and it was just a better experience overall.

## Post-Mortem
Now, I absolutely intend to continue refining the rules for "Take the Crown" over the next few play sessions. The overall takeaways from both of the play-tests was that the face cards were all extremely powerful, and the Queen was too over powered to remain as she was. Furthermore, it felt as though being the person to begin a round placed you at a major disadvantage. Often times a hand would be finished in three cards, and you would get stuck in a cycle of repeatedly starting the round without ever being able win one. So, the new rules will be that if you win a round, you start out the next one.

Additionally, a proposal for changing the face cards has been brainstormed. First, the core idea of the queen is that you're investing a card by betting that the pile will bust later. Since she was also worth 10 points, often times people would play a queen and then claim the busted pile since they were the last player to play a queen. Now I see two ways to fix this, either change the way that the queen backtracks through the players so that the player who plays it can't claim the busted pile, or change it so that a queen can't cause a pile to bust. The latter idea seemed to fit with the thematic idea of the queen more, and so the queen now is worth 0 points on the pile. She's meant to be a gamble and an investment that might pay off if the other players can't force the pile to hit 21 exactly.

Next, the Jack is meant to be a card that allows you to nullify the actions of another player by removing one of their cards from play. With the nerfs to the queen, the jack seems to also get a natural buff since his action can nullify the investment of a player who chooses to play a queen card; however, that feels like too small of a buff. Plus, we can also nerf the king via adding a mechanic to the jack, and the king feels like he is too powerful as well.

In my mind, the king is meant to be a card that you play when the pile needs 12 or 13 points to finish off. You play the king in a situation where you can almost win, but wouldn't be able to with regular cards. The king lets you just move forward automatically by playing it whenever you have to start a round, and that feels out of character. So, now the jack has the ability to kill off a king. If a player plays a king, the next player in turn order can have a "take-that" moment where they can play a Jack. The jack kills off the king and play continues with the pile only containing a jack.

## In Conclusion
And that's it! "Take the Crown" is certainly going to be continually iterated upon over the next few weeks of play, but it's at a point where I'm excited to share it with everyone :) If you play the game, reach out to me and let me know what you think of it!

Until next time though,
-Andey
