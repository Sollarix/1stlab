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

**glClear(GL_COLOR_BUFFER_BIT)** - sets the bitplane area of the window to values previously selected by glClearColor to clear buffer.

**glutSwapBuffers()** - performs a buffer swap on the layer in use for the current window.

# Draw point/triangle

**GLenum res = glewInit()** - initializes Glew Library, which is suppose to provide efficient run-time mechanisms for determining which OpenGL extensions are supported on target plaform. Also, we need to define Glew after defining Glut.

**if (res != GLEW_OK) {...}** - here we check correction of our Glew definition.

**glm::vec3 Vertices[1/3] = {...}** - here we define array of 2D point/points that will be used to draw on our graphic window.

**GLuint VBO** - we will assign GLuint as a global variable to store a pointer to the vertex buffer.

**glGenBuffers(1, &VBO)** - function to generate objects of variable types. Most often they take 2 parameters: the first defines the number of objects you want to create, and the second is a reference to an array of type GLuints to store the pointer at which the data will be stored.

**glBindBuffer(GL_ARRAY_BUFFER, VBO)** - we bind the pointer to the name of the target and then run the command on the target. These commands restrict changes to a value by a pointer until another one is restricted instead, or the call accepts 0 as the pointer. The GL_ARRAY_BUFFER parameter means that the buffer will store an array of vertices. You can specify another parameter GL_ELEMENT_ARRAY_BUFFER it indicates that the vertex indices are stored in a different buffer.

**glBufferData(GL_ARRAY_BUFFER, sizeof(Vertices), Vertices, GL_STATIC_DRAW)** - after binding our object, we fill it with data. Calling this function takes the name of the target (same as when binding), the size of the data in bytes, the address of the array of vertices, and a flag that indicates the use of patterns for this data. Since we are not going to change the buffer values, we specify GL_STATIC_DRAW. Its opposite is GL_DYNAMIC_DRAW.

### Some additions in RenderSceneCB
    
**glEnableVertexAttribArray(0)** - we must enable per-vertex attribute indexing. We don't use shaders yet in this lab, but the vertex coordinates used in the buffer are treated as an attribute of the vertex at index 0 in the fixed pipeline function (which becomes active if no shader is used). It is necessary to allow each vertex attribute to be used, otherwise they will not be available in the pipeline.

**glVertexAttribPointer(0, 3, GL_FLOAT, GL_FALSE, 0, 0)** - this call tells the pipeline how to accept the data inside the buffer. The first parameter specifies the index of the attribute. In our case, we know that this is 0 by default, but when we start using shaders, we will need to specify either explicitly specify indexes or queries for them. The second parameter is the number of components in the attribute (3 for X, Y and Z). The third parameter is the data type for each component. The next one is whether we want to normalize the attributes before using them in the pipeline. In our case, we want the data to be transmitted not named. The fifth parameter (named "step") is the number of bytes between 2 instances of the attribute. The last parameter specifies the offset in the structure that our pipeline will receive.

**glDrawArrays(GL_TRIANGLES, 0, 3)** - draws what we want, in this case GL_TRIANGLES, it uses more simple sequential drawing, unlike with indexed drawing same vertices cannot be reused without typing them multiple times, which is a waste of memory. 0 - means that we start at the first vertex, 3 - means that we will use 3 vertices.
