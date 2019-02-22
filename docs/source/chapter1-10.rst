chapter 10: Minecraft Magic with for Loops
===============================================



10.1 A Simple for Loop
------------------------
리스트에서 아이템을 꺼내 오는 예제를 보자

.. code-block:: python


    noodleSoup = ["water", "soy sauce", "spring onions", "pepper", "noodles",
    "beef", "vegetables"]


    for ingredient in noodleSoup:
    print(ingredient)



Mission #55: Magic Wand
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

9장에서 pollBlockHits() 함수를 이용했다.
이 함수를 이용해서 다음 코드를 실행해 보자.
실행한 모든 블럭이 다른 블럭으로 변하게 된다.



.. code-block:: python


    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    import time

    time.sleep(60)

    hits = mc.events.pollBlockHits()
    block = 103

    for hit in hits:
        x, y, z = hit.pos.x, hit.pos.y, hit.pos.z
        mc.setBlock(x, y, z, block)



Mission #56: Magic Stairs
~~~~~~~~~~~~~~~~~~~~~~~~~~

다음 미션을 수행해 보자.

.. code-block:: python


    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    pos = mc.player.getTilePos()
    x, y, z = pos.x, pos.y, pos.z

    stairBlock = 53

    for step in range(10):
        mc.setBlock(x + step, y + step, z, stairBlock)


Playing Around with range()
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

다음을 입력해 보자.

.. code-block:: python


    >>> aRange = range(5)
    >>> list(aRange)
    [0, 1, 2, 3, 4]

    >>> aRange = range(2, 5)
    >>> list(aRange)
    [2, 3, 4]

    >>> aRange = range(3, 10, 2)
    >>> list(aRange)
    [3, 5, 7, 9]

    >>> newRange = range(100, 0, -2)
    >>> list(newRange)
    [100, 98, 96, 94, 92, 90, 88, 86, 84, 82, 80, 78, 76, 74, 72, 70, 68, 66, 64,
    62, 60, 58, 56, 54, 52, 50, 48, 46, 44, 42, 40, 38, 36, 34, 32, 30, 28, 26,
    24, 22, 20, 18, 16, 14, 12, 10, 8, 6, 4, 2]


10.2 Other List Functions
---------------------------

이번에는 reversed() 라는 함수를 익혀 보자.

.. code-block:: python

    >>> backwardsList = reversed(aRange)
    >>> list(backwardsList)
    [9, 7, 5, 3]


    countDown = range(1, 101)
    countDown = reversed(countDown)
    for item in countDown:
    print(item)


Mission #57: Pillars
~~~~~~~~~~~~~~~~~~~~~~~~~
다음 미션을 수행해 보자.

.. code-block:: python


    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()


    def setPillar(x, y, z, height):
        """Creates a pillar. Args set position and height of pillar"""
        stairBlock = 156
        block = 155

        # Pillar top
        mc.setBlocks(x - 1, y + height, z - 1, x + 1, y + height, z + 1, block, 1)
        mc.setBlock(x - 1, y + height - 1, z, stairBlock, 12)
        mc.setBlock(x + 1, y + height - 1, z, stairBlock, 13)
        mc.setBlock(x, y + height - 1, z + 1, stairBlock, 15)
        mc.setBlock(x, y + height - 1, z - 1, stairBlock, 14)

        # Pillar base
        mc.setBlocks(x - 1, y, z - 1, x + 1, y, z + 1, block, 1)
        mc.setBlock(x - 1, y + 1, z, stairBlock, 0)
        mc.setBlock(x + 1, y + 1, z, stairBlock, 1)
        mc.setBlock(x, y + 1, z + 1, stairBlock, 3)
        mc.setBlock(x, y + 1, z - 1, stairBlock, 2)

        # Pillar column
        mc.setBlocks(x, y, z, x, y + height, z, block, 2)

    pos = mc.player.getTilePos()
    x, y, z = pos.x + 2, pos.y, pos.z

    for xOffset in range(0, 100, 5):
        setPillar(x + xOffset, y, z, 10)

기둥 7개를 그리는 코드이다.

Mission #58: Pyramid
~~~~~~~~~~~~~~~~~~~~~~

다음 코드를 실행해 보자.

.. code-block:: python

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()


    block = 24  # sandstone
    height = 10
    levels = reversed(range(height))

    pos = mc.player.getTilePos()
    x, y, z = pos.x + height, pos.y, pos.z

    for level in levels:
        mc.setBlocks(x - level, y, z - level, x + level, y, z + level, block)
        y += 1





10.3 Looping Over a Dictionary
---------------------------------

Dictionary에 사용되는 loop를 살펴보자.


.. code-block:: python

    inventory = {'gems': 5, 'potions': 2, 'boxes': 1}
    for key in inventory:
    print(key)


    gems
    potions
    boxes


    inventory = {'gems': 5, 'potions': 2, 'boxes': 1}
    for key in inventory:
    print(key + " " + str(inventory[key]))

    gems 5
    potions 2
    boxes 1

Mission #59: Scoreboard
~~~~~~~~~~~~~~~~~~~~~~~~~~~
다음 코드를 실행해 보자.

.. code-block:: python

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    import time

    scores = {}

    message = ""

    while message != "exit":
        print("Click in the Minecraft window")
        time.sleep(10)
        mc.events.clearAll()

        mc.postToChat("Go")

        time.sleep(60)

        hits = mc.events.pollBlockHits()
        numberOfHits = len(hits)
        mc.postToChat("You used your sword " + hits + " times.")

        playerName = input("Enter your name: ")
        scores[playerName] = numberOfHits

        for name in scores:
            print(name + str(scores[name]))

        message = input("Press enter in this window to start ('exit' to quit)")




10.4 for-else Loops.
-----------------------
for else 구문도 가능하다.

.. code-block:: python

    sandwich = ["Bread", "Butter", "Tuna", "Lettuce", "Mayonnaise", "Bread"]
    for ingredient in sandwich:
        print(ingredient)
    else:
        print("This is the end of the sandwich.")

    Bread
    Butter
    Tuna
    Lettuce
    Mayonnaise
    Bread
    This is the end of the sandwich.


Breaking a for-else Loop
~~~~~~~~~~~~~~~~~~~~~~~~~
다음처럼 break문을 써서 빠져 나올 수 있다.



.. code-block:: python


    sandwich = ["Bread", "Butter", "Tuna", "Lettuce", "Mayonnaise", "Bread"]
    for ingredient in sandwich:
        if ingredient == "Mayonnaise":
            print("I don't like mayonnaise on my sandwich.")
            break
        else:
            print(ingredient)
    else:
        print("This is the end of the sandwich.")

Mission #60: The Diamond Prospector
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
다음 미션을 수행해 보자.

.. code-block:: python

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    pos = mc.player.getTilePos()
    x, y, z = pos.x, pos.y, pos.z

    depth = 50

    for deep in range(depth):
        block = mc.getBlock(x, y - deep, z)
        if block == 56:
            mc.postToChat("A diamond ore is " + str(deep) + " blocks below you.")
            break
    else:
        mc.postToChat("There are no diamond ore blocks below you")



10.5 Nested for Loops and Multidimensional Lists
----------------------------------------------------

다음 코드를 실행해 보자.


.. code-block:: python

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()
    twoDimensionalRainbowList = [[0, 0, 0],
                                 [1, 1, 1],
                                 [2, 2, 2],
                                 [3, 3, 3],
                                 [4, 4, 4],
                                 [5, 5, 5]]
    pos = mc.player.getTilePos()
    x = pos.x
    y = pos.y
    z = pos.z
    startingX = x

    mc.player.setTilePos(x+3, y, z+3)

    for row in twoDimensionalRainbowList:
        for color in row:
            mc.setBlock(x, y, z, 35, color)
            x += 1
        y += 1
        x = startingX


Accessing Values in 2D Lists
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1차원 리스트는 다음처럼 하면 된다.

.. code-block:: python

    scores = [1, 5, 6, 1]
    scores[2] = 7

2차원 이상은 다음처럼 하면 된다.

.. code-block:: python

    twoDimensionalRainbowList = [[0, 0, 0],
                                 [1, 1, 1},
                                 [2, 2, 2],
                                 [3, 3, 3],
                                 [4, 4, 4],
                                 [5, 5, 5]]


    twoDimensionalRainbowList[0][1] = 7


Mission #61: Pixel Art
~~~~~~~~~~~~~~~~~~~~~~~~

다음 코드를 실행해 보자.

.. code-block:: python

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    pos = mc.player.getTilePos()
    x, y, z = pos.x, pos.y, pos.z

    mc.player.setTilePos(x+3, y, z+3)

    blocks = [[35, 35, 22, 22, 22, 22, 35, 35],
              [35, 22, 35, 35, 35, 35, 22, 35],
              [22, 35, 22, 35, 35, 22, 35, 22],
              [22, 35, 35, 35, 35, 35, 35, 22],
              [22, 35, 22, 35, 35, 22, 35, 22],
              [22, 35, 35, 22, 22, 35, 35, 22],
              [35, 22, 35, 35, 35, 35, 22, 35],
              [35, 35, 22, 22, 22, 22, 35, 35]]

    for row in reversed(blocks):
        for block in row:
            mc.setBlock(x, y, z, block)
            x += 1
        y += 1
        x = pos.x


Generating 2D Lists with Loops
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

다음을 실행해 보자.

.. code-block:: python

    import random
        randomNumbers = []
    for outer in range(10):
        randomNumbers.append([])
    for inner in range(10):
        number = random.randint(1, 4)
    randomNumbers[outer].append(number)
    print(randomNumbers)


    [[3, 1, 4, 1, 4, 1, 2, 3, 2, 2],
    [1, 3, 4, 2, 4, 3, 4, 1, 3, 2],
    [4, 2, 4, 1, 4, 3, 2, 3, 4, 4],
    [1, 4, 3, 4, 3, 4, 3, 3, 4, 4],
    [3, 1, 4, 2, 3, 3, 3, 1, 4, 2],
    [4, 1, 4, 2, 3, 2, 4, 3, 3, 1],
    [2, 4, 2, 1, 2, 1, 4, 2, 4, 3],
    [3, 1, 3, 4, 1, 4, 2, 2, 4, 1],
    [4, 3, 1, 2, 4, 2, 2, 3, 1, 2],
    [3, 1, 3, 3, 1, 3, 1, 4, 1, 2]]


Mission #62: A Weather-Worn Wall
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

다음 코드를 실행해 보자.

.. code-block:: python

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    import random


    def brokenBlock():
        brokenBlocks = [48, 67, 4, 4, 4, 4]
        block = random.choice(brokenBlocks)
        return block

    pos = mc.player.getTilePos()
    x, y, z = pos.x, pos.y, pos.z
    mc.player.setTilePos(x+3, y, z+3)
    brokenWall = []
    height, width = 5, 10

    # create the list of broken blocks
    for row in range(height):
        brokenWall.append([])
        for column in range(width):
            block = brokenBlock()
            brokenWall[row].append(block)

    # set the blocks
    for row in brokenWall:
        for block in row:
            mc.setBlock(x, y, z, block)
            x += 1
        y += 1
        x = pos.x

Outputting 3D Lists
~~~~~~~~~~~~~~~~~~~~~~~~~

다음 코드를 실행해 보자.

.. code-block:: python


    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()
    pos = mc.player.getTilePos()
    x = pos.x
    y = pos.y
    z = pos.z
    mc.player.setTilePos(x+10, y, z+10)

    cube = [[[57, 57, 57, 57], [57, 0, 0, 57], [57, 0, 0, 57], [57, 57, 57, 57]],
            [[57, 0, 0, 57], [0, 0, 0, 0], [0, 0, 0, 0], [57, 0, 0, 57]],
            [[57, 0, 0, 57], [0, 0, 0, 0], [0, 0, 0, 0], [57, 0, 0, 57]],
            [[57, 57, 57, 57], [57, 0, 0, 57], [57, 0, 0, 57], [57, 57, 57, 57]]]
    startingX = x
    startingY = y

    for depth in cube:
        for height in reversed(depth):
            for block in height:
                mc.setBlock(x, y, z, block)
                x += 1
            y += 1
            x = startingX
        z += 1
        y = startingY


Accessing Values in 3D Lists
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: python

    cube = [[[57, 57, 57, 57],
    [57, 0, 0, 57],
    [57, 0, 0, 57],
    [57, 57, 57, 57]],
    #
    [[57, 0, 0, 57],
    [0, 0, 0, 0],
    [0, 0, 0, 0],
    [57, 0, 0, 57]],
    #
    [[57, 0, 0, 57],
    [0, 0, 0, 0],
    [0, 0, 0, 0],
    [57, 0, 0, 57]],
    #
    [[57, 57, 57, 57],
    [57, 0, 0, 57],
    [57, 0, 0, 57],
    [57, 57, 57, 57]]]

cube[0] 이면

.. code-block:: python

    [[57, 57, 57, 57],
    [57, 0, 0, 57],
    [57, 0, 0, 57],
    [57, 57, 57, 57]]

cube[0][3]

.. code-block:: python

    [57, 57, 57, 57]


cube[0][3][3] = 41  처럼 변경할 수 있다.


Mission #63: Duplicate a Building
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

다음 코드를 실행해 보자.

.. code-block:: python


    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()


    def sortPair(val1, val2):
        if val1 > val2:
            return val2, val1
        else:
            return val1, val2


    def copyStructure(x1, y1, z1, x2, y2, z2):
        x1, x2 = sortPair(x1, x2)
        y1, y2 = sortPair(y1, y2)
        z1, z2 = sortPair(z1, z2)

        width = x2 - x1
        height = y2 - y1
        length = z2 - z1

        structure = []

        print("Please wait...")

        # Copy the structure
        for row in range(height):
            structure.append([])
            for column in range(width):
                structure[row].append([])
                for depth in range(length):
                    block = mc.getBlock(x1 + column, y1 + row, z1 + depth)
                    structure[row][column].append(block)

        return structure


    def buildStructure(x, y, z, structure):
        xStart = x
        yStart = y
        for row in structure:
            for column in row:
                for block in column:
                    mc.setBlock(x, y, z, block)
                    z += 1
                x += 1
                z = yStart
            y += 1
            x = xStart


    # get the position of the first corner
    input("Move to the first corner and press enter in this window")
    pos = mc.player.getTilePos()
    x1, y1, z1 = pos.x, pos.y, pos.z

    # get the position of the second corner
    input("Move to the opposite corner and press enter in this window")
    pos = mc.player.getTilePos()
    x2, y2, z2 = pos.x, pos.y, pos.z

    # copy the building
    structure = copyStructure(x1, y1, z1, x2, y2, z2)

    # get the position for the copy
    input("Move to the position you want to create the structure and press ENTER in this window")
    pos = mc.player.getTilePos()
    x, y, z = pos.x, pos.y, pos.z
    buildStructure(x, y, z, structure)




10.6 What You Learned
-------------------

for loops with lists
range() function
more about for loops
lists, such as reversing lists, looping
over dictionaries, and breaking for loops

two- and threedimensional
lists with nested loops

