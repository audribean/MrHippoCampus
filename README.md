# Mr. Hippocampus the Self-Learning Robot

Mr. Hippocampus is our contestant for the COGS 300 Virtual Robot Competition. The goal of the competition is to collect the majority of target balls within three minutes. Two robots are pitted against each other at a time, and each has a "home base" to carry targets to.

Here is our model, developed in Blender. Mr. Hippocampus makes clown noises upon firing lasers.
![The model of our robot, a hippo wearing clown clothes](/HippoPreview.png)


Basic robot implementation can be found in **CogsAgent.cs**

Strategy and self-learning implementation can be found in **Mr_Hippocampus.cs**

## Strategy

Our robot implements the following strategy, composed of three "modes":

#### COLLECT:
When Mr. Hippocampus has less than the majority (5 targets) needed to win,
it will collect the nearest targets until it does. It will return to the base
when it has at least three targets when there are no targets at the base. Once there are
at least three targets at the base, it will collect and return at least the minimum remaining balls 
(5 - # balls at base) to get the majority. This is to reduce the number of trips it needs to make.

#### DEFENSE:
When Mr. Hippocampus has at least 5 targets in its base, it will stay there and
laser the enemy if it approaches. If it is able, it will avoid enemy lasers by
moving whenever the enemy is directly facing it. Otherwise, it will shoot a constant
defensive line of lasers around the base. 

#### CRIME:
If an enemy is carrying at least one target nearby, Mr. Hippocampus will shoot it. 
If the enemy has the majority of balls and there are no more balls on the floor, 
Mr. Hippocampus will steal from the enemy. 

Mr. Hippocampus will try to dodge if it can; it has punishments for being frozen and dropping
targets. 

## Implementation
We first created our own demo of this strategy using manual keyboard controls, then trained the robot to follow it using Generative Adversarial Imitation Learning (GAIL) and Behavioral Cloning.

To promote self-learning and adherence to our strategy, an additional rewards system was added.

We then ran simulations of the competition to train the robot. The results of training can be found in **Agent.nn**
