---
title: Add Freeglut to MinGW
author: ETdoFresh
type: post
date: 2016-08-30T17:53:42+00:00
url: /add-freeglut-to-mingw/
categories:
  - Programming

---
More setup! Joy!

After setting up MinGW from our [previous post][1], now we want to add a package called freeglut to our MinGW directory so we can some graphics to our programs.

  * Download freeglut for MinGW from (<http://www.transmissionzero.co.uk/computing/using-glut-with-mingw/>)
  * Copy the contents into C:\MinGW (or wherever you installed MinGW)

OK! Done!<!--more-->

Let's try a sample program:

<pre class="lang:c++ decode:true " title="GL01Hello.cpp">/*
 * GL01Hello.cpp: Test OpenGL C/C++ Setup
 */
#include &lt;windows.h&gt;  // For MS Windows
#include &lt;GL/glut.h&gt;  // GLUT, includes glu.h and gl.h
 
/* Handler for window-repaint event. Call back when the window first appears and
   whenever the window needs to be re-painted. */
void display() {
   glClearColor(0.0f, 0.0f, 0.0f, 1.0f); // Set background color to black and opaque
   glClear(GL_COLOR_BUFFER_BIT);         // Clear the color buffer
 
   // Draw a Red 1x1 Square centered at origin
   glBegin(GL_QUADS);              // Each set of 4 vertices form a quad
      glColor3f(1.0f, 0.0f, 0.0f); // Red
      glVertex2f(-0.5f, -0.5f);    // x, y
      glVertex2f( 0.5f, -0.5f);
      glVertex2f( 0.5f,  0.5f);
      glVertex2f(-0.5f,  0.5f);
   glEnd();
 
   glFlush();  // Render now
}
 
/* Main function: GLUT runs as a console application starting at main()  */
int main(int argc, char** argv) {
   glutInit(&argc, argv);                 // Initialize GLUT
   glutCreateWindow("OpenGL Setup Test"); // Create a window with the given title
   glutInitWindowSize(320, 320);   // Set the window's initial width & height
   glutInitWindowPosition(50, 50); // Position the window's initial top-left corner
   glutDisplayFunc(display); // Register display callback handler for window re-paint
   glutMainLoop();           // Enter the infinitely event-processing loop
   return 0;
}</pre>

Then let's compile it.

<pre class="lang:default decode:true" title="Command Line">g++ GL01Hello.cpp -o GL01Hello.exe -lopengl32 -lfreeglut</pre>

 [1]: http://www.etdofresh.com/setting-up-c-makefile-project-in-visual-studio/