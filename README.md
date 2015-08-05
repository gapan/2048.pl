2048.pl
=======

This is an implementation of the popular 2048 puzzle game in Prolog. The
objective of the game is to slide numbered tiles on a grid to combine
them and create a tile with the number 2048.

The user can play against the PC, or he/she can watch the PC trying to
solve the game.

Playing against the PC
----------------------

After loading the `2048.pl` script in prolog, in order to play against
the PC, you just need to run:

    ?- play.

The board will show up in an initial position and wait for your move,
like this:

        _    _    2    _ 
        _    _    2    _ 
        _    _    _    _ 
        _    _    _    _ 
    
    Left: h/a, Down: j/s, Up: k/w, Right: l/d, Show board: b, Quit: q, Help: ? 
    
    Your move?


And then you can make your next move, using the keyboard, as described.

PC vs PC
--------

This is the interesting part, although be warned that it is slow. Really
slow. You can let the PC try to solve the game by running:

    ?- ai.

This works by calculating all possible board positions after 4 moves.
You can change the search depth by running `ai` with an argument. To use
a search depth of 3, you can run:

    ?- ai(3).

The number of possible board positions is huge, so increasing the search
depth beyond a certain level will probably make your PC run out of RAM.
Using a search depth equal to 3, it runs quite fast, but the algorithm
usually manages to create only a 512 tile, or sometimes a 1024 tile.
With the default search depth of 4, it will be slower, but it will
usually solve the game. Using a search depth of 6 or more, will solve
the game almost every time, but will require huge amounts of RAM. If you
use a search depth bigger than 4, you'll probably need at least 8GB of
RAM. If you go over a search depth of 6, you'll probably need at least
24GB. In such cases, you will most probably need to increase the RAM
assigned to the prolog global stack and local stack. If you want to
increase each one to 10GB for example, you can run:

    ?- set_prolog_stack(global, limit(10*10**9)). 
    true. 
    
    ?- set_prolog_stack(local, limit(10*10**9)). 
    true. 

If you do run out of RAM, you'll get a message like this:

    ERROR: Out of global stack.

Scores for each possible move up to the specified search depth are
calculated. These are simply the sum of squares of all values of tiles
on the board. The maximum is selected. The scores are shown on screen
for every move. Here are the first 3 moves for a game:

    ?- ai. 
        2    2    _    _ 
        _    _    _    _ 
        _    _    _    _ 
        _    _    _    _ 
    Scores: L=81356800 R=81356800 U=0 D=77061160, Move: right 
        _    _    _    4 
        _    _    _    _ 
        _    _    _    _ 
        2    _    _    _ 
    Scores: L=105760160 R=105760160 U=105760160 D=105760160, Move: right 
        _    _    _    4 
        _    _    2    _ 
        _    _    _    _ 
        _    _    _    2 
    Scores: L=134629320 R=134629320 U=104081840 D=123410480, Move: right

L, R, U and D values are the scores for moving left, right, up or down,
respectivelly.

Needless to say that there exist a lot of faster implementations that solve
the game a lot more efficiently that this does. 
