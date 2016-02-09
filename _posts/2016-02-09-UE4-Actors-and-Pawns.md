---
layout: post
title: Actors versus pawns
categories: 【 Learning C++ by Creating Games with UE4 】
tags: Unreal_Engine
---

### Actor

A UE4 <mark>actor</mark> (the Actor class) object is the basic type of the things that can be placed in the UE4 game world. In order to place anything in the UE4 world, you must derive from the Actor class.

### Pawn

A <mark>Pawn</mark> is an object that represents something that you or the computer's Artificial Intelligence (AI) can control on the screen. The Pawn class derives from the Actor class, with the additional ability to be controlled by the player directly or by an AI script. When a pawn or actor is controlled by a controller or AI, it is said to be possessed by that controller or AI.
