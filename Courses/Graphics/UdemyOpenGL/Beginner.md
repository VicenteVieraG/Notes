# Section 2: Beginner
## What is GLEW
- OpenGL Extension Wrangler
- Interface for OpenGL versions above 1.1
- Load OpenGL extensions

## Usig GLEW
- #include <GL/glew.h>
- After initialisation OpenGL context:
  - glewExperimental = GL_TRUE;
  - > This allows to acces more advanded GLEW methods
- Initialise GLEW:
  - glewInit();
- Validate if GLEW inited correctly:
  - glewGetErrorString(result);
- Check if extensions exists:
  - if(!GLEW_EXT_famebuffer object){}
- wglew.h used for Windows only functions

## What is GLWF
- Stands for OpenGL FrameWork (probably… The real meaning got lost in history)
- It is used to create windows and control.
- Creates OpenGL context.
- Handle inputs.

## What is SDL
- Simple DirectMedia Layer
- This is GLFW in steroids. Handles audiom threading, filesystems, everythig that GLFW can do and more.

## SFML
- Simple and Fast Multimedia Library.
- Like SDL but with more features.
- The OpenGL context provided is very weak. It is only based on 2D graphics.

## GLUT
- OpenGL Utility Toolkit
- Is no longer maintained.
- The less you use it, the best.

## Win32
- For the purists.
- The lowest level for window creation.
- All the windows creators listed here probably use Win32 under the hood.
- Insanely vervose.
- Not worth of learning nowadays.