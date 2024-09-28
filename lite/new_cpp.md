# new cpp proj

ref code

```
tensorflow/lite/micro/
======================
    cortex_m_generic    - platform specific
    kernel  -contains operation implementations and the associated code.
    tools   - which contains build tools and their output.
```


### device specific

By default, the project will be compiled for the host operating system. To specify a different target architecture, use TARGET= and TARGET_ARCH=


### Optimized kernels

To generate projects using optimized kernels, use the following command, replacing <subdirectory_name> with the name of the subdirectory containing the optimizations:

make -f tensorflow/lite/micro/tools/make/Makefile TAGS=<subdirectory_name> generate_projects


