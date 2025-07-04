# glTF modular library (based on C, A-type)

A-type based glTF schema and parser — designed to load `.gltf` files directly into strongly-typed model structures, independent of any rendering or graphics subsystem.

### 💡 features
- fully declarative A-type class schema for all glTF core types  
- parses GLTF JSON into usable C data structures  
- supports materials, animations, meshes, accessors, buffers, nodes, and transforms  
- works standalone without any dependency on rendering systems (e.g. Vulkan, Metal, DirectX, OpenGL)

### 📦 usage

```c
#include <import>

int main(int argc, cstr argv[]) {
    A_start(argv);

    path gltf = path("models/flower8888.gltf");
    Model orbiter = read(gltf, typeid(Model));
}
```
this loads `flower8888.gltf` into a fully resolved `Model` class with access to nodes, skins, meshes, materials, etc.

for more information, check out orbiter & trinity's use of this object; there we use a Vulkan subsystem to render this model.

whatever object we define, we may serialize in and out of json. 'Model' is simply one case of this

A-type is a general object model capable of being a very node-like experience for C.  it is a meta
object model capable of high performance reflection in C, and uniquely capable of modern development.

### 📦 building (identical for all C-based, A-type libraries)

```sh
git clone https://github.com/ar-visions/A
git clone https://github.com/ar-visions/gltf
cd gltf
mkdir build
make -f ../Makefile
```

### 🚀 setting up import for your own A-type project (use-case: orbiter)
file: import

```import
A	https://github.com/ar-visions/A	main
vec	https://github.com/ar-visions/vec	main
gltf https://github.com/ar-visions/gltf main
trinity	https://github.com/ar-visions/trinity	main

app:
	A vec gltf trinity
	linux:
		asound

```

### 🔧 environment setup
```sh
# the place where we install software, lib/include/bin/etc
export TAPESTRY="/home/user/src/tapestry"

# debug only locally cloned source (your own, and what you clone to work on)
export DBG="*"
```

also useful to setup your SRC directory so import may look here and symlink rather than checkout git ... this A-type import pattern improves general software development practices for all libraries.

### 📂 create app/lib folder in your app/lib repo, with the following Makefile:
file: Makefile

```Makefile
PROJECT := your_project
REL := $(dir $(abspath $(lastword $(MAKEFILE_LIST))))
include $(REL)../A/build.mk
```
as stated above, we add your_app.c / .cc (C++ support is there, albeit with more casting: see image.cc in trinity) to an app or lib folder.  A-type builds app or lib based on these directories and files within.  only 1 library is built per project, but any number of app modules may be made.
