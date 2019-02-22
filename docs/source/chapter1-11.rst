chapter 11: Saving and Loading Buildings with  Files and Modules
===================================================================

이 장에서는 데이터를 저장하는 파일에 대해서 배워보도록 하겠다.



11.1 Using Files
-------------------

Opening a File
~~~~~~~~~~~~~~~~~
파일은 다음 형식으로 열고 닫는다.

.. code-block:: python

    secretFile = open("secretFile.txt", "w")

w는 쓰기전용이다.
r  읽기전용
r+  읽기+쓰기
a    추가


Writing to and Saving a File
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
파일을 열어서 쓰고 저장은 다음처럼 한다.

.. code-block:: python


    secretFile = open("secretFile.txt", "w")
    secretFile.write("This is a secret file. Shhh! Don't tell anyone.")
    secretFile.close()


Reading a File
~~~~~~~~~~~~~~~~~~~
파일은 다음처럼 읽는다.

.. code-block:: python


    secretFile = open("secretfile.txt", "r")
    print(secretFile.read())
    secretFile.close()


Reading a Line of a File
~~~~~~~~~~~~~~~~~~~~~~~~~~~

readline() function 을 사용하면 한줄씩 읽게 된다.

예를 들어 파일에
"Cool\nDance\nParty"
로 되어 있으면
Cool
Dance
Party

이런식으로 읽히게 된다.


Mission #64: To-Do List
~~~~~~~~~~~~~~~~~~~~~~~~~~~





11.2 Using Modules
-------------------

toDoList.txt

.. code-block:: python

    Test
    test
    test


파일에 입력을 하고


.. code-block:: python



    toDoFile = open("toDoList.txt", "w")

    toDoList = ""

    toDoItem = input("Enter a to do list item: ")

    while toDoItem != "exit":
        toDoList = toDoList + toDoItem + " \n"
        toDoItem = input("Enter a to do list item: ")

    toDoFile.write(toDoList)
    toDoFile.close()

그 화일을 읽는 연습이다.

.. code-block:: python

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    toDoList = open("toDoList.txt", "r")

    for line in toDoList:
        mc.postToChat(line)

Using Modules
~~~~~~~~~~~~~~~~
Modules are collections of functions

Python standard library


The pickle Module
~~~~~~~~~~~~~~~~~~~

다음처럼 사용한다.

.. code-block:: python


    import pickle
    locations = {'John': 'Forest', 'Phillipa': 'Mountains', 'Pete': 'City'}
    secretFile= open("secretFile.txt", "wb")
    pickle.dump(locations, secretFile)

    import pickle
    secretFile= open("secretFile.txt", "rb")
    locations = pickle.load(secretFile)


Importing One Function with the from Clause
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

모듈에서 함수 하나만을 쓸수 있다.

.. code-block:: python

    from pickle import dump
    locations = {'John': 'Forest', 'Phillipa': 'Mountains', 'Pete': 'City'}
    secretFile= open("secretFile", "wb")
    dump(locations, secretFile)

    from pickle import dump, load
    locations = {'John': 'Forest', 'Phillipa': 'Mountains', 'Pete': 'City'}
    secretFile= open("secretFile", "wb")
    dump(locations, secretFile)
    locations = load(secretFile)
    print(locations['Phillipa'])

Importing All Functions with *
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
*를 사용하면 모든 함수를 로딩하게 된다.
*를 쓰면 편하긴 한데 여러 모듈을 한꺼번에 쓰면 동일 함수명을 쓰는것에 충돌을 가져올 수 있다.
그래서 *를 지양하고 특정 함수를 쓰는것을 권장한다.
모듈내 함수가 어떤것인지 몰라 테스트용으로 쓸때 권장한다.

Giving a Module a Nickname
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

모듈을 로딩해서 특정 이름으로 할당할 수 있다.

.. code-block:: python


    import pickle as p
    p.dump(locations, secretFile)

Mission #65: Save a Building
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

한쪽맵에서 빌딩을 저장한 파일을 다른쪽에 옮기는 미션이다.

Part 1: Saving the Building
~~~~~~~~~~~~~~~~~~~~~~~~~~~

다음 코드를 실행해 보자.

.. code-block:: python

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    import pickle


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
                    block = mc.getBlockWithData(x1 + column, y1 + row, z1 + depth)
                    structure[row][column].append(block)

        return structure

    input("Move to the first position and press ENTER in this window")
    pos1 = mc.player.getTilePos()

    # get the position of the first corner
    x1 = pos1.x
    y1 = pos1.y
    z1 = pos1.z

    input("Move to the opposite corner and press ENTER in this window")
    pos2 = mc.player.getTilePos()

    # get the position of the second corner
    x2 = pos2.x
    y2 = pos2.y
    z2 = pos2.z

    structure = copyStructure(x1, y1, z1, x2, y2, z2)

    # store the structure in a file
    pickleFile = open("pickleFile", "wb")
    pickle.dump(structure, pickleFile)


Part 2: Loading the Building
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
다음 코드를 실행해 보자.

.. code-block:: python

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    import pickle


    def buildStructure(x, y, z, structure):
        xStart = x
        zStart = z
        for row in structure:
            for column in row:
                for block in column:
                    mc.setBlock(x, y, z, block.id, block.data)
                    z += 1
                x += 1
                z = zStart
            y += 1
            x = xStart


    pickleFile = open("pickleFile", "rb")
    structure = pickle.load(pickleFile)
    pos = mc.player.getTilePos()
    x = pos.x
    y = pos.y
    z = pos.z

    buildStructure(x, y, z, structure)


건물을 다시 만드는 코드이다.



11.3 Storing Lots of Data with the shelve Module
----------------------------------------------------

pickle은 한번에 한 데이터만 저장할 수 있지만 어떤 프로그램들은 여러 종류의 변수를 넣을 필요가 있다.
여러 데이터를 쓰게 되면 각각 파일을 만들어야 되고 관리도 복잡해지고 힘들다.
파이썬에서는 shelve 모듈을 제공한다.
이것은 한 파일에 여러개의 데이터를 저장할때 쓰인다.

import shelve
    shelveFile = shelve.open("locationsFile.db")

Opening a File with shelve
~~~~~~~~~~~~~~~~~~~~~~~~~~~~
사용법은 다음과 같다.

.. code-block:: python

    import shelve
    shelveFile = shelve.open("locationsFile.db")

Adding, Modifying, and Accessing Items with shelve
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
수정은 다음과 같이 한다.

.. code-block:: python


    import shelve
    shelveFile = shelve.open("locationsFile.db")
    shelveFile['Beatrice'] = 'Submarine'
    shelveFile.close()

Mission #66: Save a Collection of Structures
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

이전에 저장했던 데이터를 pickle 말고 shelve로 저장하는 미션이다.


Part 1: Saving a Structure to a Collection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

저장했던 파일을 collection어 넣어 보도록 하자.

다음 코드를 실행해 보자.

.. code-block:: python

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    import shelve


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
                    block = mc.getBlockWithData(x1 + column, y1 + row, z1 + depth)
                    structure[row][column].append(block)

        return structure

    input("Move to the first position and press ENTER in this window")
    pos1 = mc.player.getTilePos()

    # get the position of the first corner
    x1 = pos1.x
    y1 = pos1.y
    z1 = pos1.z

    input("Move to the opposite corner and press ENTER in this window")
    pos2 = mc.player.getTilePos()

    # get the position of the second corner
    x2 = pos2.x
    y2 = pos2.y
    z2 = pos2.z

    structure = copyStructure(x1, y1, z1, x2, y2, z2)

    # name the structure
    structureName = input('What do you want to call the structure? ')

    # store the structure in a file
    shelveFile = shelve.open("shelveFile.db")
    shelveFile[structureName] = structure
    shelveFile.close()


Part 2: Loading a Structure from a Collection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

다음 코드를 실행해 보자.

.. code-block:: python

    from mcpi.minecraft import Minecraft
    mc = Minecraft.create()

    import shelve


    def buildStructure(x, y, z, structure):
        xStart = x
        zStart = z
        for row in structure:
            for column in row:
                for block in column:
                    mc.setBlock(x, y, z, block.id, block.data)
                    z += 1
                x += 1
                z = zStart
            y += 1
            x = xStart


    structureDictionary = shelve.open("shelveFile.db")

    structureName = input("Enter the structure's name ")

    pos = mc.player.getTilePos()
    x = pos.x
    y = pos.y
    z = pos.z

    buildStructure(x, y, z, structureDictionary[structureName])




11.4 Installing New Modules with pip
----------------------------------------------------
파이썬은 기본 모듈 이외에도 많은 모듈들이 존재한다.
기본적으로 pip을 이용해서 이런 모듈을 인스톨 한다.
최근의 python 3버젼은 pip이 내장되어 있다.
없는 경우는 pip 모듈을 인스톨 해야 한다.

사용법은 다음과 같다.

.. code-block:: python

    pip install Flask




11.5 Using a Module from pip: Flask
----------------------------------------------------

다음 코드를 실행해 보자.
간단한 웹서버를 구성해 보자.


.. code-block:: python

    from flask import Flask
    app = Flask(__name__)
    @app.route("/")
    def showName():
        return "Craig Richardson"
    app.run()

Mission #67: Position Website
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

player의 위치를 Flask 웹 페이지에 뿌려주는 프로그램이다.

skip this contents








11.6 What You Learned
----------------------------------------------------

how to read and write to files using Python’s standard library

giving you control over files when you create your own programs.

use modules, which extend Python’s capabilities

