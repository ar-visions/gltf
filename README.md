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
    A_start();

    path gltf = path("models/orbiter.gltf");
    Model orbiter = read(gltf, typeid(Model));
}
```

for more information, check out orbiter & trinity's use of this data; there we use a Vulkan subsystem.

### 📦 building (identical for all C-based, A-type libraries)

```sh
git clone https://github.com/ar-visions/A
git clone https://github.com/ar-visions/gltf
cd gltf
mkdir build
make -f ../Makefile
```

This loads `orbiter.gltf` into a fully resolved `Model` class with access to nodes, skins, meshes, materials, etc.

