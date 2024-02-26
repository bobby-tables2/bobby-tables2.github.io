---
layout: post
title: "August 2023 update"
date: 2023-8-6 22:48:00 +0800
categories: jekyll update
---

> I am exhausted.

# What have I been up to?
I'm starting university, and between the six month gap between this post and the last post I've done a bunch of things.

- Contributing to the Centuria GitHub repository
- Working on a bunch of side projects, but no progress
- Studying stuff related to computing, economics and mathematics

# My contributions to the Centuria repo
Centuria is a Java server that allows people to play the game [Feral (use cntr+F)](https://www.guv1.com/professional-1/2019/4/26/uden-22-wildworks-studio-networking) after its servers closed, something akin to Club Penguin private servers. \(To be clear, my contributions did not contain anything cryptocurrency or blockchain related.\)

I contributed to the project because I was always fascinated with the idea of game hacking.

My contributions are as follows:
- Reimplementing server-side support for minor room editing features
- Reimplementing server-side support for minigames

It was very difficult because:
- Studying the game's behaviour is difficult because the game's code is obfuscated
- I didn't know how to debug Java programs in my IDE of choice

# Progress on other side projects
- **IR blaster that controls lights:** Progress stalled due to difficulty with writing C++ code, as well as technical issues with electrical components.
- **Loop Labyrinth:** I haven't done anything with it because its about complicated math, and I have made the decision to private the repository containing its code.

# Topology
I tried to study topology for Loop Labyrinth and my grasp of it is still very loose. 

Regardless, a topology on a set of points S is a collection of subsets of S (regions within S where there are points that are connected to each other) such that the union of all subsets gives back S (every point makes up S), and the intersection of all subset is still in the topology (there is a smallest possible region that still contains points that are connected to each other).

A homeomorphism from space 1 to space 2 is a continuous one-to-one function that assigns each point in space 1 to a point in space 2. For example, take the points on a cube, normalise the coordinates of those points(divide by the length from origin), and you now have the points on a sphere.

Loop Labyrinth isn't very topology related but it does revolve around homeomorphisms. By teleporting objects from one edge of a plane to another, I effectively created a homeomophism that sewed together the two edges of the plane.