#  What is programming?
All programs use basic instructions as building blocks

Common ones in english
- Do this; then do that
- If this condition is true, perform this action; otherwise, do that action
- Do this action exactly 27 times
- Keep doing this until that condition is true

Instructions can be combined to implement more intricate decisions.

Example program
```
passwordFile = open('SecretPasswordFile.txt')
secretPassword = passwordFile.read()
print('enter your password.')
typedPassword = Input()
if typedPassword == secretPassword:
	print("Access Granted")
	if typedPassword == "12345":
	print("That password is one that an idiot puts on their luggage.")
	else;
	print("Access Denied")
 ```

# What is Python?
	Python is a programming language (with syntax rules for writing what is considered valid python code) and the python interpreter software that reads source code (written in the python language) and preforms its instructions

	The name python comes from the surreal british comedy group Monty Python
 
# Programmers Don't Need to Know Math
A common anxiety about learning to program is the notion that it requires a lot of math. However the truth couldn't be more contrary, not requiring more than basic arithmetic. In fact, being good at programming isn't that much different from being good at solving Sudoku puzzles. 
To solve a Sudoku puzzle, the numbers 1 through 9 must be filled in for each row, each column, and each 3×3 interior square of the full 9×9 board. Some numbers are provided to give you a start, and you find a solution by making deductions based on these numbers. In the puzzle shown in Figure 0-1, since 5 appears in the first and second rows, it cannot show up in these rows again. Therefore, in the upper-right grid, it must be in the third row. Since the last column also already has a 5 in it, the 5 cannot go to the right of the 6, so it must go to the left of the 6. Solving one row, column, or square will provide more clues to the rest of the puzzle, and as you fill in one group of numbers 1 to 9 and then another, you’ll soon solve the entire grid.

![[00016.jpg]]

_Figure 0-1: A new Sudoku puzzle (left) and its solution (right). Despite using numbers, Sudoku doesn’t involve much math. (Images © Wikimedia Commons)_

Just because Sudoku involves numbers doesn’t mean you have to be good at math to figure out the solution. The same is true of programming. Like solving a Sudoku puzzle, writing programs involves breaking down a problem into individual, detailed steps. Similarly, when _debugging_ programs (that is, finding and fixing errors), you’ll patiently observe what the program is doing and find the cause of the bugs. And like all skills, the more you program, the better you’ll become.

