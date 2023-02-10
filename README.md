# connectfour.githubio
import turtle

# Define some constants
ROWS = 6
COLUMNS = 7
SQUARE_SIZE = 100
OFFSET = 50

# Create the turtle object
t = turtle.Turtle()
t.speed(0)

# Draw the board
for row in range(ROWS):
    for column in range(COLUMNS):
        t.penup()
        t.goto(column * SQUARE_SIZE - OFFSET, row * SQUARE_SIZE - OFFSET)
        t.pendown()
        for _ in range(4):
            t.forward(SQUARE_SIZE)
            t.left(90)

# Initialize the game board
board = [[None for _ in range(COLUMNS)] for _ in range(ROWS)]

# Play the game
while True:
    # Ask for the player's move
    column = int(input("Enter a column (0-6): "))
    if column < 0 or column >= COLUMNS:
        print("Invalid move!")
        continue

    # Find the next open row in the specified column
    for row in range(ROWS - 1, -1, -1):
        if board[row][column] is None:
            break
    else:
        print("Column is full!")
        continue

    # Place the piece on the board
    board[row][column] = "red"

    # Draw the piece on the screen
    t.penup()
    t.color("red")
    x, y = (column * SQUARE_SIZE - OFFSET, row * SQUARE_SIZE - OFFSET)
    t.goto(x + SQUARE_SIZE / 2, y + SQUARE_SIZE / 2)
    t.pendown()
    t.begin_fill()
    t.circle(SQUARE_SIZE / 2 - 10)
    t.end_fill()

    # Check for a win
    if (
        any(
            all(board[row][column] == "red" for row in range(ROWS))
            for column in range(COLUMNS)
        )
        or any(
            all(board[row][column] == "red" for column in range(COLUMNS))
            for row in range(ROWS)
        )
        or all(board[i][i] == "red" for i in range(ROWS))
        or all(board[i][ROWS - i - 1] == "red" for i in range(ROWS))
    ):
        print("Red wins!")
        break

# Hide the turtle and exit
t.hideturtle()
turtle.done()
