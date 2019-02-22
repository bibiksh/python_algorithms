chapter 12: Getting Classy with Object-Oriented Programming
=============================================================
객체지향 프로그램에 대해서 알아본다 .
OOP(Object-Oriented-Programming)
객체지향 프로그램은 모든 사물을 객체로 보고 각각 기능과 변수들을 정의 하고 쓰는 개념이다.
그렇게 정의된 함수나 변수들의 집단을 Class라고 정의 하고 이 함수나 변수들을
재사용하는게 가장 중요한 요소가 된다.
class에서 쓰이는 fuction을 method라고 한다.
그리고 변수들을 attribute라고 한다.
OOP의 특성이나 기능들은 차차 알아보도록 하자.

12.1 Object-Oriented Basics
-------------------------------

파이썬에서 클래스는 다음과 같이 정의한다.

.. code-block:: python

    class ClassName(object):
        def __init__(self):
            # Body of init



12.2 Creating a Class
-----------------------
다음의 클래스를 만들어 보자.

.. code-block:: python

    class Cat(object):
        owner = "Craig"
        def __init__(self, name, weight):
            self.name = name
            self.weight = weight
        def eat(self, food):
            self.weight = self.weight + 0.05
            print(self.name + " is eating " + food)
        def eatAndSleep(self, food):
            self.eat(food)
            print(self.name + " is now sleeping...")
        def getWeightInGrams(self):
            return self.weight * 1000

    fluff = Cat("Fluff", 4.5)  # Object 생성
    print(fluff.owner)

    stella = Cat("Stella", 3.9)  # Object 생성
    print(stella.owner)           # Accessing Attributes
    print(fluff.weight)           #Accessing Attributes

    fluff.eat("tuna")
    fluff.eatAndSleep("tuna")

    print(fluff.getWeightInGrams())
    print(fluff.name)
    print(stella.name)

    fluff.eat("tuna")
    stella.eat("cake")
    stella.owner = "Matthew"

    print(stella.owner)
    print(fluff.owner)

Mission #68: Location Objects
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
위치 이동하는 클래스를 만들어 보자.

.. code-block:: python

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    class Location(object):
        def __init__(self, x, y, z):
            self.x = x
            self.y = y
            self.z = z


    bedroom = Location(64, 52, -8)
    mc.player.setTilePos(bedroom.x, bedroom.y, bedroom.z)




12.3 Understanding Methods
------------------------------

Mission #69: Ghost House
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
다음 미션을 알아보도록 하자.

.. code-block:: python

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    import time

    class Building(object):
        def __init__(self, x, y, z, width, height, depth):
            self.x = x
            self.y = y
            self.z = z

            self.width = width
            self.height = height
            self.depth = depth

        def build(self):
            mc.setBlocks(self.x, self.y, self.z,
                         self.x + self.width, self.y + self.height, self.z + self.depth, 4)

            mc.setBlocks(self.x + 1, self.y + 1, self.z + 1,
                         self.x + self.width - 1, self.y + self.height - 1, self.z + self.depth - 1, 0)

            self.buildWindows()
            self.buildDoor()

        def clear(self):
            mc.setBlocks(self.x, self.y, self.z,
                         self.x + self.width, self.y + self.height, self.z + self.depth, 0)

        def buildWindows(self):
            mc.setBlock(self.x + (self.width / 4 * 3), self.y + 2, self.z, 0)
            mc.setBlock(self.x + (self.width / 4), self.y + 2, self.z, 0)

        def buildDoor(self):
            mc.setBlocks(self.x + (self.width / 2), self.y + 1, self.z, self.x + (self.width / 2), self.y + 2, self.z, 0)


    pos = mc.player.getTilePos()
    x = pos.x
    y = pos.y
    z = pos.z
    ghostHouse = Building(x, y, z, 10, 6, 8)
    ghostHouse.build()

    time.sleep(30)

    ghostHouse.clear()
    ghostHouse.x = 8



12.4 Returning Values with Methods
---------------------------------------

당연히 Function에서 배웠듯이 리턴값을 반환한다.

Mission #70: Ghost Castle
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
다음 미션을 수행해 보도록 하자.

.. code-block:: python

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    import time


    class NamedBuilding(object):
        def __init__(self, x, y, z, width, height, depth, name):
            self.x = x
            self.y = y
            self.z = z

            self.width = width
            self.height = height
            self.depth = depth

            self.name = name

        def build(self):
            mc.setBlocks(self.x, self.y, self.z,
                         self.x + self.width, self.y + self.height, self.z + self.depth, 4)

            mc.setBlocks(self.x + 1, self.y + 1, self.z + 1,
                         self.x + self.width - 1, self.y + self.height - 1, self.z + self.depth - 1, 0)

            self.buildWindows()
            self.buildDoor()

        def clear(self):
            mc.setBlocks(self.x, self.y, self.z,
                         self.x + self.width, self.y + self.height, self.z + self.depth, 0)

        def getInfo(self):
            return self.name + "'s location is at " + str(self.x) + ", " + str(self.y) + ", " + str(self.z)

        def buildWindows(self):
            mc.setBlock(self.x + (self.width / 4 * 3), self.y + 2, self.z, 0)
            mc.setBlock(self.x + (self.width / 4), self.y + 2, self.z, 0)

        def buildDoor(self):
            mc.setBlocks(self.x + (self.width / 2), self.y + 1, self.z, self.x + (self.width / 2), self.y + 2, self.z, 0)


    pos = mc.player.getTilePos()
    x = pos.x
    y = pos.y
    z = pos.z

    ghostCastle = NamedBuilding(x, y, z, 10, 16, 16, "Ghost Castle")
    ghostCastle.build()
    mc.postToChat(ghostCastle.getInfo())

    time.sleep(30)

    ghostCastle.clear()





12.5 Creating Multiple Objects
-----------------------------------

class안에는 여러개 object를 생성할 수 있다.


Mission #71: Ghost Town
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
다음 미션을 수행해 보도록 하자.

.. code-block:: python

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    import time

    class Building(object):
        def __init__(self, x, y, z, width, height, depth):
            self.x = x
            self.y = y
            self.z = z

            self.width = width
            self.height = height
            self.depth = depth

        def build(self):
            mc.setBlocks(self.x, self.y, self.z,
                         self.x + self.width, self.y + self.height, self.z + self.depth, 4)

            mc.setBlocks(self.x + 1, self.y + 1, self.z + 1,
                         self.x + self.width - 1, self.y + self.height - 1, self.z + self.depth - 1, 0)

            self.buildWindows()
            self.buildDoor()

        def clear(self):
            mc.setBlocks(self.x, self.y, self.z,
                         self.x + self.width, self.y + self.height, self.z + self.depth, 0)

        def buildWindows(self):
            mc.setBlock(self.x + (self.width / 4 * 3), self.y + 2, self.z, 0)
            mc.setBlock(self.x + (self.width / 4), self.y + 2, self.z, 0)

        def buildDoor(self):
            mc.setBlocks(self.x + (self.width / 2), self.y + 1, self.z, self.x + (self.width / 2), self.y + 2, self.z, 0)


    pos = mc.player.getTilePos()
    x = pos.x
    y = pos.y
    z = pos.z
    ghostHouse = Building(x, y, z, 10, 6, 8)
    ghostHouse.build()

    time.sleep(30)

    ghostHouse.clear()
    ghostHouse.x = 8

다음은 마을을 형성하는 코드이다.

.. code-block:: python


    import time

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()


    class Building(object):
        def __init__(self, x, y, z, width, height, depth):
            self.x = x
            self.y = y
            self.z = z

            self.width = width
            self.height = height
            self.depth = depth

        def build(self):
            mc.setBlocks(self.x, self.y, self.z,
                         self.x + self.width, self.y + self.height, self.z + self.depth, 4)

            mc.setBlocks(self.x + 1, self.y + 1, self.z + 1,
                         self.x + self.width - 1, self.y + self.height - 1, self.z + self.depth - 1, 0)

            self.buildWindows()
            self.buildDoor()

        def clear(self):
            mc.setBlocks(self.x, self.y, self.z,
                         self.x + self.width, self.y + self.height, self.z + self.depth, 0)

        def buildWindows(self):
            mc.setBlock(self.x + (self.width / 4 * 3), self.y + 2, self.z, 0)
            mc.setBlock(self.x + (self.width / 4), self.y + 2, self.z, 0)

        def buildDoor(self):
            mc.setBlocks(self.x + (self.width / 2), self.y + 1, self.z, self.x + (self.width / 2), self.y + 2, self.z, 0)


    pos = mc.player.getTilePos()
    x = pos.x
    y = pos.y
    z = pos.z

    ghostHouse = Building(x, y, z, 10, 6, 8)
    shop = Building(x + 12, y, z, 8, 12, 10)
    hospital = Building(x + 25, y, z - 1, 30, 40, 30)
    bakery = Building(x - 12, y - 5, z, 9, 11, 13)


    ghostHouse.build()
    shop.build()
    hospital.build()
    bakery.build()

    time.sleep(30)

    ghostHouse.clear()
    shop.clear()
    hospital.clear()
    bakery.clear()





12.6 Class Attributes
--------------------------
When multiple objects share the same attribute, it’s called a class attribute.




12.7 Understanding Inheritance
--------------------------------
OOP의 가장 큰 특징중에 하나가 상속성이다.
상위 클래스를 받아서 하위 클래스를 생성하면 상위 클래스 매쏘드나 머트리붓을 모두 갖는 특징을 갖는다.
그림으로 보면 다음과 같다.
superclass <->subclass 관계이다.


.. image:: ./img/chapter12-5.png


Inheriting a Class
~~~~~~~~~~~~~~~~~~~~
Class 상속은 다음과 같이 쓰인다.

.. code-block:: python


    class Bird(object):
        def __init__(self, name, wingspan):
            self.name = name
            self.wingspan = wingspan
        def birdcall(self):
            print("chirp")
        def fly(self):
            print("flap")
    class Penguin(Bird):
        def swim(self):
            print("swimming")
        def birdcall(self):
            print("sort of a quack")
        def fly(self):
            print("Penguins cannot fly :(")
    class Parrot(Bird):
        def __init__(self, name, wingspan, color):
            self.name = name
            self.wingspan = wingspan
            self.color = color

    gardenBird = Bird("Geoffrey", 12)
    gardenBird.birdcall()
    gardenBird.fly()
    sarahThePenguin = Penguin("Sarah", 10)
    sarahThePenguin.swim()
    sarahThePenguin.fly()
    sarahThePenguin.birdcall()
    freddieTheParrot = Parrot("Freddie", 12, "blue")

    print(freddieTheParrot.color)
    freddieTheParrot.fly()
    freddieTheParrot.birdcall()

Mission #72: Ghost Hotel
~~~~~~~~~~~~~~~~~~~~~~~~~~

다음 미션을 수행해 보도록 하자.

.. code-block:: python


    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    import time


    class Building(object):
        def __init__(self, x, y, z, width, height, depth):
            self.x = x
            self.y = y
            self.z = z

            self.width = width
            self.height = height
            self.depth = depth

        def build(self):
            mc.setBlocks(self.x, self.y, self.z,
                         self.x + self.width, self.y + self.height, self.z + self.depth, 4)

            mc.setBlocks(self.x + 1, self.y + 1, self.z + 1,
                         self.x + self.width - 1, self.y + self.height - 1, self.z + self.depth - 1, 0)

            self.buildWindows()
            self.buildDoor()

        def clear(self):
            mc.setBlocks(self.x, self.y, self.z,
                         self.x + self.width, self.y + self.height, self.z + self.depth, 0)

        def buildWindows(self):
            mc.setBlock(self.x + (self.width / 4 * 3), self.y + 2, self.z, 0)
            mc.setBlock(self.x + (self.width / 4), self.y + 2, self.z, 0)

        def buildDoor(self):
            mc.setBlocks(self.x + (self.width / 2), self.y + 1, self.z, self.x + (self.width / 2), self.y + 2, self.z, 0)


    class FancyBuilding(Building):
        def upgrade(self):
            # carpet
            mc.setBlocks(self.x + 1, self.y, self.z + 1,
                         self.x + self.width - 1, self.y, self.z + self.depth - 1,
                         35, 6)

            # flowers
            mc.setBlocks(self.x - 1, self.y, self.z - 1,
                         self.x - 1, self.y, self.z + self.depth + 1,
                         37)
            mc.setBlocks(self.x - 1, self.y, self.z - 1,
                         self.x + self.width + 1, self.y, self.z - 1,
                         37)
            mc.setBlocks(self.x + self.width + 1, self.y, self.z - 1,
                         self.x + self.width + 1, self.y, self.z + self.depth + 1,
                         37)
            mc.setBlocks(self.x - 1, self.y, self.z + self.depth + 1,
                         self.x + self.width + 1, self.y, self.z + self.depth + 1,
                         37)


    pos = mc.player.getTilePos()
    x = pos.x
    y = pos.y
    z = pos.z

    ghostHotel = FancyBuilding(x, y, z, 10, 6, 8)
    ghostHotel.build()
    ghostHotel.upgrade()

    time.sleep(30)

    ghostHotel.clear()



12.8 Overriding Methods and Attributes
-----------------------------------------
subclass에서 superclass에서 정의한 method를 다시 정의할 수 있다.

다음 미션을 수행해 보자.

Mission #73: Ghost Tree
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: python

    import time

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()


    class Building(object):
        def __init__(self, x, y, z, width, height, depth):
            self.x = x
            self.y = y
            self.z = z

            self.width = width
            self.height = height
            self.depth = depth

        def build(self):
            mc.setBlocks(self.x, self.y, self.z,
                         self.x + self.width, self.y + self.height, self.z + self.depth, 4)

            mc.setBlocks(self.x + 1, self.y + 1, self.z + 1,
                         self.x + self.width - 1, self.y + self.height - 1, self.z + self.depth - 1, 0)

            self.buildWindows()
            self.buildDoor()

        def clear(self):
            mc.setBlocks(self.x, self.y, self.z,
                         self.x + self.width, self.y + self.height, self.z + self.depth, 0)

        def buildWindows(self):
            mc.setBlock(self.x + (self.width / 4 * 3), self.y + 2, self.z, 0)
            mc.setBlock(self.x + (self.width / 4), self.y + 2, self.z, 0)

        def buildDoor(self):
            mc.setBlocks(self.x + (self.width / 2), self.y + 1, self.z, self.x + (self.width / 2), self.y + 2, self.z, 0)


    class Tree(Building):
        def build(self):
            """Creates a tree at the coordinates given"""
            wood = 17
            leaves = 18

            # trunk
            mc.setBlocks(self.x, self.y, self.z, self.x, self.y + 5, self.z, wood)

            # leaves
            mc.setBlocks(self.x - 2, self.y + 6, self.z - 2, self.x + 2, self.y + 6, self.z + 2, leaves)
            mc.setBlocks(self.x - 1, self.y + 7, self.z - 1, self.x + 1, self.y + 7, self.z + 1, leaves)

        def clear(self):
            """Clears a tree at the coordinates given"""
            wood = 0
            leaves = 0

            # trunk
            mc.setBlocks(self.x, self.y, self.z, self.x, self.y + 5, self.z, wood)

            # leaves
            mc.setBlocks(self.x - 2, self.y + 6, self.z - 2, self.x + 2, self.y + 6, self.z + 2, leaves)
            mc.setBlocks(self.x - 1, self.y + 7, self.z - 1, self.x + 1, self.y + 7, self.z + 1, leaves)

    pos = mc.player.getTilePos()
    x = pos.x
    y = pos.y
    z = pos.z

    ghostTree = Tree(x, y, z, 10, 6, 8)
    ghostTree.build()

    time.sleep(10)

    ghostTree.clear()




12.9 What You Learned
--------------------------------


object-oriented programming

class and create objects

inheritance


