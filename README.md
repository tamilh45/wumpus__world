<h1>ExpNo 9: Solve Wumpus World Problem using Python demonstrating Inferences from Propositional Logic</h1> 
<h3>Name:  Tamil Pavalan M</h3>
<h3>Register no:212223110058</h3>
<h3>Date: 24/08/2026</h3>
<H3>Aim:</H3>
<p>
    To solve  Wumpus World Problem using Python demonstrating Inferences from Propositional Logic
</p>
<h1>Problem Description</h1>
<hr>
<h2>Wumpus World</h2>
<hr>
The Wumpus world is a simple world example to illustrate the worth of a knowledge-based agent and to represent knowledge representation.

The figure below shows a Wumpus world containing one pit and one Wumpus. There is an agent in room [1,1]. The goal of the agent is to exit the Wumpus world alive. The agent can exit the Wumpus world by reaching room [4,4]. The wumpus world contains exactly one Wumpus and one pit. There will be a breeze in the rooms adjacent to the pit, and there will be a stench in the rooms adjacent to Wumpus.

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/cd6b68dc-c79f-4dcb-8126-04da90d65912)

<center>Wumpus World Representation</center>
<p>
This is a python program that uses propositional logic sentences to check which rooms are safe. 

It is assumed that there will always be a safe path that the agent can take to exit the Wumpus world. The logical agent can take four actions: Up, Down, Left and Right. These actions help the agent move from one room to an adjacent room. The agent can perceive two things: Breeze and Stench.
</p>

<hr>
<h1>Sample Input and Output:</h1>
<hr>

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/8696111a-a4a7-47cb-ba4b-43a4ef88573f)
![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/4be5bf06-79fa-4fa0-9334-38a33f06060b)
<h1> Program: </h1>

```
# Wumpus World

wumpus = [
    ["Save", "Breeze", "PIT", "Breeze"],
    ["Smell", "Save", "Breeze", "Save"],
    ["WUMPUS", "GOLD", "PIT", "Breeze"],
    ["Smell", "Save", "Breeze", "PIT"]
]

# Initial Variables
# row and column store the player's current position
# starting at the top-left corner.
# arrow = True means the player has an arrow available
# player = True controls the game loop
# score = 0 starts the player's score at zero

row = 0
column = 0
arrow = True
player = True
score = 0

while player:

    choice = input(
        "press u to move up\n"
        "press d to move down\n"
        "press l to move left\n"
        "press r to move right\n"
    )

    # Move Up
    if choice == "u":
        if row != 0:
            row -= 1
        else:
            print("move denied")

        print("current location:", wumpus[row][column], "\n")

    # Move Down
    elif choice == "d":
        if row != 3:
            row += 1
        else:
            print("move denied")

        print("current location:", wumpus[row][column], "\n")

    # Move Left
    elif choice == "l":
        if column != 0:
            column -= 1
        else:
            print("move denied")

        print("current location:", wumpus[row][column], "\n")

    # Move Right
    elif choice == "r":
        if column != 3:
            column += 1
        else:
            print("move denied")

        print("current location:", wumpus[row][column], "\n")

    else:
        print("move denied")

    # If the player encounters Smell
    if wumpus[row][column] == "Smell" and arrow != False:

        arrow_choice = input(
            "do you want to throw an arrow-->\n"
            "press y to throw\n"
            "press n to save your arrow\n"
        )

        if arrow_choice == "y":

            arrow_throw = input(
                "press u to throw up\n"
                "press d to throw down\n"
                "press l to throw left\n"
                "press r to throw right\n"
            )

            # Throw Arrow Up
            if arrow_throw == "u":

                if wumpus[row - 1][column] == "WUMPUS":
                    print("wumpus killed!")
                    score += 1000
                    print("score:", score)

                    wumpus[row - 1][column] = "Save"
                    wumpus[1][0] = "Save"
                    wumpus[3][0] = "Save"

                else:
                    print("arrow wasted...")
                    score -= 10
                    print("score:", score)

            # Throw Arrow Down
            elif arrow_throw == "d":

                if wumpus[row + 1][column] == "WUMPUS":
                    print("wumpus killed!")
                    score += 1000
                    print("score:", score)

                    wumpus[row + 1][column] = "Save"
                    wumpus[1][0] = "Save"
                    wumpus[3][0] = "Save"

                else:
                    print("arrow wasted...")
                    score -= 10
                    print("score:", score)

            # Throw Arrow Left
            elif arrow_throw == "l":

                if wumpus[row][column - 1] == "WUMPUS":
                    print("wumpus killed!")
                    score += 1000
                    print("score:", score)

                    wumpus[row][column - 1] = "Save"
                    wumpus[1][0] = "Save"
                    wumpus[3][0] = "Save"

                else:
                    print("arrow wasted...")
                    score -= 10
                    print("score:", score)

            # Throw Arrow Right
            elif arrow_throw == "r":

                if wumpus[row][column + 1] == "WUMPUS":
                    print("wumpus killed!")
                    score += 1000
                    print("score:", score)

                    wumpus[row][column + 1] = "Save"
                    wumpus[1][0] = "Save"
                    wumpus[3][0] = "Save"

                else:
                    print("arrow wasted...")
                    score -= 10
                    print("score:", score)

            arrow = False

    # If player enters Wumpus room
    if wumpus[row][column] == "WUMPUS":

        score -= 1000

        print(
            "\nWumpus here!!\n"
            "You Die\n"
            "And your score is:",
            score,
            "\n"
        )

        break

    # If player finds Gold
    if wumpus[row][column] == "GOLD":

        score += 1000

        print("You found the GOLD!")
        print("You Win!")
        print("And your score is:", score, "\n")

        break

    # If player falls into a Pit
    if wumpus[row][column] == "PIT":

        score -= 1000

        print(
            "Ahhhhh!!!!\n"
            "You fell in pit.\n"
            "And your score is:",
            score,
            "\n"
        )

        break
```

<h1> Output: </h1>
<img width="627" height="822" alt="image" src="https://github.com/user-attachments/assets/c97f5aed-0492-4527-8227-3be3858c9e9c" />

<h1> Result: </h1>
Wumpus World Problem using Python demonstrating Inferences from Propositional Logic is created successfully


