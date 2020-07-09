---
title: Setting up C++ Makefile Project in Visual Studio
author: ETdoFresh
type: post
date: 2016-08-26T19:28:12+00:00
url: /setting-up-c-makefile-project-in-visual-studio/
categories:
  - Programming

---
<img class="alignleft wp-image-289 size-full" src="http://www.etdofresh.com/wp-content/uploads/2016/08/vsicon.png" alt="vsicon" width="30" height="32" />For my computer graphics course, I have to submit all my projects using C++, compiled using g++ and a Makefile.

If you don't know what a Makefile is, it's basically a list of steps/depencies to get to the final product. For example, to end up with DogSimulator.exe, you will need to run g++ on DogSimulator.o and Dog.o (compiled objects). And the prerequisites to DogSimulator.o and Dog.o are DogSimulator.cpp and Dog.cpp respectively.

It's not too hard in the terminal, because once you have all your files in the terminal, you just type "make" and the magic ensues. But I'm a snob for my Visual Studio IDE, so I am going to set it up there. Haha.<!--more-->

### Step 1 &#8211; Install Software

  * **Visual Studio** (<http://www.visualstudio.com>) 
      * We need an IDE, and the whole reason for this post 🙂
      * Make sure to select C++ when prompted during install

  * **MinGW** (<http://www.mingw.org>) 
      * Nice package that includes G++ and Make
      * Basic Setup: mingw32-gcc-g++
      * All Packages: mingw32-make (bin) and mingw32-pthreads-w32 (dev)
      * Make sure to include C:\MinGW\bin in your environment path.
      * Copy C:\MinGW\bin\mingw32-make.exe to C:\MinGW\bin\make.exe

### Step 2- Create a Visual Studio C++ Makefile Project

[<img class="aligncenter wp-image-290" src="http://www.etdofresh.com/wp-content/uploads/2016/08/vscppstartscreen-300x88.png" alt="vscppstartscreen" width="500" height="146" srcset="http://localhost/wp-content/uploads/2016/08/vscppstartscreen-300x88.png 300w, http://localhost/wp-content/uploads/2016/08/vscppstartscreen-768x225.png 768w, http://localhost/wp-content/uploads/2016/08/vscppstartscreen.png 908w" sizes="(max-width: 500px) 100vw, 500px" />][1]

<img class="alignright wp-image-292 size-medium" src="http://www.etdofresh.com/wp-content/uploads/2016/08/vscppmakesettings-300x235.png" alt="vscppmakesettings" width="300" height="235" srcset="http://localhost/wp-content/uploads/2016/08/vscppmakesettings-300x235.png 300w, http://localhost/wp-content/uploads/2016/08/vscppmakesettings.png 666w" sizes="(max-width: 300px) 100vw, 300px" /> Now we should be able to create a new C++ Makefile project. I'll list two examples below. Regardless of which one you use, use the following settings when creating the project.

  * Build command line: make
  * Clean commands: make clean
  * Rebuild command line: make clean all

### Step 3 &#8211; Simple Hello World Example!

We will create two files: **main.cpp** and **Makefile**

<pre class="lang:c++ decode:true" title="main.cpp">#include &lt;iostream&gt;

using namespace std;

int main(int argc, char* argv[])
{
	cout &lt;&lt; "Hello World!" &lt;&lt; endl;
	cin.get();
	return 0;
}</pre>

<pre class="lang:vim decode:true " title="Makefile">all: HelloWorld

HelloWorld: main.o
	g++ -o HelloWorld main.o

main.o: main.cpp
	g++ -c main.cpp

clean:
	rm *o HelloWorld</pre>

&nbsp;

Just click the Play Button (ie Local Windows Debugger). Hello World should come up!

 [1]: http://www.etdofresh.com/wp-content/uploads/2016/08/vscppstartscreen.png