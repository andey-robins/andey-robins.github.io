---
layout: post
title: Dwarf Fortress and Fixing Minecraft
---
## Immersion
I first discovered Dwarf Fortress back when I was a freshman in high school. I had been playing minecraft for nearly four years at that point, I was just beginning to develop a love of programming, and the idea of procedurally generating societies was fascinating to me. I never really got into the game itself (I found the interface difficult to understand and use and my computer at the time was unnable to accurately simmulate the depth of the game), but the idea of a civilization being able to be simulated to rise, conquer, and then fall was fascinating to me.

I began to learn about the basics of anthropology and constructing cultures from nothing but fiction. I was fascinated by JRR Tolkein and his ability to basically write the entire history of middle earth, much of which was unnecesarry for the story of Frodo and Sam, George RR Martin creating a world that seemed more realistic and interesting than the one I lived in, and any other form of long form, world building fiction I could get my hands upon.

I finally stepped back a few months ago and asked myself, why did I find these works of fiction so interesting? And after much thought, everything I knew circled back around to complete immersion. The worlds created in these books seemed fleshed out and alive. The people within these stories didn't spend their dialogue telling you what was going on in the world. Environmental variables and other forms of story telling shared the history of the world.

This complete immersion drew me into the stories when they might otherwise have been less than completely engaging. There's a reason that, despite not enjoying the entirety of Lord of the Rings, I tried to get through every book.

So let's return to Dwarf Fortress. That game uses this idea of environmental storytelling and NPC storytelling to build a world that the player feels as if they're only getting a glimpse of it. It isn't the volume of information that is engaging, it's the idea that a player has no control over those histories and stories that have unfolded within the world. Compare this with a game like Minecraft. In Minecraft the player is a god, the world is theirs to do with as they wish. When they want to make a history for something, they can just make it up. Minecraft is a wonderful game, but it doesn't engage me in the same way that Dwarf Fortress does.

## Fixing Minecraft
Making game systems in which players aren't the only active agents is what makes these worlds so interesting. This AI creates a world that feels breathing and alive. So how can we make these systems seem living despite the world being cold steel? How could we transform Minecraft to be environmentally engaging in the same way Dwarf Fortress is?

The Villagers.

We need to give the villagers a new motivation. When the player is gone, they should do things to improve their village. I propose that these actions can be categorized into four different levels, similar to [Maslow's Hierarchy of Needs](https://en.wikipedia.org/wiki/Maslow's_hierarchy_of_needs).

|Level|Actualization|
|---|---|
|Body|Food, Water, etc.|
|Safety|Home, Defense, etc.|
|Belonging|Community, Friends, etc.|
|Expression|Art, Culture, etc.|

## Body
The realization of the body/physical level is pretty simple. There are already farms placed all around most villages, and in recent updated villagers have begun passively tending these fields. This gives a good indication of the world being alive. If the actors within the system are caring for their own basic needs, it stands to reason that they are doing things intelligently. Fulfilling these basic resource gathering requirements is a good first step towards building immersive worlds.

## Safety
One of the biggest immersion breakers that I've seen in Minecraft comes when a creeper blows up part of a village (because I, an upright citizen, would never destroy a villager's home). The hole in the road and building just stay there. Nothing is ever repaired, and over time the village just deteriorates. Instead of just generating the world passively one time, make the villagers take their collected resources and begin repairing broken infrastructure.

This accomplishes two things. It keeps the world in good shape, something that is always nice and immersive when you aren't focussed on avoiding massive potholes everywhere in the ground. It also makes the people in the village seem alive and conscious. They're actively working to maintain their home and lifestyle, a very human trait.

These goals don't even need massive complex reasoning behind them. If the building simply regenerate slowly after a day or two, it would seem as though a villager went out, gathered some resources, and fixed their home themselves. As far as implementation, while requiring more resources than just leaving the broken pieces around, it would still be low on the resource constraints on a simulation or game.

If a zombie attack were to come into the village, have the villagers begin to build a wall. Something as simple as a programatic trigger could start a phase of construction. From there, each time the area is loaded from the save file, move the wall forward one step until it has been completed. It's a somewhat simple concept, but it makes the NPCs seem to react to the world around them independent of the player.

## Belonging
This is where we begin to have to visually demonstrate less quantifiable concepts like community. One of the easiest ways I see to do this is simply expanding the village. It stands to reason that a community that could protect themselves and provide enough basic resources to live would begin to attract other people. Additionally, new children, growing up, would further expand the population of each village. Growing the village in size would visually indicate this growth of a community.

People coming into the area would also lead to other community structures being built. Things like bonfires, wells, bath houses, genereal stores, and city squares are all present in larger villages where a community has been built, but lacking in smaller towns where they struggle just to survive. Again, the resource cost of creating this level of immersion is not nothing, but it isn't ridiculously high. It's possible to make it happen with only marginally more programming than the changes in the Safety segment.

However, this level is where we begin to need more complex ideas to begin emerging. We need to start telling the stories of these civilizations. I see a few ways to go about doing that, which we may expand upon in a later blog post, but for now I'm going to talk about what I view as the simpleset way to go about doing this.

Like both of the games we've discussed so far, the answer lies in procedural generation. This time, we're using it to create artifacts of this civilization. Things like a famous sword, a historic cup, or some other functional object. These objects are generated with a somewhat generic story that refers to a randomly generated person of history. For instance: "The sword wielded by Rugathar in the Battle of Arridar. Legend tells that over two dozen men were slain by this sword before Rugathar was dealt his mortal blow."

Short quips like this lead to an idea that there is more to the world than is being hinted at, but still leaves much of it open to the imagination of a player, ultimately what creates the strongest immersion of all.

## Expression
This segment of generation would introduce things like art and writen works, pieces of history that are preserved not for any practical reasons like a sword, but for the sole purpose of maintaining a story of those who came before. Ideas related to how to drive this Expressive segment of a civilization tie very closely with the postponed ideas above, so watch for a second blog post detailing how we can give purpose to these figments of a coder's immagination.

Until next time.
-Andey
