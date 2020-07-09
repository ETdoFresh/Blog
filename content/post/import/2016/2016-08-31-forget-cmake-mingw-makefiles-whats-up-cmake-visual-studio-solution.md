---
title: Forget MinGW Makefiles… What’s up Visual Studio?
author: ETdoFresh
type: post
date: 2016-09-01T00:04:39+00:00
url: /forget-cmake-mingw-makefiles-whats-up-cmake-visual-studio-solution/
categories:
  - Programming

---
[<img class="aligncenter wp-image-353" src="http://www.etdofresh.com/wp-content/uploads/2016/08/CSCI5631-SmallVictory-300x162.png" alt="CSCI5631-SmallVictory" width="601" height="325" srcset="http://localhost/wp-content/uploads/2016/08/CSCI5631-SmallVictory-300x162.png 300w, http://localhost/wp-content/uploads/2016/08/CSCI5631-SmallVictory-768x416.png 768w, http://localhost/wp-content/uploads/2016/08/CSCI5631-SmallVictory-1024x554.png 1024w, http://localhost/wp-content/uploads/2016/08/CSCI5631-SmallVictory-1200x649.png 1200w, http://localhost/wp-content/uploads/2016/08/CSCI5631-SmallVictory.png 1920w" sizes="(max-width: 601px) 100vw, 601px" />][1]Hours.... literally a handful of hours trying to setup MinGW for my class projects. Yeah, MinGW was kicking my butt... I just threw my hands up, waved the white flag, and gave up. You may have saw in the [last post][2] that we did get Freeglut working... but once it came to glew32, it all came unglued.<!--more-->

So yeah, here we go again. Nice and fresh. I download the [source for glew][3] and [source for freeglut][4]. I used [Cmake][5] and Visual Studio 2015 to compile the libraries (dynamic and static/debug and release). I'll include them here for convenience's sake.

  * [freeglut-3.0.0-compiled-with-vs2015][6]
  * [glew-2.0.0-compiled-with-vs2015][7]
  * _These are not needed for tutorial below_

[<img class="aligncenter wp-image-355" src="http://www.etdofresh.com/wp-content/uploads/2016/08/vscppempty01-300x209.png" alt="vscppempty01" width="450" height="313" srcset="http://localhost/wp-content/uploads/2016/08/vscppempty01-300x209.png 300w, http://localhost/wp-content/uploads/2016/08/vscppempty01-768x535.png 768w, http://localhost/wp-content/uploads/2016/08/vscppempty01.png 939w" sizes="(max-width: 450px) 100vw, 450px" />][8]Great! So how do we use this? Well, let's start from scratch... Let's make an empty Visual Studio Project.

Let's make a simple file main.cpp file to make sure we are up and running.

<pre class="lang:c++ decode:true" title="main.cpp">int main(int argc, char* argv[])
{
	return 0;
}</pre>

[<img class="aligncenter size-medium wp-image-356" src="http://www.etdofresh.com/wp-content/uploads/2016/08/vscppempty02-300x18.png" alt="vscppempty02" width="300" height="18" srcset="http://localhost/wp-content/uploads/2016/08/vscppempty02-300x18.png 300w, http://localhost/wp-content/uploads/2016/08/vscppempty02.png 373w" sizes="(max-width: 300px) 100vw, 300px" />][9]Press F6 or from the menu Build > Build Solution. You should see Build Succeeded. Now let's add some libraries and get into the knitty gritty.

First thing to understand is static vs dynamic libraries. Simply put, **static** libraries are compiled into the exe whereas **dynamic** libraries exist outside the exe as dll files. In this post, I'll deal exclusively with dynamic libraries.

Download and extract my [Visual Studio 2015 Dynamic Freeglut and Glew32 zip file][10] into your Project directory (with main.cpp). Now we have to setup the dependencies and other settings on the project itself. So go to the Project's Properties (Right click Project and click Properties).

[<img class="aligncenter wp-image-358" src="http://www.etdofresh.com/wp-content/uploads/2016/08/vscppempty03-300x214.png" alt="vscppempty03" width="450" height="321" srcset="http://localhost/wp-content/uploads/2016/08/vscppempty03-300x214.png 300w, http://localhost/wp-content/uploads/2016/08/vscppempty03-768x549.png 768w, http://localhost/wp-content/uploads/2016/08/vscppempty03.png 840w" sizes="(max-width: 450px) 100vw, 450px" />][11]

First, we want to make sure we are including headers in our include folder. Select **ALL CONFIGURATIONS**. Under C/C++ > General > Additional Include Directories, add **include**.

[<img class="aligncenter wp-image-359" src="http://www.etdofresh.com/wp-content/uploads/2016/08/vscppempty04-300x215.png" alt="vscppempty04" width="450" height="322" srcset="http://localhost/wp-content/uploads/2016/08/vscppempty04-300x215.png 300w, http://localhost/wp-content/uploads/2016/08/vscppempty04-768x549.png 768w, http://localhost/wp-content/uploads/2016/08/vscppempty04.png 847w" sizes="(max-width: 450px) 100vw, 450px" />][12]

The code that we will be dealing with, we need to set a preprocessor flag, so here we add at the beginning \_CRT\_SECURE\_NO\_WARNINGS;

[<img class="aligncenter wp-image-360" src="http://www.etdofresh.com/wp-content/uploads/2016/08/vscppempty05-300x214.png" alt="vscppempty05" width="450" height="321" srcset="http://localhost/wp-content/uploads/2016/08/vscppempty05-300x214.png 300w, http://localhost/wp-content/uploads/2016/08/vscppempty05-768x547.png 768w, http://localhost/wp-content/uploads/2016/08/vscppempty05.png 846w" sizes="(max-width: 450px) 100vw, 450px" />][13]

Let's include our freeglut and glew32 libraries. We add both the release and debug version of the library in all configuration for ease.

[<img class="aligncenter wp-image-361" src="http://www.etdofresh.com/wp-content/uploads/2016/08/vscppempty06-300x116.png" alt="vscppempty06" width="825" height="320" srcset="http://localhost/wp-content/uploads/2016/08/vscppempty06-300x116.png 300w, http://localhost/wp-content/uploads/2016/08/vscppempty06-768x298.png 768w, http://localhost/wp-content/uploads/2016/08/vscppempty06-1024x397.png 1024w, http://localhost/wp-content/uploads/2016/08/vscppempty06-1200x465.png 1200w, http://localhost/wp-content/uploads/2016/08/vscppempty06.png 1560w" sizes="(max-width: 825px) 100vw, 825px" />][14]

Finally, we do a little Post-Build scripting to copy over the DLLs and Shaders from our project directory to our output directory. xcopy /d /y silently copies over the file only if newer. Notice we have a different copy statement between Debug and Release since we want to copy over the different DLLs.

OK. We're done! Here's an example using these libraries and settings. [Check out this visual studio solution (Project1.zip)][15]!

PS – _I used a slightly different folder structure than the tutorial, but everything else is the same._

 [1]: http://www.etdofresh.com/wp-content/uploads/2016/08/CSCI5631-SmallVictory.png
 [2]: http://www.etdofresh.com/add-freeglut-to-mingw/
 [3]: http://glew.sourceforge.net/
 [4]: http://freeglut.sourceforge.net/
 [5]: https://cmake.org/
 [6]: http://www.etdofresh.com/wp-content/uploads/2016/08/freeglut-3.0.0-compiled-with-vs2015.zip
 [7]: http://www.etdofresh.com/wp-content/uploads/2016/08/glew-2.0.0-compiled-with-vs2015.zip
 [8]: http://www.etdofresh.com/wp-content/uploads/2016/08/vscppempty01.png
 [9]: http://www.etdofresh.com/wp-content/uploads/2016/08/vscppempty02.png
 [10]: http://www.etdofresh.com/wp-content/uploads/2016/08/vs2015includeDynamicFreeglutGlew32.zip
 [11]: http://www.etdofresh.com/wp-content/uploads/2016/08/vscppempty03.png
 [12]: http://www.etdofresh.com/wp-content/uploads/2016/08/vscppempty04.png
 [13]: http://www.etdofresh.com/wp-content/uploads/2016/08/vscppempty05.png
 [14]: http://www.etdofresh.com/wp-content/uploads/2016/08/vscppempty06.png
 [15]: http://www.etdofresh.com/wp-content/uploads/2016/08/Project1.zip