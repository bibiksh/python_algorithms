chapter 5: Figuring Out What’s True and False with Booleans
===============================================================


5.1 Boolean Basics
----------------------------
A Boolean is a bit like a light switch: it is either True (on) or False (off)


Mission #17: Stop Smashing Blocks!
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

마인크래프트에서 immutable 설정을 on으로 하는 프로그램을 실행해 봅시다.

.. code-block:: python

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    mc.setting("world_immutable", True)


반대로 immutable 설정을 off로 하는 프로그램을 실행해 봅시다.

.. code-block:: python

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    mc.setting("world_immutable", False)




5.2 Concatenating Booleans
---------------------------------

이전장에서 배운것처럼 boolean 변수도 string으로 변환될 필요가 있다.

agree = True
print("I agree: " + str(agree))
I agree: True



5.3 Comparators
-------------------
연산자를 의미한다.
많이 쓰이는 기본적인 연산자들은 다음과 같다.

.. sourcecode:: pycon

    • Equal to (==)
    • Not equal to (!=)
    • Less than (<)
    • Less than or equal to (<=)
    • Greater than (>)
    • Greater than or equal to (>=)

Equal To
~~~~~~~~~~

두개의 값이 동일한지 판단을 할때 쓰인다.


Mission #18: Am I Swimming?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

다음 코드를 실행해 보자.
block type이 물인지 판별하는 코드이다.

.. code-block:: python

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    pos = mc.player.getPos()
    x = pos.x
    y = pos.y
    z = pos.z

    blockType = mc.getBlock(x, y, z)
    mc.postToChat(blockType == 9)

block type이 9이면 물이다.


Mission #19: Am I Standing in Something  Other Than Air?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

공중에 떠있는지 확인 하는 코드를 실행해 보자.

.. code-block:: python

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    pos = mc.player.getPos()
    x = pos.x
    y = pos.y
    z = pos.z

    blockType = mc.getBlock(x, y, z)
    notAir = blockType != 0
    mc.postToChat("The player is not standing in air: " + str(notAir))


Mission #20: Am I Above the Ground?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

다음 코드를 실행해 보자.

.. code-block:: python


    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    pos = mc.player.getTilePos()
    x = pos.x
    y = pos.y
    z = pos.z
    highestBlockY = mc.getHeight(x, z)
    aboveGround = y >= highestBlockY
    mc.postToChat("The player is above ground: " + str(aboveGround))



Mission #21: Am I Close to Home?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

다음은 임의의 홈을 설정후 가깝게 있는지 확인하는 코드이다.

.. code-block:: python

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    import math

    homeX = 10
    homeZ = 10
    pos = mc.player.getTilePos()
    x = pos.x
    z = pos.z
    distance = math.sqrt((homeX - x) ** 2 + (homeZ - z) ** 2)
    far = distance <= 40
    mc.postToChat("Your house is nearby: " + str(far))






5.4 Logical Operators
------------------------
 and,or,not 연산자등이 있다.

다음은  and 연산자에 대한 두개값의 결과이다.


.. image:: ./img/chapter5-1.png


Mission #22: Am I Entirely Underwater?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

player가 물밑에 있는지  확인하는 로직이다.

.. code-block:: python

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    pos = mc.player.getPos()
    x = pos.x
    y = pos.y
    z = pos.z

    blockType = mc.getBlock(x, y, z)
    blockType2 = mc.getBlock(x, y + 1, z)

    underwater = blockType == 9 and blockType2 == 9
    mc.postToChat("The player is underwater: " + str(underwater))


다음은  or 연산자에 대한 두개값의 결과이다.


.. image:: ./img/chapter5-2.png


Mission #23: Am I in a Tree?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

다음은 player가 나무에 있는지 확인하는  코드이다.


.. code-block:: python

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    pos = mc.player.getPos()
    x = pos.x
    y = pos.y
    z = pos.z

    blockType = mc.getBlock(x, y - 1, z)
    inTree = blockType == 18 or blockType == 11
    mc.postToChat("The player is in a tree: " + str(inTree))


Mission #24: Is This Block Not a Melon?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

다음 코드는 멜론 블럭인지 확인하는 코드이다.

.. code-block:: python

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    x = 10
    y = 11
    z = 12
    melon = 103
    block = mc.getBlock(x, y, z)

    noMelon = not block == melon

    mc.postToChat("You need to get some food: " + str(noMelon))


Logical Operator Order
~~~~~~~~~~~~~~~~~~~~~~~

로직컬 연산자는 다음순으로 우선순위가 있다.

.. sourcecode:: pycon


    1. not
    2. and
    3. or



Mission #25: Am I in the House?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

player가 집에 있는지 확인하는 코드이다.

.. code-block:: python


    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    buildX = 10
    buildY = 11
    buildZ = 12
    width = 10
    height = 5
    length = 6

    pos = mc.player.getTilePos()
    x = pos.x
    y = pos.y
    z = pos.z

    inside = buildX < x < buildX + width and buildY < y < buildY + height and buildZ < z < buildZ + length
    mc.postToChat("The player is at home: " + str(inside))





5.5 What You Learned
-----------------------------

이 장에서는 Booleans, comparators, and logical operators 등을 배웠다.

