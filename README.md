# Blackjack-in-Python
"A fun and interactive digital Blackjack game developed during my exchange program. Compete against the dealer, implement strategies, and experience the thrill of 21 in this terminal-based game! Perfect for beginners and card game enthusiasts."

#Libaries we need for the code to run
import math
import turtle
import random

#The dictionaries
cardsdictionary = {2 : 2, 3 : 3, 4 : 4, 5 : 5, 6 : 6, 7 : 7, 8 : 8, 9 : 9, 10 : 10, "Jack" : 10, "Queen": 10 , "King" : 10, "Ace": 11}
icondictionary = {"Clubs" : "Black", "Diamonds" : "Red", "Hearts" : "Red", "Spades" : "Black"}

#Variables and lists needed to run the program
dealbust = ""
playbust = ""
blackjack = ""
dragon = ""
card3ace = ""
playerscardlist = []
dealerscardlist = []
xcounter = 60
dealerx = 60

#To draw the blackjacktable
def blackjacktable():
    turtle.tracer( 100000 )
    turtle.speed("fastest")
    turtle.hideturtle()
    turtle.Screen().bgcolor("#75B74E")
    turtle.goto(50,210)
    turtle.color("Black")
    turtle.write(str("Dealer"), align="center", font=("Arial", 20, "normal"))
    turtle.pendown()
    turtle.color("#75B74E")
    turtle.home()
    turtle.penup()
    turtle.goto(50,-50)
    turtle.color("Black")
    turtle.write(str("Player"), align="center", font=("Arial", 20, "normal"))
    turtle.pendown()
    turtle.color("#75B74E")
    turtle.home()
    turtle.penup()
    turtle.update()
          
#Function to draw a card
def card(x):
    turtle.pendown()
    turtle.forward(40)
    turtle.left(90)
    turtle.forward(80)
    turtle.left(90)
    turtle.forward(40)
    turtle.write(str(x), align="center", font=("Arial", 12, "normal"))
    turtle.left(90)
    turtle.forward(80)
    turtle.left(90)
    turtle.penup()
    turtle.update()

#(This card needs to be hidden at the beginning)    
def carddealer2():
    turtle.pendown()
    turtle.forward(40)
    turtle.left(90)
    turtle.forward(80)
    turtle.left(90)
    turtle.forward(40)
    turtle.left(90)
    turtle.forward(80)
    turtle.left(90)
    turtle.penup()
    turtle.update()

def card1():
    global iconplayer1
    global playercard
    turtle.home()
    turtle.color(iconplayer1[1])
    turtle.begin_fill()
    card(playercard1[0])
    turtle.end_fill()

def card2():
    global iconplayer2
    global playercard2
    turtle.goto(60,0)
    turtle.begin_fill()
    turtle.color(iconplayer2[1])
    card(playercard2[0])
    turtle.end_fill()
    
def card3():
    global icondealer1
    global dealercard1
    turtle.goto(0,100)
    turtle.color(icondealer1[1])
    turtle.begin_fill()
    card(dealercard1[0])
    turtle.end_fill()
                
def card4():
    global icondealer2
    turtle.goto(60,100)
    turtle.color(icondealer2[1])
    turtle.begin_fill()
    carddealer2()
    turtle.end_fill()
    turtle.update()
    
#To draw all the cards at once   
def basegame():
    global iconplayer1
    global iconplayer2
    global icondealer1
    global icondealer2
    card1()
    card2()
    card3()
    card4()

#To reveal the secondcard of the dealer
def dealerreveal():
    global icondealer1
    global icondealer2
    global dealercard1
    global dealercard2
    
    turtle.goto(0,100)
    turtle.color(icondealer1[1])
    turtle.begin_fill()
    card(dealercard1[0])
    turtle.end_fill()
    turtle.goto(60,100)
    turtle.color(icondealer2[1])
    turtle.begin_fill()
    card(dealercard2[0])
    turtle.end_fill()
    turtle.update()

#Dealing the cards to player
def cardsplayer():
    global playercards
    global playercard1
    global playercard2
    global blackjack
    global iconplayer1
    global iconplayer2
    playercard1 = random.choice(list(cardsdictionary.items()))
    iconplayer1 = random.choice(list(icondictionary.items()))
    playercard2 = random.choice(list(cardsdictionary.items()))
    iconplayer2 = random.choice(list(icondictionary.items()))
    if playercard1[1] == cardsdictionary["Ace"] and playercard2[1] == cardsdictionary["Ace"]:
        playercard1 = playercard1
        playercard2 = ["Ace",1]

    cardcombo1 = str(playercard1[0]) + " " + iconplayer1[0]
    playerscardlist.append(cardcombo1)
    cardcombo2 = str(playercard2[0]) + " " + iconplayer2[0]
    playerscardlist.append(cardcombo2)
    playercards = playercard1[1] + playercard2[1]
    print("Your cards are: ",playerscardlist, " a total of ", playercards)
    if playercards == 21 and len(playerscardlist) == 2:
        blackjack = "blackjack"

#Dealing the cards to dealer    
def cardsdealer():
    global dealercards
    global dealercard1
    global dealercard2
    global icondealer1
    global icondealer2
    dealercard1 = random.choice(list(cardsdictionary.items()))
    icondealer1 = random.choice(list(icondictionary.items()))
    dealercard2 = random.choice(list(cardsdictionary.items()))
    icondealer2 = random.choice(list(icondictionary.items()))
    if dealercard1[1] == cardsdictionary["Ace"] and dealercard2[1] == cardsdictionary["Ace"]:
        dealercard1 = dealercard1
        dealercard2 = [1,1]

    dealercombo1 = str(dealercard1[0]) + " " + icondealer1[0]
    dealerscardlist.append(dealercombo1)
    dealercombo2 = str(dealercard2[0]) + " " + icondealer2[0]
    dealerscardlist.append(dealercombo2)
    dealercards = dealercard1[1] + dealercard2[1]
    print("The dealers card is: ", dealercombo1)

#If player wants extracard with checks    
def extracard():
    global playercards
    global playbust
    global dealbust
    global blackjack
    global xcounter
    global dragon
    global balance
    global playercard1
    global playercard2
    global card3ace
    cardinput = input("Do you want to add another card, yes/no? ")
    while cardinput != "no":
        if cardinput == "yes":
            turtle.home()
            xcounter = xcounter + 60
            turtle.goto(xcounter,0)
            playercard3 = random.choice(list(cardsdictionary.items()))
            playercards = playercards + playercard3[1]
            if playercards >21 and playercard1[0] == "Ace":
                playercards = playercards - playercard1[1]
                playercard1 = [1,1]
                playercards = playercards + playercard1[1]
            if playercards >21 and playercard2[0] == "Ace":
                playercards = playercards - playercard2[1]
                playercard2 = [1,1]
                playercards = playercards + playercard2[1]
            if playercard3[0] == "Ace":
                card3ace = "Ace"
            if playercards >21 and card3ace == "Ace":
                playercards = playercards - 11 + 1
                card3ace =""
            if playercards >21 and playercard3[0] == "Ace":
                playercards = playercards - playercard3[1]
                playercard3 = ["Ace",1]
                playercards = playercards + playercard3[1]                
            iconplayer3 = random.choice(list(icondictionary.items()))
            cardcombo3 = str(playercard3[0]) + " " + iconplayer3[0]
            playerscardlist.append(cardcombo3)
            
            turtle.color(iconplayer3[1])
            turtle.begin_fill()
            card(playercard3[0])
            turtle.end_fill()
            turtle.update()
            if playercards > 21:
                print("You busted, Your cards were: ",playerscardlist, " and a total of ",playercards)
                print("Your new balance is: ", balance)
                playbust = "busted"
                break
            elif len(playerscardlist) == 5 and playercards <=21:
                winnings = (moneyinput * 2)- moneyinput
                totalwinnings = winnings + moneyinput
                balance = balance + totalwinnings
                print("Dragon! Congrats you won: ", winnings)
                print("Your cards were: ", playerscardlist, " and a total of: ", playercards)
                print("The dealers cards were: ", dealerscardlist, " and a total of: ", dealercards)
                print("Your new balance is: ", balance)
                dragon = "dragon"
                break
            else:
                print("Your cards are: ",playerscardlist, " and a total of ",playercards)
        else:
            print("Error, I did not understand your input")
        cardinput = input("Do you want to add another card, yes/no? ")

#Dealer extra cards with checks      
def dealercardextra():
    global balance
    global moneyinput
    global dealercards
    global playbust
    global dealbust
    global dealerx
    global dealercard1
    global dealercard2
    while dealercards <= 16 and playbust != "busted" and blackjack != "blackjack" and dragon != "dragon":
        turtle.home()
        dealerx = dealerx + 60
        turtle.goto(dealerx,100)
        dealercard3 = random.choice(list(cardsdictionary.items()))
        icondealer3 = random.choice(list(icondictionary.items()))
        dealercards = dealercards + dealercard3[1]
        if dealercards >21 and dealercard1[0] == "Ace":
            dealercards = dealercards - dealercard1[1]
            dealercard1 = [1,1]
            dealercards = dealercards + dealercard1[1]
        if dealercards >21 and dealercard2[0] == "Ace":
            dealercards = dealercards - dealercard2[1]
            dealercard2 = [1,1]
            dealercards = dealercards + dealercard2[1]
        if dealercard3[0] == "Ace" and dealercards >21:
            dealercards = dealercards - dealercard3[1]
            dealercard3 = [1,1]
            dealercards = dealercards + dealercard3[1]            
        dealercombo3 = str(dealercard3[0]) + " " + icondealer3[0]
        dealerscardlist.append(dealercombo3)
        turtle.color(icondealer3[1])
        turtle.begin_fill()
        card(dealercard3[0])
        turtle.end_fill()
        turtle.update()
            
        if dealercards >21:
            dealbust = "busted"
            winnings = (moneyinput * 2)- moneyinput
            totalwinnings = winnings + moneyinput
            balance = balance + totalwinnings
            print("The dealer is busted!", " You won: ", winnings)
            print("Your cards were: ", playerscardlist, " and a total of: ", playercards)
            print("The dealers cards were: ", dealerscardlist, " and a total of: ", dealercards)
            print("Your new balance is: ", balance)

#Checks to see who is the winner             
def winnercheck():
    global playercards
    global dealercards
    global playbust
    global dealbust
    global balance
    global moneyinput
    global blackjack
    global dragon
    if playercards == 21 and dealercards != 21 and len(playerscardlist) == 2 and dragon != "dragon":
            winnings = (moneyinput * 2.5) - moneyinput
            totalwinnings = winnings + moneyinput
            balance = balance + totalwinnings
            print("Blackjack, well done!", "You won: ", winnings)
            print("Your cards were: ", playerscardlist, " and a total of: ", playercards)
            print("The dealers cards were: ", dealerscardlist, " and a total of: ", dealercards)
            print("Your new balance is: ", balance)
            blackjack = ""
            
    elif playercards > dealercards and playercards <22 and dealercards != 21 and dragon != "dragon":
        winnings = (moneyinput * 2)- moneyinput
        totalwinnings = winnings + moneyinput
        balance = balance + totalwinnings
        print("Congrats you won: ", winnings)
        print("Your cards were: ", playerscardlist, " and a total of: ", playercards)
        print("The dealers cards were: ", dealerscardlist, " and a total of: ", dealercards)
        print("Your new balance is: ", balance)

    elif playercards == 21 and dealercards == 21 and dragon != "dragon":
        if len(playerscardlist) < len(dealerscardlist):
            winnings = (moneyinput * 2)- moneyinput
            totalwinnings = winnings + moneyinput
            balance = balance + winnings
            print("Congrats you won: ", winnings)
            print("Your cards were: ", playerscardlist, " and a total amount of cards: ", len(playerscardlist))
            print("The dealers cards were: ", dealerscardlist, " and a total amount of cards: ", len(dealerscardlist))
            print("Your new balance is: ", balance)
        elif len(dealerscardlist) < len(playerscardlist):
            print("You lost!")
            print("Your cards were: ", playerscardlist, " and a total amount of cards: ", len(playerscardlist))
            print("The dealers cards were: ", dealerscardlist, " and a total amount of cards: ", len(dealerscardlist))
            print("Your new balance is: ", balance)
            blackjack = ""
        else:
            balance = balance + moneyinput
            print("It is a draw, no winners!")
            print("Your cards were: ", playerscardlist, " and a total amount of cards: ", len(playerscardlist))
            print("The dealers cards were: ", dealerscardlist, " and a total amount of cards: ", len(dealerscardlist))
            print("Your new balance is: ", balance)
            blackjack = ""

    elif playercards == dealercards and playercards !=21 and dragon != "dragon":
        balance = balance + moneyinput
        print("It is a draw, no winners!")
        print("Your cards were: ", playerscardlist, " and a total of: ", playercards)
        print("The dealers cards were: ", dealerscardlist, " and a total of: ", dealercards)
        print("Your new balance is: ", balance)

    elif dealercards > playercards and dealbust != "busted" and dragon != "dragon":
        print("You lost!")
        print("Your cards were: ", playerscardlist, " and a total of: ", playercards)
        print("The dealers cards were: ", dealerscardlist, " and a total of: ", dealercards)
        print("Your new balance is: ", balance)

    elif playbust == "busted":
        playbust = ""
    elif dealbust == "busted":
        dealbust = ""
    elif dragon == "dragon":
        dragon = ""

#Resetting all the variables and lists for new game
def listreset():
    global playerscardlist
    global dealerscardlist
    global card3ace
    playerscardlist = []
    dealerscardlist = []
    card3ace = ""

#Code for the game    
def game():
    global xcounter
    global dealerx
    global playerscardlist
    global dealerscardlist
    blackjacktable()
    cardsplayer()
    cardsdealer()
    basegame()
    extracard()
    xcounter = 60
    dealerreveal()
    dealercardextra()
    dealerx = 60
    winnercheck()   
    listreset()

#Code for blackjack option menu
def finalgame():
    global balance
    global moneyinput
    if balance <= 0:
        print("You don't have enough balance to play with, please update your account")   
    elif balance > 0:
        moneyinput = int(input("With how much do you want to play this round with: "))
        if moneyinput > balance:
            print("You don't have enough credit to play with this amount, please update your account or play with a lower amount")
        elif moneyinput == 0:
            print("You have to play with an input which is at least 1")
        else:
            balance = balance - moneyinput
            turtle.clear()
            game()

#Code for updating balance menu        
def totalbalance():
    global balance
    global moneyinput
    global firstinput
    print("Your current balance: ", balance)
    updateinput = input("Do you want to update your balance, yes or no? ")
    while updateinput != "no":
        if updateinput == "yes":
            moneyinput = int(input("With how much credit do you want update your account? "))
            balance = balance + moneyinput
            firstinput = firstinput + moneyinput
            print("Your new total balance is: ", balance)
            updateinput = "no"
        else:
            print("Error, i did not understand your input")
            updateinput = input("Do you want to update your balance, yes or no? ")

#Printstatement after the game is done
def finalprint():
    global balance
    global firstinput
    if firstinput < balance:
        print("Congrats you made a profit!")
        print("You made ", (balance - firstinput), " and a total final balance of: ", balance)
    elif firstinput > balance:
        print("You made a lost!")
        print("You lost in total ", ((balance - firstinput)*-1), " and finished with a final balance of: ", balance)
    else:
        print("You made no profit!")
        print("Your final balance is: ", balance)
    
#Finalcode with everything combined
def blackjackgame():
    global moneyinput
    global balance
    global firstinput
    print("Welcome to a game of blackjack!")        
    moneyinput = int(input("With how much credit do you want to update your total account with? "))
    user_input = input("Do you want to (p)lay a game of blackjack, (u)pdate your balance or (q)uit? ")
    balance = moneyinput
    firstinput = moneyinput
    while user_input != "q":
        if user_input == "p":
            finalgame()    
        elif user_input == "u":
            totalbalance()   
        else:
            print("Error, i did not understand your input")
        user_input = input("Do you want to (p)lay a game of blackjack, (u)pdate your balance or (q)uit? ")
    finalprint()    
    turtle.exitonclick()

blackjackgame()
