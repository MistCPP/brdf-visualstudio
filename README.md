# BRDFExplorer-VisualStudio
disney brdf explorer 的visual studio2022版本

工程只需要添加zlib库，不需要glew和glut，链接zlib时需要注意 预处理器宏ZLIB_WINAPI​：
在使用zlibwapi的动态库时，必须在编译你的项目源代码前，预定义ZLIB_WINAPI这个宏。
这是因为zlibwapi.dll的函数调用约定是WINAPI（即__stdcall），而zlib默认使用的是CDECL约定，不定义此宏会导致链接错误（未定义符号...)。可以在项目属性 -> C/C++ -> 预处理器 -> 预处理器定义中添加它。

工程使用QT6.9.2编译，对一些4.8.1之后不再支持的接口做了改动：
```cpp
//typedef OPENGL_CORE_FUNCS GlFuncs;
typedef QOpenGLExtraFunctions GlFuncs;

//glf = glcontext->versionFunctions<GlFuncs>();
glf = glcontext->extraFunctions();

//layout->setMargin( 1 );
layout->setContentsMargins(1, 1, 1, 1);

//float* p = (float*)glf->glMapBuffer( GL_TEXTURE_BUFFER, GL_WRITE_ONLY );
float* p = (float*)glf->glMapBufferRange(GL_TEXTURE_BUFFER, 0, numBytes, GL_MAP_WRITE_BIT);
```
