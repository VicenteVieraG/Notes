# Shaders and Rendering Pipeline
## What is the Rendering Pipeline?

- The rendering pipeline is a series of stages that take place in ordr to render an image to the screen.
- A lot of the rendering pipeline stages are programable via shaders.
- Shaders are pieces of code written in GLSL (OpenGL Shading Language), or HLSL (High-Level Shading Language) if you are using Direct3D.
- GLSL is based on C.

## Rendering Pipeline Stages

1. ### Vertex Specification
    - A vertex is a point in space, usually defined with x, y and z coordinates
    - A primitive is a simple shape defined using one or more vertices
    - Usually we use triangles, but we can also use points, lines, and quads.
    - #### Setting up the data of the vertices for the primitives we want ro render.
        1. Done in the application itself
        2. Uses VAOs (Vertes Array Objects) and VBOs (Vertex Buffer Objects)
        3. VBO defines the data itself
        4. Attribute Pointers define where and how shaders can access vertex data.
    - #### Creating VAO/VBO
        1. Generate a VAO ID
        2. Bind the VAO with that ID
        3. Generate a VBO ID
        4. Bind the VBO with that ID (now you're working on the chosen VBO attached to the chosen VAO)
        5. Attach the vertx data to that VBO
        6. Define the Attribute Pointer formatting
        7. Enable the Attribute Pointer
        8. Unbind the VAO and VBO, ready for the next object to be bound.
    - #### Initiating Draw
        1. Activate Shader Program you want to use
        2. Bind VAO of object you wanto to draw
        3. Call `glDrawArrays`, wich initiates the rest of the pipeline.
2. ### Vertex Shader (Programmable)
    - Handles vertices individually
    - NOT optional
    - Must store somethig in `gl_Position` as it is used by later stages
    - Can specify additional outputs that can be picked up and used by user-defined shaders later in pipeline
    - Inputs consist of the vertes date itself.
    - Vertex Shader simple example:
        ```GLSL
        #version 330

        lauout (location = 0) in vec3 pos;

        void main(){
            gl_position = vec4(pos, 1.0);
        }
        ```
3. ### Tessellation (Programmable)
    - Allows you to divide up data into smaller primitives
    - Relatively new shader type. Appeared in OpenGL 4.0
    - Can be used to add higher levels of detail dynamically.
4. ### Geometry Shader (Programmable)
    - Vertex Shader handles vertices, Geometry Shader handles primitives (groups og primitives)
    - Takes primitives then “emits” their vertices to create the given primitive, or even new primitives
    - Can alter data given to it to modify given primitives, or even create new ones
    - Can eve alter the primitive types (points, lines, triangles, etc).
6. ### Vertex Post-Processing
   - #### Transforms Feedback (if enabled):
     - Result of Vertex and Geometry stages saved to buffers for later use
   - #### Clipping:
     - Primitives that won't be visible are removed (don't want to draw things we can't see!)
     - Positions converted from “clip-space” to “window space”.
7. ### Primitive Assembly
   - Vertices are converted into a series of primitives
   - So, if rendering triangles… 6 vertices would become 2 triangles (3 vertices each)
   - Face culling.
   - Face culling is the removal of primitives that can not be seen, or are facing “away” from the viewer. We don't want to draw something if can't see it!
8. ### Rasterizarion
   - Converts primitives in to “Fragments”
   - Fragmentes are pieces of data for each pixel obtaind from the rasterization process
   - Fragment data will ve interpolated vased on its position relative to each vertex.
9.  ### Fragment Shader (Programmable)
    - Handles data for each fragment
    - Is optional but, it's rare to not use it. Exeptions are cases where noly depth or stencil data is required
    - Most important output is the colour of the pixel that the fragment covers
    - Simplest OpenGL programs usually have a Vertex Shader and a Fragment Shader.
    - Example of Fragment Shader:
        ```GLSL
        #version 330

        out vec4 colour;

        void main(){
            colour = vec4(1.0, 0.0, 0.0, 1.0);
        }
        ```
10. ### Per-Sample operations.
    - Series of test run to see if the gragment should ve drawn
    - #### Most important test: Depth test
      - Determines if something is in front of the point being drawn
    - #### Colour Blending:
      - Using defined operations, fragment solours are “blended” together with overlapping fragments. Usually used to handle transparent objects
      - Fragment data written to currently bound Frambuffer (usually the default buffer)
      - Lastly, inte application code the user usally defines a buffer swap here, puttng the newly updated Framebuffer to the front
      - The pipeline is complete!