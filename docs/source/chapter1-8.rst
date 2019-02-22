chapter 8: Functions Give You Superpowers
=============================================

Function이란 다음 특징을 가진다.

Reusability
~~~~~~~~~~~~
Functions save time. Because you don’t have to rewrite the
same code over and over again, writing a program is faster and easier.

Debugging
~~~~~~~~~~~~
By containing tasks in groups of code, it is easier to identify
where a problem originates and make changes to fix the problem.


Modularity
~~~~~~~~~~~~~
You can develop different functions to use in the same
program independently of one another. This makes it easier to share
code with other people and reuse functions in other programs.
Scalability Using functions makes it easier to increase the size of a
program and the amount of data it processes.


8.1 Defining Your Own Functions
------------------------------------
함수 정의는 다음처럼 한다.

.. code-block:: python

    def greeting():
    print("Hello")
    print("Nice to meet you")


함수 호출은 정의한대로 호출하면 된다.

greeting()

Functions Take Arguments
~~~~~~~~~~~~~~~~~~~~~~~~~

함수에 전달자가 들어가는 경우가 대부분이다.
아래 예제를 보자.

.. code-block:: python

    def fancyGreeting(personName):
        print("Hello, " + personName)


    fancyGreeting("Mario")
    fancyGreeting("Steve")

fancyGreeting() 호출하게 되면 전달자가 없으므로 오류가 난다.

Mission #41: Build a Forest
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

숲을 만드는 코드를 짜보자.

.. code-block:: python


    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()


    def growTree(x, y, z):
        """Creates a tree at the coordinates given"""
        wood = 17
        leaves = 18

        # trunk
        mc.setBlocks(x, y, z, x, y + 5, z, wood)

        # leaves
        mc.setBlocks(x - 2, y + 6, z - 2, x + 2, y + 6, z + 2, leaves)
        mc.setBlocks(x - 1, y + 7, z - 1, x + 1, y + 7, z + 1, leaves)

    pos = mc.player.getTilePos()
    x = pos.x
    y = pos.y
    z = pos.z


    growTree(x + 1, y, z)
    growTree(x + 10, y, z)
    growTree(x + 20, y, z)

Refactoring a Program
~~~~~~~~~~~~~~~~~~~~~~~~~~~

코드를  재수정 또는 구조를 변경하는 작업들을 refactoring 이라고 한다.

다음 코드를 변경하는 작업을 해보자.

.. code-block:: python

    name1 = input("Hello, what is your name?")
    print("Pleased to meet you, " + name1)
    name2 = input("Hello, what is your name?")
    print("Pleased to meet you, " + name2)
    name3 = input("Hello, what is your name?")
    print("Pleased to meet you, " + name3)

    def helloFriend():
        name = input("Hello, what is your name?")
        print("Pleased to meet you, " + name)

    helloFriend()
    helloFriend()
    helloFriend()


Mission #42: Refactor Away
~~~~~~~~~~~~~~~~~~~~~~~~~~

다음 코드를 refactoring 작업을 해보도록 하자.

.. code-block:: python


    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    import time


    def makeMelon(x, y, z):
        pos = mc.player.getPos()
        x = pos.x
        y = pos.y
        z = pos.z
        mc.setBlock(x, y, z, 103)
        time.sleep(10)

    pos = mc.player.getPos()
    x = pos.x
    y = pos.y
    z = pos.z

    makeMelon(x, y + 1, z)
    makeMelon(x, y + 3, z)
    makeMelon(x + 2, y, z)
    makeMelon(x, y, z)
    makeMelon(x, y + 1, z + 2)
    makeMelon(x, y, z + 3)

Commenting with Docstrings
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
코멘트 처리를 해서 코드에 대한 설명을 붙여서 이해를 돕는 역할을 많이 한다.

.. code-block:: python

    def duplicateString(stringToDbl):
        """ Prints a string twice on the same line.
        stringToDbl argument should be a string """
        print(stringToDbl * 2)

실제 코멘트들은 실행코드에는 안들어 가지만 메모리에는 포함이 되므로 과도한 코멘트는 지향이 필요하다.

Line Breaks in Arguments
~~~~~~~~~~~~~~~~~~~~~~~~~~
라인 문장이 길때 다음줄을 이용하는것이 가독성을 위해서 좋다.

.. code-block:: python

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()
    pos = mc.player.getPos()
    width = 10
    height = 12
    length = 13
    block = 103
    mc.setBlocks(pos.x, pos.y, pos.z,
                 pos.x + width, pos.y + height, pos.z + length, block)

Function Return Values
~~~~~~~~~~~~~~~~~~~~~~~
함수를 이용하는 목적중에 하나가 결과값을 도출하는 데 있다.
아래 코드를 살펴보자.

.. code-block:: python

    def calculateCookiePrice(cost):
        price = cost + 2
        price = price * 10
        return price


Mission #43: Block ID Reminder
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

다음 코드를 실행해 보자.
함수를 호출하면 block id를 리턴하는 코드이다.


.. code-block:: python

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()


    def melon():
        return 103


    def water():
        return 9


    def wool():
        return 35


    def lava():
        return 10


    def tnt():
        return 46


    def flower():
        return 37


    def diamondBlock():
        return 57


    block = melon()
    pos = mc.player.getTilePos()
    mc.setBlock(pos.x, pos.y, pos.z, block)





8.2 Using if Statements and while Loops in Functions
-------------------------------------------------------

fucntion에서 if문과 while loop를 쓰는법을 배워 보도록 하자.



if Statements
~~~~~~~~~~~~~~~

다음처럼 문자로 입력한 부분을 숫자로 처리하는 구문을 보자

.. code-block:: python

    def wordToNumber(numToConvert):
    """ Converts a number written as a word to an integer """
        if numToConvert == "one":
            numAsInt = 1
        elif numToConvert == "two":
            numAsInt = 2
        elif numToConvert == "three":
            numAsInt = 3
        elif numToConvert == "four":
            numAsInt = 4
        elif numToConver == "five":
            numAsInt = 5
        return numAsInt

Mission #44: Wool Color Helper
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

다음 미션을 수행해 보자.

.. code-block:: python


    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()


    def getWoolState(color):
        """Takes a color as a string and returns the wool block state
        for that color"""

        if color == "pink":
            blockState = 6
        elif color == "black":
            blockState = 15
        elif color == "grey":
            blockState = 7
        elif color == "red":
            blockState = 14
        elif color == "green":
            blockState = 5
        elif color == "brown":
            blockState = 0
        elif color == "yellow":
            blockState = 4
        elif color == "blue":
            blockState = 11
        elif color == "light blue":
            blockState = 3
        elif color == "purple":
            blockState = 10
        elif color == "cyan":
            blockState = 9
        elif color == "orange":
            blockState = 1
        elif color == "light grey":
            blockState = 8

        return blockState

    colorString = input("Enter a block color: ")
    state = getWoolState(colorString)

    pos = mc.player.getTilePos()
    mc.setBlock(pos.x, pos.y, pos.z, 35, state)

while Loops
~~~~~~~~~~~~~~~


.. code-block:: python

    def printMultiple(toPrint, repeats):
    """ Prints a string a number of times determined by the repeats variable """
    count = 0
    while count < repeats:
    print(toPrint)
    count += 1

    def doubleUntilHundred(numberToDbl):
    """ Doubles a number until it is greater than 100. Returns the number of
        times the number was doubled """
        count = 0
        while numToDbl < 100:
            numberToDbl = numberToDbl * 2
            count += 1
        return count


Mission #45: Blocks, Everywhere
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
다음 미션을 수행해 보자.


.. code-block:: python

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    import random


    def randomBlockLocations(blockType, repeats):
        """Creates blocks at random locations"""
        count = 0
        while count < repeats:
            x = random.randrange(-127, 128)
            z = random.randrange(-127, 128)
            y = mc.getHeight(x, z)
            mc.setBlock(x, y, z, blockType)
            count += 1

    randomBlockLocations(103, 10)
    randomBlockLocations(35, 37)
    randomBlockLocations(57, 102)





8.3 Global and Local Variables
-----------------------------------
글로벌 변수와 로컬 변수에 대해서 알아 보자.

.. code-block:: python


    eggs = 12
    def increaseEggs():
         eggs += 1
        print(eggs)
    increaseEggs()

상기 코드는 에러를 표현한다.
두개의 eggs값이 다르기때문이다.


.. code-block:: python


    >>> eggs =12
    >>> def increaseEggs():
        eggs=0
        eggs +=1
        print(eggs)


    >>> increaseEggs()
    1
    >>> print(eggs)
    12
    >>>
로컬 변수와 차별을 위해 글로벌 변수 앞에는 global 이라고 표현한다.
상기에는 묵시적 global로 표기된 eggs값을 로컬 변수 eggs값에서 변경할 수 없다.

.. code-block:: python

    eggs = 12
    def increaseEggs():
        global eggs
        eggs += 1
        print(eggs)


    increaseEggs()

Mission #46: A Moving Block
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

다음 미션을 수행해 보자.

.. code-block:: python

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    import time


    def calculateMove():
        """ Changes the x and z variables for a block. If the block
        in front of the block is less than 2 blocks higher it will move
        forward, otherwise it will try to move left, then backwards,
        then finally right."""
        global x
        global y
        global z

        currentHeight = mc.getHeight(x, z) - 1

        forwardHeight = mc.getHeight(x + 1, z)
        rightHeight = mc.getHeight(x, z + 1)
        backwardHeight = mc.getHeight(x - 1, z)
        leftHeight = mc.getHeight(x, z - 1)

        if forwardHeight - currentHeight < 3:
            x += 1
        elif rightHeight - currentHeight < 3:
            z += 1
        elif leftHeight - currentHeight < 3:
            z -= 1
        elif backwardHeight - currentHeight < 3:
            x -= 1

        y = mc.getHeight(x, z)


    pos = mc.player.getTilePos()
    x = pos.x
    z = pos.z
    y = mc.getHeight(x, z)

    while True:
        # calculate block movement
        calculateMove()

        # place block
        mc.setBlock(x, y, z, 103)

        # wait
        time.sleep(1)

        # remove the block
        mc.setBlock(x, y, z, 0)





8.4 What You Learned
-----------------------


create and call functions

return statements


functions return values

loops and if statements inside functions


