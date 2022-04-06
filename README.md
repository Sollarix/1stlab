# Change color of graphic window
**glutInit(&argc, argv)** - is a function that initializes our GLUT Library.

**glutInitDisplayMode(GLUT_DOUBLE | GLUT_RGBA)** - here we define some GLUT options. GLUT_DOUBLE define double buffering and GLUT_RGBA define color buffer.

**glutInitWindowSize(800, 600)** - here we define size of our windows which will be used to draw our graphics.

**glutInitWindowPosition(200, 50)** - define position of our window.

**glutCreateWindow("Tutorial 01")** - define name of our window.

**glutDisplayFunc(RenderSceneCB)** - here we started working in the window system and call function RenderSceneCB that performs operations in this window.

**glutMainLoop()** - this function is necessary so that our window is displayed until we turn it off ourselves.

### Now we gonna look at RenderSceneCB
**glClearColor(0.0f, 0.0f, 0.0f, 0.0f)** - specifies the color and alpha values used by glClear to clear the color buffers.

**glClear(GL_COLOR_BUFFER_BIT)** - sets the bitplane area of the window to values previously selected by glClearColor.

**glutSwapBuffers()** - performs a buffer swap on the layer in use for the current window.

# Draw point
