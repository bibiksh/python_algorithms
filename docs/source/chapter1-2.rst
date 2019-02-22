chapter 2: 변수로 이동하기
=========================================


2.1 프로그램이란 무엇인가
--------------------------


컴퓨터가 특정한 업무를 할 수 있도록 일련의 명령 집합이다.



2.2 변수값 저장하기
---------------------------------
이 장에서 배우게 될 중요한 내용은 변수이다.
variable 로 표현되며 여러가지 내용물을 채울 수 있는 모양이 변형되는 그릇이라고 생각하면 된다.

pickaxes = 12 할당해 보자.

bread=145  할당해 보자.


.. code-block:: python

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()
    import time

    pickaxes = 12

    bread=145

    time.sleep(2)
    mc.postToChat(pickaxes)

    time.sleep(2)
    mc.postToChat(bread)



다음은 입력이 안된다.

pickaxes = 12 iron = 30 cobblestone = 25

상기처럼 계속 입력행태가 들어가면 오류가 난다.



Syntax Rules for Variables
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

다음은 변수로 쓸수 없는 규칙이다.

Don’t include symbols in your variable names, except for underscores (_),
or you’ll get a syntax error.

Don’t start a variable name with a number, as in 9bread. Using numbers
elsewhere in a variable name is fine, as in bread9.

You don’t need to add spaces on either side of the equal sign: your program
will run fine without them. But they do make the code easier to
read, so it’s a good idea to add them.

변수 이름에 심볼을 넣으면 안된다.예외 _
숫자로 첫 변수이름을 쓰면 안된다. 예 ,9bread, bread9 OK
할당 (=) 기호에 스페이스를 넣을 필요가 없다.

변수에 값이 저장되었더라도, 그것은 저장이 안된다. 변수값은 컴퓨터의 임시 저장소에 저장된다.
따라서 프로그램이 바뀌거나 하면 값이 사라지게 된다.
IDLE에서 변수값이 저장되는지 확인해 보자.


변수값 바꾸기
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

변수는 변경이 가능하다.


.. code-block:: python

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()
    import time

    pickaxes = 12

    bread=145

    time.sleep(2)
    mc.postToChat(pickaxes)


    time.sleep(2)
    mc.postToChat(bread)


    time.sleep(2)

    pickaxes = 30
    bread=20

    time.sleep(2)
    mc.postToChat(pickaxes)


    time.sleep(2)
    mc.postToChat(bread)

Integers
~~~~~~~~~~~~~~~~~

정수를 의미한다.
다음에서 x,y,z 변수값을 넣어 보자.
라즈베리 파이에서 평면은
X : -127 ~ 127
Y : -127 ~ 127
Z : -127 ~ 127
공간 안에서만 입력할 수 있다.
프로그램상에서는 다양한 값을 넣을 수 있다.


.. code-block:: python


    from mcpi.minecraft import Minecraft
    import mcpi.block as block
    import time

    mc = Minecraft.create()


    #Set x, y, and z variables to represent coordinates

    x = 60
    y = 1
    z = 113
    """
    x = 0
    y = 0
    z = 0
    """
    #Change the player's position
    # mc.player.setTilePos(x, y, z)
    mc.player.setTilePos(x, y, z)

    time.sleep(5)

    mc.postToChat("this is sean notebook")



Floats
~~~~~~~~~~~~~~~~~

정수를 포함한 소수까지 확장은 넓은 변수이다.
소숫점 이하 정확한 지점까지 이동해 보자.

.. code-block:: python


    #Connect to Minecraft
    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    #Set x, y, and z variables to represent coordinates
    x = 63.5
    y = 1.0
    z = 113.5

    #Change the player's position
    mc.player.setPos(x, y, z)



2.3 타임 모듈을 이용해서 천천히 또는 잠시 대기상태를 만들어보자
--------------------------------------------------------------

player를 좀 느리게 처리를 하려면 다음 모듈을 쓰면 된다.

.. code-block:: python


    import time

    time.sleep(초)






2.4 Debugging
-------------------
Everyone makes mistakes

다음을 실행해 보자.

.. code-block:: python

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    #Set x, y, and z variables to represent coordinates
    #x = 63.5
    y = 1.0
    z = 113.5

    #Change the player's position
    mc.player.setPos(x, y, z)


버그를 수정해 보자.
버그 1

.. code-block:: python


    from mcpi.minceraft inport Minecraft
    # mc = Minecraft.create()

    x = 10
    y = 11
    z = 12


버그를 수정해 보자.
버그 2

.. code-block:: python

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    x = 120
    y = 4
    z = -12

    # mc.player.setPos(x, z, y)
    mc.player.setTilePos(x, y, z)




2.5 What You Learned
-----------------------

player position


variables
- integers
- floats

setPos()
setTilePos()
time.sleep(초)



