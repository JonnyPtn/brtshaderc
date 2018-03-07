# brtshaderc
Hack of the bgfx shaderc tools in library version to compile bgfx shaders source at runtime.
Inspired from Lumix engine code.

- It use the original shaderc code without doing any modification (easy to keep updated).
- Compiled shaders are built in memory without any write file access to disk.

## Compilation

Drop content in bgfx folder and build bgfx as usual.
This will build 'brtshaderc' a library version of shaderc than can be linked to your project.

## Example

```cpp
#include <brtshaderc.h>
...

// compile vertex shader
const bgfx::Memory* memVsh =  shaderc::compileShader(shaderc::ST_VERTEX,"vs_cubes.sc");
bgfx::ShaderHandle vsh = bgfx::createShader(memVsh);

// compile fragment shader
const bgfx::Memory* memFsh =  shaderc::compileShader(shaderc::ST_FRAGMENT,"fs_cubes.sc");
bgfx::ShaderHandle fsh = bgfx::createShader(memFsh);

// build program using shaders
mProgram = bgfx::createProgram(vsh, fsh, true);
```

or using arguments list syntax style (same as binary version) :

```
int argc = 0;
const char* argv[16];
argv[argc++] = "-f";
argv[argc++] = "vs_cubes.sc";
argv[argc++] = "--varyingdef";
argv[argc++] = "varying.def.sc";
argv[argc++] = "--type";
argv[argc++] = "v";
argv[argc++] = "--platform";
argv[argc++] = "windows";
argv[argc++] = "--profile";
argv[argc++] = "ps_4_0";

const bgfx::Memory* memVsh = shaderc::compileShader(argc, argv);
bgfx::ShaderHandle vsh = bgfx::createShader(memVsh);
```