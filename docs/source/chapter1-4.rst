chapter 4: Chatting with Strings
=====================================


4.1 What Are Strings?
-----------------------
A string data type includes any amount of text, from a single letter or
symbol—like "a" or "&"—to a large block of text


Mission #11: Hello, Minecraft World
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

다음 코드를 실행해 보자.

.. code-block:: python


    from mcpi.minecraft import Minecraft
    import time
    mc = Minecraft.create()
    time.sleep(2)
    mc.postToChat("Hello, Minecraft World")
    time.sleep(2)
    mc.postToChat("This is sean kim")

player가 어느 위치에 있는지 출력을 해보자.

.. code-block:: python

    from mcpi.minecraft import Minecraft
    import time
    mc = Minecraft.create()

    pos = mc.player.getTilePos()

    x=pos.x
    y=pos.y
    z=pos.z

    mc.postToChat(x)
    mc.postToChat(y)
    mc.postToChat(z)

    time.sleep(2)
    mc.postToChat("Hello, Minecraft World")
    time.sleep(2)
    mc.postToChat("This is sean kim")



4.2 The print() Function
----------------------------

postToChat 역할과 동일한 역할을 하는 함수이다.
파이썬 코드에서 string 출력을 위해서 많이 쓰인다.



4.3 The input() Function
---------------------------
사용자의 입력값을 기다릴때 쓰인다.

다음 코드를 입력해 보자.

.. code-block:: python


    from mcpi.minecraft import Minecraft
    import time
    mc = Minecraft.create()
    mcid=mc.getPlayerEntityIds()
    mc.postToChat(mcid)

    blockType = int(input("Enter a block type: "))
    pos = mc.player.getTilePos()
    x = pos.x
    y = pos.y
    z = pos.z
    time.sleep(2)
    mc.setBlock(x, y, z, blockType)

    time.sleep(2)
    mc.player.setTilePos(x,y,z-5)
    mc.player.setTilePos(mcid)
    mc.postToChat("mission cleared")


Mission #12: Write Your Own Chat Message
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

다음 코드를 입력해 보자

.. code-block:: python

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    message = input("Enter your message: ")
    mc.postToChat(message)





4.4 Joining Strings
----------------------
String을 합치는 작업을 말한다.

.. code-block:: python

    from mcpi.minecraft import Minecraft
    import time
    mc = Minecraft.create()

    firstName='John'
    LastName='Lenon'

    fullname=firstName+LastName

    time.sleep(2)
    mc.postToChat(fullname)

Converting Numbers to Strings
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

숫자를 String으로 표현해서 나타낼때가 있는데 다음의 경우
숫자를 String으로 변경해서 표현한다.
the str() function, which converts non-string data types into strings


다음 코드를 실행해 보자.

.. code-block:: python


    import time
    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    pos1 = mc.player.getTilePos()
    x1 = pos1.x
    y1 = pos1.y
    z1 = pos1.z

    time.sleep(10)

    pos2 = mc.player.getTilePos()
    x2 = pos2.x
    y2 = pos2.y
    z2 = pos2.z

    # Compare the difference between the starting position and ending position
    xDistance = x2 - x1
    yDistance = y2 - y1
    zDistance = z2 - z1

    #Post the results to the chat
    mc.postToChat("The player has moved x: " + str(xDistance) + ", y: "
        + str(yDistance) + ", and z: " + str(zDistance))

Mission #13: Add Usernames to Chat
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

다음 코드를 출력해 보자.

.. code-block:: python

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    userName = input("Enter your username: ")
    message = input("Enter your message: ")
    mc.postToChat(userName + ": " + message)




4.5 Converting Strings to Integers with int()
-----------------------------------------------
the int() function converts non-integer data types into integer






Mission #14: Create a Block with Input
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

블락타입을 입력받아서 처리하는 코드를 출력해 보자.

.. code-block:: python

    from mcpi.minecraft import Minecraft
    import time
    mc = Minecraft.create()
    mcid=mc.getPlayerEntityIds()
    mc.postToChat(mcid)

    blockType = int(input("Enter a block type: "))
    pos = mc.player.getTilePos()
    x = pos.x
    y = pos.y
    z = pos.z
    time.sleep(2)
    mc.setBlock(x, y, z, blockType)

    time.sleep(2)
    mc.player.setTilePos(x,y,z-5)
    mc.player.setTilePos(mcid)
    mc.postToChat("mission cleared")




4.6 Bounce Back from Errors
-------------------------------

Python uses exception handling to make sure your program can recover from
errors and continue running when they occur

기본 형은
try:
    XXX
except:
    XXXX



Mission #15: Only Numbers Allowed
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

다음 숫자만 입력할 수 있는 코드를 출력해 보자.

.. code-block:: python


    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    pos = mc.player.getTilePos()
    x = pos.x
    y = pos.y
    z = pos.z

    try:
        blockType = int(input("Enter a block type: "))
        mc.setBlock(x, y, z, blockType)
    except:
        mc.postToChat("You did not enter a number! Enter a number next time.")


Mission #16: Sprint Record
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

두 지점 이동한 거리를 출력하는 코드를 짜보자.
중간에 sleep을 두자


.. code-block:: python


    import time
    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    pos1 = mc.player.getTilePos()
    x1 = pos1.x
    y1 = pos1.y
    z1 = pos1.z

    time.sleep(10)

    pos2 = mc.player.getTilePos()
    x2 = pos2.x
    y2 = pos2.y
    z2 = pos2.z

    # Compare the difference between the starting position and ending position
    xDistance = x2 - x1
    yDistance = y2 - y1
    zDistance = z2 - z1

    #Post the results to the chat
    mc.postToChat("The player has moved x: " + str(xDistance) + ", y: "
        + str(yDistance) + ", and z: " + str(zDistance))




4.7 What You Learned
------------------------

string
print
join string
user input
data type change
handled exception




