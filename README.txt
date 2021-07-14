# Tic-tac-toe

"""
tic tac toe

1. board
2. while
3. quit
4. check input 1. isnum, 2. bounce
5. istkaen?
6. add to board active_user
7. iswin 1. check_row, 2. check col 3. check diag
"""

board = [
        ['_', '_', '_'],
        ['_', '_', '_'],
        ['_', '_', '_']
        ]

user = True
turn = 0

def display_board(board):
    for row in board:
        for slot in row:
            print(slot, end='  ')
        print()
    
def to_quit(user_input):
    if user_input == 'q'.casefold():
        print("Thanks for playing.")
        return True
    else: return False

def check_input(user_input):
    # check if it is num
    if not isnum(user_input): return False
    user_input = int(user_input)
    # check if it is from 1 to 9
    if not bound(user_input): return False
    else: return True

def isnum(user_input):
    if not user_input.isnumeric():
        print("It is not a valid number.")
        return False
    else: return True

def bound(user_input):
    if user_input > 9 or user_input < 1:
        print("This is a out of bounce.")
        return False
    else: return True

def istaken(coords, board):
    row = coords[0]
    col = coords[1]

    if board[row][col] != '_':
        print("This place is already taken.")
        return True

def  coordinate(user_input):
    row = int(user_input/3)
    col = int(user_input%3)

    return (row, col)

def add_to_board(coords, board, active_user):
    row = coords[0]
    col = coords[1]
    board[row][col] = active_user
    
    
def current_user(user):
    if user: return 'X'
    else: return '0'

def iswin(user, board):
    if check_row(user, board): return True
    if check_col(user, board): return True
    if check_diag(user, board): return True

def check_row(user, board):
    for row in board:
        complete_row = True
        for slot in row:
            if slot != user:
                complete_row = False
                break
        if complete_row: return True
    return False

def check_col(user, board):
    for col in range(3):
        complete_col = True
        for row in range(3):
            if board[row][col] != user:
                complete_col = False
                break
        if complete_col: return True
    return False

def check_diag(user, board):
    if board[0][0] == user and board[1][1] == user and board[2][2] == user: return True
    elif board[0][2] == user and board[1][1] == user and board[2][0] == user:   return True

while turn < 9:
    active_user = current_user(user)
    display_board(board)
    user_input = input("\nPlease enter a number from 1 to 9: ")
    if to_quit(user_input): break
    if not check_input(user_input):
        print("Please try again.")
        continue
    user_input = int(user_input) - 1
    coords = coordinate(user_input)
    if istaken(coords, board):
        print("Please try again")
        continue
    add_to_board(coords, board, active_user)
    if iswin(active_user, board):
        print(f"{active_user.upper()} won!")
        break
    turn += 1
    print("Tie :)")
    user = not user

input()
