chapter 6: Making Mini-Games with if Statements
=================================================
이 장에서는 조건문에 대해서 배워 보도록 하자.


6.1 Using if Statements
---------------------------


Mission #26: Blast a Crater
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

다음은 사용자 입력을 받아서 입력 하라고 하면 블력을 생성하는 프로그램이다.

.. code-block:: python


    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()
    answer = input("Create a crater? Y/N ")

    if answer == "Y":
        pos = mc.player.getPos()
        mc.setBlocks(pos.x + 1, pos.y + 1, pos.z + 1, pos.x - 1, pos.y - 1, pos.z - 1, 0)
        mc.postToChat("Boom!")

Mission #27: Prevent Smashing, or Not
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
다음은 immutable을 활용해서 else 구문을 적용한 코드이다.

.. code-block:: python

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    answer = input("Do you want to make the blocks immutable? Y/N ")

    if answer == "Y":
        mc.setting("world_immutable", True)
        mc.postToChat("World is immutable")
    else:
        mc.setting("world_immutable", False)
        mc.postToChat("World is mutable")

Mission #28: Offer a Gift
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

다이아몬드인지를 판별하고 다른 조건이 나오고...마지막 조건은 특정 위치로 다이아몬드를 가져 가라는 코드이다.


.. code-block:: python

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()
    x = 10
    y = 11
    z = 12
    gift = mc.getBlock(x, y, z)

    # if gift is a diamond block
    if gift == 57:
        mc.postToChat("Thanks for the diamond.")
    # else if gift is a sapling
    elif gift == 6:
        mc.postToChat("I guess tree saplings are as good as diamonds...")
    else:
        mc.postToChat("Bring a gift to " + str(x) + ", " + str(y) + ", " + str(z))


Mission #29: Teleport to the Right Place
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

if,elif,else문에 대한 활용 코드이다.

.. code-block:: python

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()


    points = int(input("Enter your points: "))
    if points > 6:
        mc.player.setPos(32, 18, -38)
    elif points > 4:
        mc.player.setPos(60, 20, 32)
    elif points > 2:
        mc.player.setPos(112, 10, 112)
    elif points <= 2:
        mc.player.setPos(0, 12, 20)
    else:
        mc.postToChat("I don't know what to do with that information.")


Nested if Statements
~~~~~~~~~~~~~~~~~~~~~~~~


이중 if문을 가질때 안쪽에 들어가는 if문을 말한다.



Mission #30: Open a Secret Passage
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

이번 미션을 수행하기 위하여 이전장에서 실행했던 빌딩을 지어보도록 하자.

.. code-block:: python

    from mcpi.minecraft import Minecraft
    import time

    mc = Minecraft.create()

    mc.player.setTilePos(20,1,20)

    pos = mc.player.getTilePos()
    x = pos.x
    y = pos.y
    z = pos.z
    """
    width = 3
    height = 1
    length = 3
    """

    width = 10
    height = 5
    length = 6



    blockType = 4

    #blockType = 0

    air = 0


    time.sleep(5)
    mc.player.setTilePos(x-1,y,z-1)

    mc.setBlocks(x, y, z, x + width, y + height, z + length, blockType)
    #mc.setBlocks(x , y , z ,x + width , y + height , z + length , air)
    mc.setBlocks(x + 1, y + 1, z + 1,x + width - 2, y + height - 2, z + length - 2, 0)
    diamond=57
    mc.setBlocks(x+5, y, z, x + 6, y + 1, z + 1, diamond)


그리고 다음 코드를 실행해 보자.
다이아몬드 블럭을 체크한후 다이아몬드 블럭이면 블럭을 지우는 코드를 실행해 보자.

.. code-block:: python


    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    # x = 10
    # y = 11
    # z = 12

    x = 20
    y = 1
    z = 20


    gift = mc.getBlock(x+5, y, z+1)
    mc.postToChat(gift)

    if gift != 0:
        if gift == 57:
    #         mc.setBlocks(5, -2, 5, 6, -1, 6, 0)
            mc.setBlocks(x+5, y, z, x+6, y+1, x+1, 0)
        else:
    #         mc.setBlocks(4, -3, 4, 7, -3, 4, 10)
            mc.setBlocks(20, 1, 20, 19, 1, 19, 0)
    else:
        mc.postToChat("Place an offering on the pedestal.")










6.2 Using if Statements to Test a Range of Values
----------------------------------------------------

입력된 숫자나 기타 조건이 범위가 주어질때 쓰인다.

다음 코드를 입력해 보자.
x,y,z 좌표값이 잘못 입력했을때 체크하는 구문이다.



.. code-block:: python

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    valid = True

    x = int(input("Enter x: "))
    y = int(input("Enter y: "))
    z = int(input("Enter z: "))

    if not -127 < x < 127:
        valid = False
    # check if y is not between -63 and 63
    if not -63 < y < 63:
        valid = False
    # check if z is not between -127 and 127
    if not -127 < z < 127:
        valid = False

    if valid:
        mc.player.setPos(x, y, z)
    else:
        mc.postToChat("Please enter a valid location")








6.3 Boolean Operators and if Statements
--------------------------------------------

Mission #32: Take a Shower
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
skip this mission


6.4 What You Learned
-------------------------

if statements, else statements, and elif statements