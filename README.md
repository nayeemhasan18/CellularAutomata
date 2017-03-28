Assignment 1 – Spring 2015 Page 1 of 4
Faculty of Engineering and
Information Technology
School of Software
31927 - Applications Development with .NET
32998 - .NET Applications Development
SPRING 2015
ASSIGNMENT 1 SPECIFICATION
DUE DATE – 18th September 2015
FINAL DUE DATE – 24th September 2015
This assignment is worth 25% of the total marks for this subject.
ASSIGNMENT DOCUMNTS
This assignment is split into two documents.
1. Assignment Specification. This document contains the specification for what you will be
required to do.
2. Assignment Addendum. This document contains all other details regarding the
assignment, including assignment submission and the assessment scheme.
BACKGROUND
Cellular Automata are a fascinating area of computing science. The basic idea is to take some
2 or 3 dimensional space and break it up into a grid, with each square or cube in the space
being a cell. Each cell has a state or a number of states that evolve over time. How these
states evolve depends on the states of neighbouring cells and a set of rules relating them.
Perhaps the most famous example of Cellular Automata is the game of Life, developed by
John Conway and first published in Martin Gardner's "Mathematical Games" column in the
October 1970 and February 1971 issues of Scientific American.
The rules of Life are very simple. It uses a 2 dimensional space and each cell in the space has
a state that is either alive or dead. If exactly 3 of the 8 neighbouring cells of a cell are alive
then the cell becomes alive. If exactly 2 of the neighbouring cells are alive then the state of
the cell remains unchanged. In all other variations the cell dies. These rules are applied to
every cell in the space. When viewed on a computer the result is a pattern of dots that wildly
swirls around the screen. If you want to know more about Life, the Universe and Everything
then I highly recommend the book “The Recursive Universe” by William Poundstone. It is out
of print but you can pick up second hand copies via www.amazon.com. You can also
download a windows version of Life from
http://psoup.math.wisc.edu/Life32.html
In real life, Cellular Automata are used in many areas. Particularly to model real world
phenomena. Examples would be modelling galaxy formation, aerodynamic simulations and
the climate (including the effects of greenhouse gas emission).
Assignment 1 – Spring 2015 Page 2 of 4
REQUIREMENT
In this assignment you are to prepare a C# program that will run a simple 1 dimensional
automata. You can imagine the automata as being a line of cells that can have 4 possible
states. These states have the values 0 to 3 and each state is represented by the following
character, 0 by a space, 1 by a ‘.’, 2 by a ‘+’ and 3 by a ‘#. The following is an example of a set
of 12 cells
#++. .#+ .#
The Cellular Automata examines each cell in the line and then checks the cell on either side
of it. As part of the automata, wrap around is implemented. This means that the cell at the
far left uses the cell at the far right as its left neighbour and the cell at the far right uses the
cell at the far left as its right neighbour.
The program will then work out the value of the next state of each cell. For example, if the
cell has a state of 1 then the next state is 2, if the cell has a state of 3 then the next state is 0.
It will also work out the previous state. For example, if the cell has a state of 0 then the
previous state is 3, if the cell has a state of 3 then the previous state is 2.
The following rules are then applied to each cell.
1. If both of the neighbouring cells have a state equal to the next state then the cell is
changed to the previous state.
2. If only one of the neighbouring cells has a state equal to the next state then the cell is
changed to the next state
3. If both neighbours have the same state as the cell then the cell is changed to the next
state
4. If neither rule 1, 2 or 3 applies then the cell remains unchanged.
Assuming there are 7 cells in the line, we can see how the rules apply to the following
example.
0123456
#. .+++
Applying the rules to cell 0
 Rule 4 applies. The cells remains a #
Applying the rules to cell 1
 Rule 4 applies. The cell remains a .
Applying the rules to cell 2
 Rule 1 applies. The cell becomes a #
Applying the rules to cell 3
 Rule 2 applies. The cell becomes a +
Applying the rules to cell 4
 Rule 4 applies. The cells remains a +
Applying the rules to cell 5
 Rule 3 applies. The cell becomes a #
Assignment 1 – Spring 2015 Page 3 of 4
Applying the rules to cell 6
 Rule 2 applies. The cell becomes a #
The resultant output for the next generation will be
0123456
#.#++##
It’s important to note you can’t change cell 0 before you determine what happens to cell 1
and cell 5. The same applies to all the cells. You have to work them all out at once before
you can change them. The way to do this is to store the automata in an array and then use
another array to build up the new generation.
The following example uses 64 cells and has been run for 20 generations.
gen 1 ##+#+ +#. . #+. # # #++#+ +## + # .###. # . .+ +## + . +
gen 2 #.## .. ##.#.. #+.+ + #### ## + +..# #..+ ..#++ ## + ...+
gen 3 .# .... #.#... # + + + ++. .++...##+ +..+++
gen 4 ... ..++.. .#.+..+ + + ......... + +++...+++++.### .... ++++#+
gen 5 .+.#.++++.#.#+++++ + +..+++++++..+ +#+++++###++# ..++..+#####.
gen 6 +++#++##++#.#####+ + ++++#####++++ ######## ### ..+++++## #.
gen 7 +##########.# ## + +#### ####+ ..++##### . +
gen 8 ## #. . + ## . ## ..............++## ... +
gen 9 # ...... ....... + ....... ..++++++++++++++## .....+..#
gen 10 ..++++....+++++..+ .....+++++.....++############## ..++++++.#
gen 11 ..++##++++++###++++..+++++###+++++++## ..++####++
gen 12 ..++########## ####++++##### ######### ..............++## ##+
gen 13 .++## ###### ..++++++++++++++## ##.
gen 14 ++## ........... ...............++############## .. #.
gen 15 +## ..+++++++++..........+++++++++++++++## .... +
gen 16 ## ..++#######++++++++++++############### ..............++.. +
gen 17 # ..++## ############## ..++++++++++++++++..#
gen 18 ..++## ... ...............++##############++.#
gen 19 ..++## ..+..................+++++++++++++++## ##++
gen 20 ..++## ..+++++++++++++++++++++############### .......... ##+
Final hash = 3736
PROGRAM DETAILS
In the program you are to create, there will be 64 cells in your Cellular Automata space. You
will print a total of 20 generations of the Automata in exactly the same format as the example
above.
To do this you must do the following
1. Your program must use a command line argument to enter a positive integer greater than
zero. This integer will be a seed value you use with the random number generator. E.g.
>cell_autom 123
This is assuming you call your project cell_autom.
2. Your program must check to make sure the command line argument is correct. If not your
program must generate an error message that includes a message stating how the program
is to be used.
3. The CoinPuzzle lab shows how to use the random number generator. You will use it to
create numbers in the range 0 to 3 which will correspond to initial cell states.
The format of each line printed will be
Assignment 1 – Spring 2015 Page 4 of 4
1. “gen “. There will be two spaces after gen.
2. Generation number. This must be exactly two spaces. Single digit numbers will be
padded to the left with a space. Numbers start at 1 and finish at 20.
3. A space
4. The contents of the current generation of cells.
4. The final piece of information you will print is a hash value of the last line of cells
printed. A hash value is a number that is formed by jumbling data together to give a
semi-random number. You will calculate the hash with the following formula.
ℎ  = 	
 + 1 × 
. _


For example, using the final seven cells above
0123456
#.#++##
Hash Value = 1×3 + 2×1 + 3×3 + 4×2 + 5×2 + 6×3 + 7×3
= 3 + 2 + 9 + 8 + 10 + 18 + 21
= 61
The example printout above uses the seed value of 123, giving a final hash of 3736. Your
program must exactly match its output when using that seed value.
As part of this assignment you are expected to break it up into a sensible set of objects as part
of your program design.
ASSIGNMENT OBJECTIVES
The purpose of this assignment is to demonstrate competence in the following skills.
 Program design
 Array manipulation
 Creating classes and methods in C#
 Command Line Arguments
These tasks reflect all the subject objectives.
The solution I have for this assignment takes about 230 lines of code, including white space,
comments, etc. As part of your subject workload assessment, it is estimated this assignment
will take 25 hours to complete.
