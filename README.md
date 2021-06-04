# znaaz-neiu-AI

final_project.py

import sys
import random 

board=[" "," "," "," "," "," "," "," "," "]

def makeBoard(board):
    
    print(board[0],"|",board[1],"|",board[2])
    print('*********')
    print(board[3],"|",board[4],"|",board[5])
    print('*********')
    print(board[6],"|",board[7],"|",board[8])

print("TicTacToe")

hlp=sys.argv

if len(hlp) > 1:
 hlp1=str(hlp[1])

 if(hlp1=="help"):
    print("The tictacoe is a two player game, where you will play against a bot.Bot represents x on board and you are represented as any letter that you have selected.In order to win you should block the Bot from putting x three times in a row,column or diagnol,likewise you will win only if you can put your letter 3 times in a row, column or diagnol.All the best!")

player_letter=input("Enter any letter but not x:")
print("Select any positions from 0-8 to make moves on board.")


print("Bot's move is represented as x and your move as the letter given by you.")
  
def gameWonByPlayer():
        
        move=1
        if move==1 :
            if board[move]==player_letter and board[move+1]==player_letter and board[move-1]==player_letter:
                return True
        move=7
        if move==7 :
            if board[move]==player_letter and board[move+1]==player_letter and board[move-1]==player_letter:
                return True
        move=3    
        if move==3:  
            if board[move]==player_letter and board[move+3]==player_letter and board[move-3]==player_letter:
                return True 
        move=5
        if move==5 :
            if board[move]==player_letter and board[move+3]==player_letter and board[move-3]==player_letter:
                return True 
        move=4
        if move==4 :
            if board[move]==player_letter and board[move+1]==player_letter and board[move-1]==player_letter:
                return True
        if move==4 :
            if board[move]==player_letter and board[move+3]==player_letter and board[move-3]==player_letter:
                return True
            
        if move==4: 
            if board[move]==player_letter and board[move+2]==player_letter and board[move-2]==player_letter:
                return True
        if move==4: 
            if board[move]==player_letter and board[move+4]==player_letter and board[move-4]==player_letter:
                return True
        else:
            return False



def gameWonByBot():
        
        move=1 
        if move==1 :
            if board[move]=="x" and board[move+1]=="x" and board[move-1]=="x":
                return True
        move=7
        if move==7 :
            if board[move]=="x" and board[move+1]=="x" and board[move-1]=="x":
                return True
        move=3    
        if move==3:  
            if board[move]=="x" and board[move+3]=="x" and board[move-3]=="x":
                return True 
        move=5
        if move==5 :
            if board[move]=="x" and board[move+3]=="x" and board[move-3]=="x":
                return True 
        move=4
        if move==4 :
            if board[move]=="x" and board[move+1]=="x" and board[move-1]=="x":
                return True
        if move==4 :
            if board[move]=="x" and board[move+3]=="x" and board[move-3]=="x":
                return True
            
        if move==4: 
            if board[move]=="x" and board[move+2]=="x" and board[move-2]=="x":
                return True
        if move==4: 
            if board[move]=="x" and board[move+4]=="x" and board[move-4]=="x":
                return True
        else:
            return False



def gameDraw():
     if(board[0]!=" " and board[1]!=" " and board[2]!=" " and board[3]!=" " and board[4]!=" " and board[5]!=" " and board[6]!=" " and board[7]!=" " and board[8]!=" " ):
         return True
     else:
         return False

      
def playerMoves():
    move=int(input("Player,please enter the position :"))
    if board[move]==" ":
        board[move]=player_letter
        makeBoard(board)
        if gameWonByPlayer():
            print("player wins")
            sys.exit()
        if gameDraw():
            print("Game draw!")
            sys.exit()
    else:
     print("Can't insert there, its already filled!")
     playerMoves()
     return



def botMoves():
    bscore=-100
    bmove=0
    for i in range (len(board)):
        if(board[i]==" "):
            board[i]="x"
            score=minimax(board,0,False)
            board[i]=" "
            if(score > bscore):
                bscore=score
                bmove=i
    if board[bmove]==" ":
        board[bmove]="x"
        makeBoard(board)
        if(gameDraw()):
            print("Game Draw!")
            sys.exit()
        if gameWonByBot():
            print("Bot Wins")
    else:
     print("Can't insert there, its already filled!")
     botMoves()
     return
                    
      
def minimax(board, depth, maximize):
   
    if gameWonByPlayer():
        return -100
    
    elif gameWonByBot():
        return 100
    
    elif gameDraw():
        return 0
    
    if maximize:
     bscore=-100
     
     for i in range (len(board)):
        if(board[i]==" "):
            board[i]="x"
            score=minimax(board,0,False)
            board[i]=" "
            if(score > bscore):
                bscore=score
               
    
     return bscore
    else:
        bscore=1000
        for i in range (len(board)):
         if(board[i]==" "):
            board[i]=player_letter
            score=minimax(board,0,True)
            board[i]=" "
            if(score < bscore):
                bscore=score
        return bscore


def botFirstRandomMove():
 num1 = random.randint(0, 8)
 
 if(board[num1]==" "):
   board[num1]="x"
   makeBoard(board)
   return          


for i in range(0,1): 
      botFirstRandomMove()      
                

while True:
    
    playerMoves()
    
    print("----------")
    
    if gameWonByPlayer() or gameWonByBot():
        break
   
    botMoves()
    
    if gameWonByPlayer() or gameWonByBot():
        break
    

    
