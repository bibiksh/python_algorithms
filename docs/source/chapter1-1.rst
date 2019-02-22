chapter 1: Setting Up for Your Adventure
============================================


1.1 Setting Up Your Windows PC
----------------------------------
Install Python
~~~~~~~~~~~~~~~

python을  다음 사이트에서 받는다.

https://www.python.org/downloads/windows/

인스톨을 특정 디렉토리에 인스톨한다.

.. code-block:: python

    D:\SEANLAB\PYTHON\Python3.7\Lib\site-packages\mcpi\minecraft.py


그리고 윈도우 시스템 설정에서 path를 잡아 준다.



one drive에서 다음 경로로 가면 MinecraftPythonAPI.zip
인스톨 한다.

.. code-block:: python

    D:\OneDrive\OneDrive_4619\OneDrive - leverage innovative users\devtools\minecraft



minecraft.py 화일을 열어

.. code-block:: python

    @staticmethod
    def create(address = "localhost", port = 4711):
    return Minecraft(Connection(address, port))

다음과 같이 변경한다.

.. code-block:: python

    @staticmethod
    def create(address = "192.168.30.9", port = 4711):
    return Minecraft(Connection(address, port))



Install JDK
~~~~~~~~~~~~~~~~~

다음 사이트에서 받는다.

http://www.java.com/en/download/



윈도우 시스템 변수에
JAVA_HOME  C:\Program Files\Java\jdk1.8.0_151
그리고 path 변수에

.. code-block:: python

    C:\Program Files\Java\jdk1.8.0_151\bin


를 넣는다.


Install Eclipse
~~~~~~~~~~~~~~~~~

다음 사이트에서 받는다.

http://www.eclipse.org

인스톨 후 실행 시킨후
Help-Eclipse Market Place에서
Pydev를 찾아서 인스톨 한다.


1.2 Setting Up Your Mac
---------------------------

skip this sub chapter..


1.3 Setting Up Your Raspberry Pi
-----------------------------------

skip this sub chapter..


1.4 Getting to Know IDLE
------------------------------

IDLE에 다음 코드를 입력해 보자


.. code-block:: python

    from mcpi.minecraft import Minecraft
    from mcpi import block
    mc = Minecraft.create()
    mc.postToChat("test")

    mc.postToChat(4+5)


    mc.postToChat(178+234)





1.5 Testing Your Minecraft Python Setup
------------------------------------------



1.6 Python이란
------------------------------------------
Interpreter,no compile
~~~~~~~~~~~~~~~~~~~~~~~~~~
Python is a high-level programming language, with applications in numerous areas, including web programming,
scripting, scientific computing, and artificial intelligence.
It is very popular and used by organizations such as Google, NASA, the CIA, and Disney.
Python is processed at runtime by the interpreter.
There is no need to compile your program before executing it.


Python 3.X,CPython
~~~~~~~~~~~~~~~~~~~~~~~~
The three major versions of Python are 1.x, 2.x and 3.x. These are subdivided into minor versions, such as 2.7 and 3.3.
Code written for Python 3.x is guaranteed to work in all future versions.
Both Python Version 2.x and 3.x are used currently.
This course covers Python 3.x, but it isn't hard to change from one version to another.

Python has several different implementations, written in various languages.
The version used in this course, CPython, is the most popular by far.

print("Hello world!")
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Let's start off by creating a short program that displays "Hello world!".
In Python, we use the print statement to output text:

print('Hello world!')
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

