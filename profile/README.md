# cpp-toolbox

The purpose of this organization is as follows:

* To store a collection of repositories which use eachother to build up more complex programs. This is so that we stop writing same code, and doing it in a slightly different way each time, but rather improve the quality of existing code.
* Since writing C++ code is relatively lower level when compared to other modern languages it's important to modularize in this way to reduce cognitive load.
* Most of the content will be taloired for game development so there will be examples of sound, physics, etc...
* Make sure all code runs on windows, mac and linux, with an emphasis on linux first as anyone can install linux, but not everyone can afford windows or mac.

Anyone is welcome to contribute

# Projects
All projects use submodules to facilitate the integration of subprojects, subprojects need to be setup to link to eachother using `sbpt`, for managing external libraries we use `conan` so install it on your system and follow their docs for preliminary setup on how to generate a profile before you run any conan commands.

```
# get all subproject content
cd project
git submodule update --init --recursive

# generate dynamic includes to linked subprojects
cd sbpt
python sbpt initialize ../src

# install required packages
conan install . --build=missing

# generate build system and then build
cmake --preset conan-release
cmake --build --preset conan-release

cd build/Release
# now run the executable
```

From there run the executable, note that if you try running the executable from anywhere else it will probably fail because it depends on paths of resources being relative to this folder, which may be fixed in the future. 

If you are looking to develop existing code, note that we use a consistent style guide to keep things organized, we use `clang-format` for this, to populate the project with the correct settings, go to the root of the project and do:
```
cd clang_formatting
./create_symlinks.sh
```

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
* [mwe networked physics world with character](https://github.com/opengl-toolbox/mwe_networked_physics_world_with_character)- demonstrates a multi-threaded client-server network model using enet, supports connections and renders other players on the map

# sbpt

When subprojects use other subprojects you usually have to hard-code includes to those locations which differ based on file structure, therefore [`sbpt`](https://github.com/cpp-toolbox/sbpt) was created to fix this issue.

# Creating New Subprojects
Use this as a `readme.md` template to let people know what external libraries the subproject depends as a bullet list of links to conan packages which can be found at the [conan center](https://conan.io/center/recipes)

