# opengl-toolbox

The purpose of this organization is as follows:

* To store a collection of repositories which use eachother to build up a nice abstraction layer over opengl.
* To stop writing the same code, and doing it in a slightly different way each time, but rather improve the quality of existing code.
* Since writing C++ code is relatively lower level when compared to game engines, it's important to modularize to reduce cognitive load.
* To store minimal working examples of opengl code
* Most of the content will be taloired for game development so there will be examples of sound, physics, etc...

Anyone is welcome to contribute

# Sub Projects
Anything denoted by SUBPROJECT is a repository of files, which probably will not work on it's own, but is to be used in a larger application, so far we have the following:

### Interaction
* [input snapshot](https://github.com/opengl-toolbox/input_snapshot)
* [window](https://github.com/opengl-toolbox/window)
* [mouse](https://github.com/opengl-toolbox/mouse)
* [camera](https://github.com/opengl-toolbox/camera)
* [physics](https://github.com/opengl-toolbox/physics)

### Graphics
* [glad3.3](https://github.com/opengl-toolbox/glad_opengl_3.3_core)
* [render primitives](https://github.com/opengl-toolbox/render_primitives)
* [shaders](https://github.com/opengl-toolbox/shaders)
* [shader pipeline](https://github.com/opengl-toolbox/shader_pipeline)
* [model loading](https://github.com/opengl-toolbox/model_loading)
* [font rendering](https://github.com/opengl-toolbox/font_rendering)

### Sound
* [sound system](https://github.com/opengl-toolbox/sound_system)


### Misc.
* [math](https://github.com/opengl-toolbox/math)
* [game loop](https://github.com/opengl-toolbox/game_loop)
* [organizational tools](https://github.com/opengl-toolbox/organizational_tools)
* [stopwatch](https://github.com/opengl-toolbox/stopwatch)

# Minimal Working Examples
Along with these SUBPROJECTS we also have some minimally working examples that use the subprojects:
* [mwe glfw](https://github.com/opengl-toolbox/mwe_glfw) - glfw window using opengl
* [mwe shader pipeline](https://github.com/opengl-toolbox/mwe_shader_pipeline) - exmaple usage on how to use the shader pipeline
* [mwe model loading](https://github.com/opengl-toolbox/mwe_model_loading) - model loading with noclip 3d character controller
* [mwe font rendering](https://github.com/opengl-toolbox/mwe_font_rendering) - demonstrates font rendering with freetype fonts
* [mwe physics world with character](https://github.com/opengl-toolbox/mwe_physics_world_with_character) - demonstrates a 3d world with a character that can be controlled with mouse and keyboard (Jolt Physics)
* [mwe sound world with character](https://github.com/opengl-toolbox/mwe_sound_world_with_character) - demonstrates a 3d world with positional sound with a character which can be controleld with mouse and keyboard (openal)
* [mwe networking](https://github.com/opengl-toolbox/mwe_networking) - basic network setup with enet


# Creating New Subprojects
Use this as a `readme.md` template to let people know what external libraries the subproject depeds on and how to set up the cmake file: 

````

# Info

...

# Depdendencies

...

# CMake

```
...

include_directories(TODO_FILL_IN)
add_subdirectory(TODO_FILL_IN)

... 

target_link_libraries(your_project_name ... TODO_FILL_IN)
```
````

