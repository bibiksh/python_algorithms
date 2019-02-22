chapter 9: Hitting Things with Lists and Dictionaries
========================================================

이 장에서는 데이터 타입으로 List 와 Dictionary를 배워보도록 하겠다.

9.1 Using Lists
-------------------

리스트는 다음처럼 표기한다.

.. code-block:: python


    emptyList = []

빈 리스트를 작성할 수도 있고 다음처럼 초기화 값을 갖는 리스트도 표현 가능하다.

.. code-block:: python

    noodleSoup = ["water", "soy sauce", "spring onions", "noodles", "beef"]



초기화 값은 integer 또는 string을 집어 넣을 수 있다.

.. code-block:: python

    wackyList = ["cardigan", 33, "goofballs"]




Accessing a List Item
~~~~~~~~~~~~~~~~~~~~~~~~~
리스트의 호출은 다음과 같이 한다.

.. code-block:: python

    print(noodleSoup[0])


Changing a List Item
~~~~~~~~~~~~~~~~~~~~~~~~~~~
list값은 mutable이다. 따라서 변경가능하다는 얘기다.

다음처럼 직접 접근해서 변경가능하다.

.. code-block:: python

    noodleSoup[4] = "chicken"



Mission #47: High and Low
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

다음 미션을 수행해 보자.

.. code-block:: python

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    import time

    heights = [100, 0]
    count = 0

    while count < 60:
        pos = mc.player.getTilePos()

        if pos.y < heights[0]:
            heights[0] = pos.y
        elif pos.y > heights[1]:
            heights[1] = pos.y

        count += 1
        time.sleep(1)

    mc.postToChat("Lowest: " + str(heights[0]))
    mc.postToChat("Highest: " + str(heights[1]))

이동한 곳의 가장 높은곳과 낮은곳을 찾는 코드이다.
약간의 시간이 필요하다.






9.2 Manipulating Lists
--------------------------

리스트는 내장 함수로 추가 삭제가 가능하다.

Adding an Item
~~~~~~~~~~~~~~~~~~

.. code-block:: python

    noodleSoup.append("vegetables")

    food = []
    food.append("cake")

Inserting an Item
~~~~~~~~~~~~~~~~~~~
중간에 집어 넣을 수도 있다.


.. code-block:: python

    noodleSoup = ["water", "soy sauce", "spring onions", "noodles", "beef", "vegetables"]

    noodleSoup.insert(3, "pepper")

    ["water", "soy sauce", "spring onions", "pepper", "noodles", "beef", "vegetables"]

 만약 리스트를 넘는 곳에 넣게 되면 자동적으로 맨 마지막에 넣어지게 된다.

.. code-block:: python

    noodleSoup.insert(10, "salt")

    ["water", "soy sauce", "spring onions", "pepper", "noodles", "beef","vegetables", "salt"]

 Deleting an Item
~~~~~~~~~~~~~~~~~

다음처럼 아이템을 삭제할 수  있다.

.. code-block:: python

    del noodleSoup[5]


인덱스 번호를 모를 경우는 다음처럼 처리하면 된다.

.. code-block:: python

    beefPosition = noodleSoup.index("beef")
    del noodleSoup[beefPosition]


Mission #48: Progress Bar
~~~~~~~~~~~~~~~~~~~~~~~~~~
다음 미션을 수행해 보자.
10개의 유리 상자를 쌓은 다음에 하나씩 barblock으로 교체하는 코드이다.

.. code-block:: python

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    import time

    pos = mc.player.getTilePos()
    x = pos.x + 1
    y = pos.y
    z = pos.z

    # Add 10 glass blocks (block id 20) to this list
    blocks = [20, 20, 20, 20, 20, 20, 20, 20, 20, 20]
    barBlock = 22  # Lapis lazuli

    count = 0
    while count <= len(blocks):
        # Add setBlock() for the remaining blocks in the list
        mc.setBlock(x, y, z, blocks[0])
        mc.setBlock(x, y + 1, z, blocks[1])
        mc.setBlock(x, y + 2, z, blocks[2])
        mc.setBlock(x, y + 3, z, blocks[3])
        mc.setBlock(x, y + 4, z, blocks[4])
        mc.setBlock(x, y + 5, z, blocks[5])
        mc.setBlock(x, y + 6, z, blocks[6])
        mc.setBlock(x, y + 7, z, blocks[7])
        mc.setBlock(x, y + 8, z, blocks[8])
        mc.setBlock(x, y + 9, z, blocks[9])

        count += 1

        # Delete the last block in the list
        del blocks[9]

        # Insert a bar block at the first position in the list
        blocks.insert(0, barBlock)

        time.sleep(2)






9.3 Treating Strings like Lists
------------------------------------
스크링을 리스트처럼 쓰이기도 한다.

.. code-block:: python

    flavor = "Grape"
    print(flavor[1])

    firstName = "Lyra"
    lastName = "Jones"
    initials = firstName[0] + " " + lastName[0]
    print(initials)
    L J




9.4 Tuples
-------------------
Tuples are a type of list that is immutable
변경이 불가능한 리스트 타입이라고 보면 된다.
표현은 아래처럼 한다.

.. code-block:: python

    distance = (5.17, 5.20, 4.56, 53.64, 9.58, 6.41, 2.20)

한개의 값은 다음처럼 입력한다. ","는 꼭 입력한다.

.. code-block:: python

    distance = (5.17,)

Setting Variables with Tuples
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
tuple은 다음처럼 유용하게 쓰인다.


.. code-block:: python


    measurements = 6, 30


    width, height = 6, 30

Mission #49: Sliding
~~~~~~~~~~~~~~~~~~~~~~

tuple을 이용해서 다음처럼 쓸 수 있다.

.. code-block:: python

    x = 10
    y = 11
    z = 12

    x, y, z = 10, 11, 12

다음 코드를 실행해 보자.

.. code-block:: python

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    import random
    import time

    pos = mc.player.getPos()
    x, y, z = pos.x, pos.y, pos.z

    while True:
        x += random.uniform(-0.2, 0.2)
        z += random.uniform(-0.2, 0.2)
        y = mc.getHeight(x, z)

        mc.player.setPos(x, y, z)
        time.sleep(0.1)

Returning a Tuple
~~~~~~~~~~~~~~~~~~~~~~
tuple로 리턴값을 줄 수 있다.

.. code-block:: python

    def getDateTuple(dateString):
    year = int(dateString[0:4])
    month = int(dateString[5:7])
    day = int(dateString[8:10])
    return year, month, day

다음처럼 string을 tuple로 리턴할 수 있다.

.. code-block:: python

    getDateTuple("1997-09-27")
    (1997, 9, 27)

    year, month, day = getDateTuple("1997-09-27")

9.4 Other Useful Features of Lists
--------------------------------------

List Length
~~~~~~~~~~~~~
리스트의 크기를 다음처럼 구할 수 있다.


.. code-block:: python

    >>> noodleSoup = ["water", "soy sauce", "spring onions", "noodles", "beef",
    "vegetables"]
    >>> print(len(noodleSoup))

Mission #50: Block Hits
~~~~~~~~~~~~~~~~~~~~~~~~~

60초 동안 블럭을 터치하고 터치한 블럭 갯수를 구하는 코드를 구해 보자.

.. code-block:: python

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    import time

    #Wait 60 seconds
    time.sleep(60)

    #Get the list of block hits
    blockHits = mc.events.pollBlockHits()

    #Display the length of the block hits list to chat
    blockHitsLength = len(blockHits)
    mc.postToChat("Your score is " + str(blockHitsLength))


Randomly Choosing an Item
~~~~~~~~~~~~~~~~~~~~~~~~~~~
다음처럼 list에서 임으로 선택하는 것을 쓸 수 있다.

.. code-block:: python

    import random
    colors = ["red", "green", "blue", "yellow", "orange", "purple"]
    print(random.choice(colors))

Mission #51: Random Block
~~~~~~~~~~~~~~~~~~~~~~~~~~
다음처럼 리스트에서 임의로 선택하는 블럭을 쓸 수 있다.

.. code-block:: python

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    import random

    pos = mc.player.getTilePos()
    x, y, z = pos.x, pos.y, pos.z

    blocks = [57, 41, 22, 42, 103]
    block = random.choice(blocks)

    mc.setBlock(x, y, z, block)

Copying a List
~~~~~~~~~~~~~~~~~~

다음 코드를 실행해 보자.

.. code-block:: python

    >>> cake = ["Eggs",
    "Butter",
    "Sugar",
    184 Chapter 9
    "Milk",
    "Flour"]
    >>> print(id(cake))

다음처럼 복사할 경우 달라야 되는데 출력해 보면 동일하다.
이건 컴퓨터가 실제로 동일 주소를 가지고 있고 복사한것이 아니다.

.. code-block:: python

    >>> cake = ["Eggs",
    "Butter",
    "Sugar",
    "Milk",
    "Flour"]
    >>> # Store the list in a second variable
    >>> chocolateCake = cake
    >>> chocolateCake.append("Chocolate")

다음처럼 하면 복사한 다른 개체가 생성된다.

.. code-block:: python

    >>> chocolateCake = cake[:]


Items and if Statements
~~~~~~~~~~~~~~~~~~~~~~~~~~
To find out whether a value is in a list, you can use the in operator

다음을 보자.

.. code-block:: python


    >>> cake = ["Eggs", "Butter", "Sugar", "Milk", "Flour"]
    >>> print("Eggs" in cake)

    >>> cake = ["Eggs", "Butter", "Sugar", "Milk", "Flour"]
    >>> if "Ham" in cake:
    >>> print("That cake sounds disgusting.")
    >>> else:
    >>> print("Good. Ham in a cake is a terrible mistake.")

    >>> cake = ["Eggs", "Butter", "Sugar", "Milk", "Flour"]
    >>> if "Ham" not in cake:
    >>> print("Good. Ham in a cake is a terrible mistake.")
    >>> else:
    >>> print("That cake sounds disgusting")


Mission #52: Night Vision Sword
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
다음 미션을 수행해 보자.
다이아몬드 블럭을 터치했을 경우 빠져 나가는 코드이다.

.. code-block:: python


    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    import time

    blocks = []
    i=0
    while i<100:
        hits = mc.events.pollBlockHits()
        i +=1
        if len(hits) > 0:
            hit = hits[0]
            hitX, hitY, hitZ = hit.pos.x, hit.pos.y, hit.pos.z
            block = mc.getBlock(hitX, hitY, hitZ)
            blocks.append(block)

        if 56 in blocks:
            mc.postToChat("You found some diamond ore!")
            break

        time.sleep(0.2)



9.4 Dictionaries
-------------------
a set of keys 로 주어지는 리스트라고 생각하면 된다.

.. code-block:: python

    person = {'name': 'David',
    'age': 42,
    'favoriteAnimal': 'Snake',
    'favoritePlace': 'Inside a cardboard box'}


    trainTimes = {1.00: 'Castle Town',
    2.30: 'Sheep Farm',
    3.15: 'Lake City',
    3.45: 'Castle Town',
    3.55: 'Storage Land'
    }

Accessing Items in Dictionaries
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: python


    person = {'name': 'David',
    'age': 42,
    'favoriteAnimal': 'Snake',
    'favoritePlace': 'Inside a cardboard box'}
    agentName = person['name']


Mission #53: Sightseeing Guide
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
다음 미션을 수행해 보자.

.. code-block:: python


    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    places = {"House": (10, 11, 12),
              "Tower": (20, -2, 3),
              "Store room": (6, 2, 1)}

    choice = ""
    while choice != "exit":
        choice = input("Enter a location ('exit' to close): ")
        if choice in places:
            location = places[choice]
            x, y, z = location[0], location[1], location[2]
            mc.player.setTilePos(x, y, z)

Changing or Adding an Item ina Dictionary
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Dictionary도 변경 추가 가능하다.


.. code-block:: python

    person['age'] = 43

삭제도 가능하다.

.. code-block:: python


    del person['favoriteAnimal']


Mission #54: Block Hits Score
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
다음 미션을 수행해 보자.

.. code-block:: python


    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    import time

    name = ""
    scoreboard = {}

    while True:
        # Get the player's name
        name = input("What is your name? ")

        # Break loop if name is exit
        if name == "exit":
            break
        mc.postToChat("Go!")

        # Wait 60 seconds
        time.sleep(60)

        # Get the list of block hits
        blockHits = mc.events.pollBlockHits()

        # Display the length of the block hits list to chat
        blockHitsLength = len(blockHits)
        mc.postToChat("Your score is " + str(blockHitsLength))

        scoreboard[name] = blockHitsLength

        print(scoreboard)






9.4 What You Learned
----------------------

lists, tuples, and dictionaries

wackyList = ["cardigan", 33, "goofballs"]

distance = (5.17, 5.20, 4.56, 53.64, 9.58, 6.41, 2.20)

person = {'name': 'David',
    'age': 42,
    'favoriteAnimal': 'Snake',
    'favoritePlace': 'Inside a cardboard box'}