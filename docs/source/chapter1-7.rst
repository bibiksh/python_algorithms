chapter 7: Dance Parties and Flower Parades with while Loops
==============================================================

7.1 A Simple while Loop
----------------------------

while 구문은 아래 구조로 되어 있다.

.. code-block:: python


    count = 1
    while count <= 5:
        print(count)
        count += 1
    print("Loop finished")



Mission #33: A Random Teleportation Tour
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

random 함수를 이용하여 임의로 움직이는 코드를 짜보자.


.. code-block:: python


    import time
    import random
    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    count = 0
    while count < 5:
        x = random.randrange(-127, 128)
        y = random.randrange(0, 64)
        z = random.randrange(-127, 128)

        mc.postToChat("x:"+str(x))
        mc.postToChat("Y:"+str(y))
        mc.postToChat("Z:"+str(z))
        mc.player.setTilePos(x, y, z)
        count += 1
        time.sleep(10)





7.2 Controlling Loops with a Count Variable
----------------------------------------------

Mission #34: The Watery Curse
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
다음 미션을 수행해 보자.

.. code-block:: python


    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    import time

    count = 0

    while count < 30:
        pos = mc.player.getPos()
        mc.setBlock(pos.x, pos.y, pos.z, 8)
        count += 1
        time.sleep(1)

Infinite while Loops
~~~~~~~~~~~~~~~~~~~~~~~

무한 반복을 의미 한다.

.. code-block:: python


    while True:
        print("Hello")


    while True:
        print("Hello")
    print("This line is never reached")


Mission #35: Flower Trail
~~~~~~~~~~~~~~~~~~~~~~~~~~~
skip this mission




7.3 Fancy Conditions
------------------------

다음 코드를 보자
초기값은 while 루프가 실행되지만 사용자 입력값에 따라서 빠져나갈 수 있다.


.. code-block:: python

    continueAnswer = "Y"
    coins = 0
    while continueAnswer == "Y":
        coins = coins + 1
        continueAnswer = input("Continue? Y/N")
    print("You have " + str(coins) + " coins")



Mission #36: Diving Contest
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
skip this mission

Boolean Operators and while Loops
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

boolean operator들도 while 문에 쓰인다.

.. code-block:: python


    password = "cats"
    passwordInput = input("Please enter the password: ")
    attempts = 0
    while password != passwordInput and attempts < 3:
        attempts += 1
        passwordInput = input("Incorrect. Please enter the password: ")
    if password == passwordInput:
        print("Password accepted.")


Checking a Range of Values in while Loops
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
while에 변수값 범위를 지정할 수 있다.

.. code-block:: python

    position = 0
    while 0 <= position <= 10:
        position = int(input("Enter your position 0-10: "))
    print(position)


Mission #37: Make a Dance Floor
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

다음 미션을 수행해 보자.

.. code-block:: python

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()
    import time

    pos = mc.player.getTilePos()
    floorX = pos.x - 2
    floorY = pos.y - 1
    floorZ = pos.z - 2
    width = 5
    length = 5
    block = 41
    mc.setBlocks(floorX, floorY, floorZ,
                 floorX + width, floorY, floorZ + length, block)

    while floorX <= pos.x <= floorX + width and floorZ <= pos.z <= floorZ + length:
        if block == 41:
            block = 57
        else:
            block = 41
        mc.setBlocks(floorX, floorY, floorZ,
                     floorX + width, floorY, floorZ + length, block)
        # get the player's position
        pos = mc.player.getTilePos()
        # wait 0.5 seconds
        time.sleep(0.5)

Nested if Statements and while Loops
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

whlile문 안에 if문이 들어가는 경우이다.

.. code-block:: python

    word = "mine"
    count = 0
    while count < 50:
        print(word)
        if word == "mine":
            word = "craft"
        else:
            word = "mine"

Mission #38: The Midas Touch
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

다음 미션을 수행해 보자.
player가 지나간 자리는 모두 황금색으로 변하는 코드이다.


.. code-block:: python

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    air = 0
    water = 9

    while True:
        pos = mc.player.getTilePos()
        blockBelow = mc.getBlock(pos.x, pos.y - 1, pos.z)

        if blockBelow != air and blockBelow != water:
            # change the block below the player to gold
            mc.setBlock(pos.x, pos.y - 1, pos.z, 41)





7.4 Ending a while Loop with break
---------------------------------------

while문을 빠져 나갈때는 break를 쓴다.

.. code-block:: python

    while True:
        userInput = input("Enter a command: ")
        if userInput == "exit":
            break
        print(userInput)
     print("Loop exited")



Mission #39: Create a Persistent Chat with a Loop
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
다음 미션을 수행해 보자.

.. code-block:: python


    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    userName = input("Enter your username: ")

    while True:
        message = input("Enter your message: ")
        if message == "exit":
            break
        mc.postToChat(userName + ": " + message)

Mission #40: Hot and Cold
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: python

    from mcpi.minecraft import Minecraft
    import math
    import time
    import random
    mc = Minecraft.create()

    destX = random.randint(-127, 127)
    destZ = random.randint(-127, 127)
    destY = mc.getHeight(destX, destZ)

    print(destX, destY, destZ)

    block = 57
    mc.setBlock(destX, destY, destZ, block)
    mc.postToChat("Block set")

    while True:
        pos = mc.player.getPos()
        distance = math.sqrt((pos.x - destX) ** 2 + (pos.z - destZ) ** 2)

        if distance == 0:
            break

        if distance > 100:
            mc.postToChat("Freezing")
        elif distance > 50:
            mc.postToChat("Cold")
        elif distance > 25:
            mc.postToChat("Warm")
        elif distance > 12:
            mc.postToChat("Boiling")
        elif distance > 6:
            mc.postToChat("On fire!")
        elif distance == 0:
            mc.postToChat("Found it")




7.4 What You Learned
----------------------

while loops
loops with conditions
