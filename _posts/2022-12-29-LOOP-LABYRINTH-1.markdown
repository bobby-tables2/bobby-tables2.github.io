---
layout: post
title:  "Loop Labyrinth | A 3D labyrinth game with a looping world | Development Update 1"
date:   2022-12-29 13:10:00 +0800
categories: jekyll update
---

# What is Loop Labyrinth about?

![GIF of gameplay from Loop Labyrinth](/assets/images/loop_labyrinth1/gameplay1.gif)

Loop Labyrinth is actually my latest attempt at making a 3D labyrinth game in Unity. The main game mechanic that I spent about a year working on is that objects teleport to the other side of the board instead of falling off of it.

![The fundamental polygon of a torus.](https://upload.wikimedia.org/wikipedia/commons/thumb/f/f2/TorusAsSquare.svg/313px-TorusAsSquare.svg.png)

The idea of a looping board was inspired by [this video about topology.](https://youtu.be/lmcT2mP2bfE) More specifically, [the notion of a fundemental polygon.](https://en.wikipedia.org/wiki/Fundamental_polygon#Examples_of_Fundamental_Polygons_Generated_by_Parallelograms) From my very limited understanding it describes objects that have specific types of holes by using squares whose edges connect to each other in some way.

# What was it like to make Loop Labyrinth?

Initially, the biggest challenge for me was to implement a looping board from scratch, which was very difficult since Unity does not natively support weird geometrical sapces that warp like this.

![A character and its doppelganger](/assets/images/loop_labyrinth1/doppelganger.png)

My first eureka moment was when I remembered how old video games create the illusion of a mirror by having a body double mime the main character's actions.

![Body doubles](/assets/images/loop_labyrinth1/teleportation1.png) ![Teleportation](/assets/images/loop_labyrinth1/teleportation2.gif)

I would then have to create body doubles of each teleportable object in the game, and when the object reaches the edge of the board, just swap its position with the body double on the opposite edge.

I initially did this with colliders at each end of the board but this was unsuccessful. I settled on keeping track of the position of each object relative to the breadth and width of the board.

The next major obstacle I faced was that objects frequently fell out of the board when they teleported.

![Height adjustment](/assets/images/loop_labyrinth1/teleportation3.gif)

I tried to fix this by ensuring each body double and the original object had the same distance from the ground.

Both the body double would send a raycast downwards to measure their respective distance from the ground. The height of the body double would than be altered to match that of the original before teleportation occurs.

However, the solution ultimately seemed to also involve making the collider for the board very thick.

I also made various other quality of life improvements, such as ensuring that the board tilts in alignment with the camera (so that pressing W always makes the board tilt forwards).

# What are you currently working on?

I am currently working on a level editor for Loop Labyrinth.

![GIF of gameplay from Loop Labyrinth](/assets/images/loop_labyrinth1/editor.gif)

It was not easy. For the editor menu, I had to write a convoluted web of scripts that referenced each other in other to keep track of which object in the scene was being edited.

Another painful aspect was making the highlight effect when you select an object. I had to learn how to make a custom shader with ShaderGraph, and completely rework how the game used materials and shaders.

I'm currently struggling with making editor gizmos to move and rotate objects in the level. I had to use Unity's line renderer to draw 3D arrows around objects, but for whatever reason it suddenly broke when I tried to make them move with the object. I also don't really what math equations to use to make the object follow the mouse along an axis properly.

I plan to replace the editor with [GILES](https://github.com/Unity-Technologies/giles) eventually.