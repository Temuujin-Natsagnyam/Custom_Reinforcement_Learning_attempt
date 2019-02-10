This is a very crude experimental Machine Learning experiment project I did out of curiosity. It built onto the map code in the map repository.

###Background
After watching a youtube non-technical introductory video into Neural Networks (https://youtu.be/aircAruvnKk), with the initial intent to implement it into my traversable 2D string map I made. I wanted to code what I understood and took away from his video. But it wasn't a technical programming introduction at all, so I had to use what I already learned in Python. 

The video explained concepts such as neurons (and how they simply contain numbers), neuron connections (or weights), scoring, and somehow intelligently recalibrating the weights according to the score. There were conceptual explanations of gradient descent and random initialisation.

#Algorithmic logic behind it
I created a 2D array (named dummy_weights) with identical size to the map(which is basically a 2D array), which contained random values. This was my understanding of the randomly initialised neuron connections or weights associated to each decision the agent(the thing that moves around the map) could make. Then I automated (turned it user independent) the agent to simply assess its four possible moves(up,down,left,right) based on the 2D array (dummy_weights)'s values. So in the beginning it moves randomly. The goal is a point G on the map

The next stage was to give the agent punishments for wrong decisions. My understanding of this concept is to lower the neural weight associated with that decision/move which caused the punishment. So I simply(crudely) just set it so that when it moves to a "X"(wall) it deducts int(5) from the 2D array(dummy_weights)'s corresponding element. Since the agent's decision is based on the values inside dummy_weights I thought it qualifies as a punishment. The state of the bot at this stage is that after a few moves it simply moves left and right forever. 

My next step was to somehow intelligently make the agent stop moving back to its previous after every single move without affecting the weight of its previous state, because it is not necessarily a wrong move. I wanted to come up with a dynamic backtracking solution, but in the end I simply(crudely) just made the agents decisions to simply not assess its previous state when comparing dummy_weight values. This worked for me since I didn't want to affect the weights. At this point, I thought to myself that I've finally stopped the un-productive repetitive moves done by the agent, but after a few dozen moves the agent very commonly simply circles around the same 4 states continuously. 

I realised that the movements were counter-productive because only I know what the goal is, not the agent. So, its best survival tactic is to simply circle forever (that's what I like to think, it's probably worlds far from something that sophisticated such as survival). I was puzzled as to how to incentivize it to move towards G without meddling with the randomly set weights as the programmer(only the agent should change the weights), otherwise that would no longer be a learning algorithm. So, I brainstormed different solutions but they were all beyond my capabilities, so I compromised for a function which temporarily reduced the value of weights based on how far way it is from the goal. I do this by: When the agent is assessing its next three possible moves according to the values in dummy_weights, a function determines the hypotenuse from that potential next point to the goal and that hypotenuse is deducted from the weight. So moves further from goal are less attractive, but after move is finished that deduction is undone. This is kind of like how when we are lost in a maze, but we still have a general directional sense of where the exit is if we ignore the walls.

Now you can see the algorithm works, and if you run map_agent_thingy.py, you can see its performance over multiple generations. (I mean generations as to how many times its run consecutively). More often than not the trend is always decreasing over each time the agent tries the map. 

#Key Takeaways
Having finished it now, I concede it's more of a weighted pathfinding algorithm than a machine learning neural network. But I proudly stand by it. I think it displays key concepts of Neural Networks and Reinforcement Learning. Such as improvement over each attempt, weights(although not really), punishments and incentives, Virtual training environments. This project has been extremely fun and I plan to come back to this once I am confident with my Machine Learning technical abilities. 


