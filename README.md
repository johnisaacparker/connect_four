# connect_four
Play my Python Connect Four game!
import numpy as np
ROW_COUNT = 6
COL_COUNT = 7
def create_board():
  board = np.zeros((ROW_COUNT, COL_COUNT))
  return board

def drop_piece(board, row, col, piece):
    board[row][col] = piece
    

def is_valid_location(board, col):
    return board[ROW_COUNT-1][col] == 0

def get_next_open_row(board, col):
    for r in range(ROW_COUNT):
        if board[r][col] == 0:
            return r
def print_board(board):
    print(np.flip(board, 0))
    
def winning_move(board, piece):
    
    #check all horizontal locations for win
    for c in range(COL_COUNT-3):
        for r in range(ROW_COUNT):
            if board[r][c] == piece and board[r][c+1] == piece and board[r][c+2] == piece and board[r][c+3] == piece:
                return True
    
    #check vertical locatons for win
    for c in range(COL_COUNT):
        for r in range(ROW_COUNT-3):
            if board[r][c] == piece and board[r+1][c] == piece and board[r+2][c] == piece and board[r+3][c] == piece:
                return True
            
    #check positively sloped diagonals
    for c in range(COL_COUNT-3):
        for r in range(ROW_COUNT-3):
            if board[r][c] == piece and board[r+1][c+1] == piece and board[r+2][c+2] == piece and board[r+3][c+3] == piece:
                return True
            
    
    #check negatively sloped diagonals
    for c in range(COL_COUNT-3):
        for r in range(3, ROW_COUNT):
            if board[r][c] == piece and board[r-1][c+1] == piece and board[r-2][c+2] == piece and board[r-3][c+3] == piece:
                return True
board = create_board()
game_over = False
turn = 0

while not game_over:
  #ask for player 1 input
  if turn == 0:
    col = int(input('Player 1, make your selection.(0-6) >'))
    
    if is_valid_location(board, col):
        row = get_next_open_row(board, col)
        drop_piece(board, row, col, 1)
    
    if winning_move(board, 1):
        print('Player 1 Wins!')
        game_over = True
    
  #ask for Player 2 input
  else:
      
      col = int(input('Player 2, make your selection.(0-6) >'))
      
      if is_valid_location(board, col):
        row = get_next_open_row(board, col)
        drop_piece(board, row, col, 2)
        
      if winning_move(board,1):
        print('Player 1 Wins!')
        game_over = True     
  turn += 1
  turn = turn % 2
  print_board(board)
