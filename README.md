<h1>ExpNo 7 : Implement Alpha-beta pruning of Minimax Search Algorithm for a Simple TIC-TAC-TOE game</h1> 
<h3>Name:   HARSETHA J    </h3>
<h3>Register Number: 212223220032         </h3>
<H3>Aim:</H3>
<p>
Implement Alpha-beta pruning of Minimax Search Algorithm for a Simple TIC-TAC-TOE game
</p>
<h1>GOALS of Alpha-Beta Pruning in MiniMax Search Algorithm</h1>

<h3>Improve the decision-making efficiency of the computer player by reducing the number of evaluated nodes in the game tree.</h3>
<h3>Tic-Tac-Toe game implementation incorporating the Alpha-Beta pruning and the Minimax algorithm with Python Code.</h3>
<h1>IMPLEMENTATION</h1>

The project involves developing a Tic-Tac-Toe game implementation incorporating the Alpha-Beta pruning with the Minimax algorithm. Using this algorithm, the computer player analyzes the game state, evaluates possible moves, and selects the optimal action based on the anticipated outcomes.

<h1>The Minimax algorithm</h1>

recursively evaluates all possible moves and their potential outcomes, creating a game tree.

<h1>Alpha-Beta pruning</h1>

Alpha–Beta (𝛼−𝛽) algorithm is actually an improved minimax using a heuristic. It stops evaluating a move when it makes sure that it’s worse than a previously examined move. Such moves need not to be evaluated further.

When added to a simple minimax algorithm, it gives the same output but cuts off certain branches that can’t possibly affect the final decision — dramatically improving the performance
<hr>
<h2>Sample Input and Output:</h2>

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/8d5e329a-9aff-41a6-bcf0-46efa10e1b92)
![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/438b242d-54ba-443e-b040-a936e6ae3b55)
![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/99a33390-fa11-4ade-a19f-e93bcd7aaec9)
![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/440797bd-53cb-49c1-b18d-89776864c3e7)
![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/81575a16-26b2-46f1-a8ac-27c9ed0a0fe5)

# PROGRAM
```
import math
board = [" " for _ in range(9)]
def print_board():
  print()
  for i in range(0, 9, 3):
    print(f" {board[i]} | {board[i+1]} | {board[i+2]} ")
    if i < 6:
      print("---|---|---")
  print()
def check_winner(player):
  win_combos = [
      (0, 1, 2),
      (3, 4, 5),
      (6, 7, 8), 
      (0, 3, 6),
      (1, 4, 7),
      (2, 5, 8), 
      (0, 4, 8),
      (2, 4, 6),  
  ]
  return any(board[a] == board[b] == board[c] == player for a, b, c in win_combos)
def is_draw():
  return " " not in board
def minimax(depth, is_maximizing, alpha, beta):
  if check_winner("O"):  
    return 10 - depth
  if check_winner("X"):  
    return depth - 10
  if is_draw():
    return 0

  if is_maximizing:
    best_score = -math.inf
    for i in range(9):
      if board[i] == " ":
        board[i] = "O"
        score = minimax(depth + 1, False, alpha, beta)
        board[i] = " "
        best_score = max(best_score, score)
        alpha = max(alpha, best_score)
        if beta <= alpha:  
          break
    return best_score
  else:
    best_score = math.inf
    for i in range(9):
      if board[i] == " ":
        board[i] = "X"
        score = minimax(depth + 1, True, alpha, beta)
        board[i] = " "
        best_score = min(best_score, score)
        beta = min(beta, best_score)
        if beta <= alpha:  
          break
    return best_score


def best_move():
  best_score = -math.inf
  move = -1
  for i in range(9):
    if board[i] == " ":
      board[i] = "O"
      score = minimax(0, False, -math.inf, math.inf)
      board[i] = " "
      if score > best_score:
        best_score = score
        move = i
  board[move] = "O"

print("Tic-Tac-Toe: You are X, Computer is O")
print("Positions are 1 to 9 (top-left to bottom-right)")
print_board()

while True:
  try:
    pos = int(input("Enter your move (1-9): ")) - 1
    if pos < 0 or pos > 8 or board[pos] != " ":
      print("Invalid move! Try again.")
      continue
  except ValueError:
    print("Please enter a valid number between 1 and 9.")
    continue

  board[pos] = "X"
  print_board()

  if check_winner("X"):
    print("You win!")
    break
  if is_draw():
    print("It's a draw!")
    break

  print("Computer is thinking...")
  best_move()
  print_board()

  if check_winner("O"):
    print("Computer wins!")
    break
  if is_draw():
    print("It's a draw!")
    break
```
# OUTPUT

<img width="725" height="663" alt="image" src="https://github.com/user-attachments/assets/0576bd90-cfab-4f23-80e4-12f95f4acdc6" />

# RESULT

Thus, the Tic-Tac-Toe game using the Minimax Algorithm with Alpha-Beta Pruning was successfully implemented in Python.
