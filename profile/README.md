# cpp-toolbox

A collection of repositories which use eachother to build up more complex programs. 

The goal is to stop writing same code, and doing it in a slightly different way each time, but rather improve the quality of existing code.

Most of the content will be taloired for game development so there will be examples of sound, physics, etc...

The code should run on on windows, mac and linux, with an emphasis on linux first as anyone with a computer can get linux, but not everyone can afford windows or mac.

Anyone is welcome to contribute

**NOTE: Before you do anything else, [read this article](https://toolbox.cuppajoeman.com/tool_howtos/git/projects_as_composition_of_submodules.html) to understand why the structure is the way that it is**

# Projects
The projects in this repo should do one thing well, and only do that, try not to have multiple goals when creating new projects in this organization.

All projects use submodules to facilitate the integration of subprojects, subprojects need to be setup to link to eachother using `sbpt`, for managing external libraries we use `conan` so install it on your system and follow their docs for preliminary setup on how to generate a profile before you run any conan commands.

First `cd` into the root of the project, then: 

```
# get all subproject content
git submodule update --init --recursive

# generate dynamic includes to linked subprojects
cd sbpt
python sbpt.py initialize ../src
cd ..

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
Anything denoted by SUBPROJECT is a repository of files, which probably will not work on it's own, but is to be used in a larger application, there are 50+ repositories here so listing them out would be too long, instead read about how to interact with them in the tools section


# Minimal Working Examples
Along with these SUBPROJECTS we also have some minimally working examples that use the subprojects:
* [mwe glfw](https://github.com/opengl-toolbox/mwe_glfw) - glfw window using opengl
* [mwe shader cache](https://github.com/cpp-toolbox/mwe_shader_cache) - a wrapper around working with shaders, greatly simplifies interaction with opengl and shaders
* [mwe texture atlas](https://github.com/cpp-toolbox/mwe_texture_atlas) - a system for working with texture atlases through a simple json format
* [mwe vertex geometry](https://github.com/cpp-toolbox/mwe_vertex_geometry) - a minimal place to view 3d geometry, uses a noclip fps camera
* [mwe model loading](https://github.com/opengl-toolbox/mwe_model_loading) - model loading with noclip 3d character controller
* [mwe model loading lighting](https://github.com/cpp-toolbox/mwe_model_loading_lighting) - same as above with lighting
* [mwe font rendering](https://github.com/opengl-toolbox/mwe_font_rendering) - demonstrates font rendering with freetype fonts
* [mwe physics world with character](https://github.com/opengl-toolbox/mwe_physics_world_with_character) - demonstrates a 3d world with a character that can be controlled with mouse and keyboard (Jolt Physics)
* [mwe sound world with character](https://github.com/opengl-toolbox/mwe_sound_world_with_character) - demonstrates a 3d world with positional sound with a character which can be controleld with mouse and keyboard (openal)
* [mwe networking](https://github.com/opengl-toolbox/mwe_networking) - basic network setup with enet
* [mwe networked physics world with character](https://github.com/opengl-toolbox/mwe_networked_physics_world_with_character)- demonstrates a client-server network model using enet, supports connections and renders other players on the map

# tools

## [`build_notifier`](https://github.com/cpp-toolbox/build_notifier)
Every project here uses conan for package management, due to that you usually have to run the command `cmake --build --preset conan-release` a bunch, which is tiresome, and while you can go back in your terminals history I wanted a more robust way to deal with this, as a cherry on top when compilation finishes there is a success or fail sound so you can stop staring at the build process and continue working in the mean time.

## [`sbpt`](https://github.com/cpp-toolbox/sbpt)
When subprojects use other subprojects you usually have to hard-code includes to those locations which differ based on file structure, therefore this script was created to fix this issue.

## [`cpp_file_generator`](https://github.com/cpp-toolbox/cpp_file_generator)
IDE's have a lot of features, but language servers are catching up, one feature that's nice that a language server doesn't have right now is simply creating new `.cpp`/`.hpp` pairs for a new class or file you want to make, this generator does so.

## [`editor_configurations`](https://github.com/cpp-toolbox/editor_configurations/)
When working with a cpp-toolbox project there are usually four main things you want to do
1. build the program
2. run the program
3. debug the program
4. use git
   
the editor configurtion repository tries to facilitate those needs in a simple manner for whatever editor that the developers currently use. Since I use neovim then I have those configurations there to start neovim with these terminals opened (in buffers) run `python scripts/editor_configurations/launch_nvim.py` or from a running instance of nvim `:source scripts/editor_configurations/cpp_terminal_autostart.vim`.


## [`cpp_project_bootstrapper`](https://github.com/cpp-toolbox/cpp_project_bootstrapper)
Making new cpp projects can become tiresome, setting up the required files takes time away from coding, but in our context we have to be able to make a lot of different projects for testing purposes and the creation of mwe's therefore this script helps manage that process to be much faster than usual

## [`process_changes_in_submodules`](https://github.com/cpp-toolbox/process_changes_in_submodules)
When you're working in projects mainly composed of submodules, then when you make various changes around the project you'll notice it takes a longer time to commit those changes because you have to visit each submodule seperately and give it their own commit, while this is fine, the moving around part and figuring out where you need to go part is tiresome, this script fixes that.

## [`cpp_tbx_submodule_adder`](https://github.com/cpp-toolbox/cpp_tbx_submodule_adder)
When you're building up new projects you'll find that adding submodules can be cumbersome, in order to know what submodules you have you have to look at the web interface go to the project, copy the clone url and so on, this script solves this by providing a command line interface to list and select submodules automatically.

