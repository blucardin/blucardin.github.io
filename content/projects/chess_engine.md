---
title: "Chess Engine"
date: 2025-07-13T03:20:23-07:00
draft: false
---

<iframe style="border:1px #FFFFFF none" src="https://blucardin.github.io/chess_engine/" title="iFrame" width="100%" height="500vh" scrolling="no" frameborder="no" allow="fullscreen"></iframe>

## I Wrote a Chess Engine!

You can play it in the IFrame above, or [here](https://blucardin.github.io/chess_engine/). 

It uses minimax trees with alpha-beta pruning and a human-generated evaluation function. 

Then to make it faster, instead of evaluating the board entirely at the end of every search, it just evaluates the board once at the start, and tracks it's value down through the tree by applying the value delta caused by each move.  

Then, since we know if a move is good or bad in the short term by looking at it's value delta, we can maximize alpha/beta cuts by sorting the list of possible moves at every node (except the last) before we explore. Effectively, implementing 1-ply iterative deepening at every node. 

And, I wrote it in Rust using the Bevy game engine, so it compiles to WebAssembly and runs in the browser - isn't that neat? And because it is so fast, it can look 6 moves into the future without significant wait times.  

I am still working on optimizing the memory usage - right now it is copying every board at every possible move to check if the king is in check, and I know I can write something better and faster. 

I am planning to implement neural network or evolutionary guided heuristic functions in the future, but with limited experiments, using even a shallow neural network to evaluate board transpositions proved to be too slow to allow a lookahead of more than a few moves. If I get around to it, I would even like to write something that used rollouts to estimate value for monte-carlo tree search. 

I am extremely satisfied with this project, it can even beat some of my friends who are 1500+ ELO players. Next step is to connect it to the Lichess Bot API so I can get its ELO confirmed. 


