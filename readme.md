# parasolid\_frustrum

The goal of this project is to make it very easy to write
C++ code that can read Parasolid text transmit files.

It *does not* implement any file writing, or graphical output.
It also *does not* implement binary file reading.

What it *does* do is:

- provide a modern CMake interface
- read text transmit (x\_t) files _either_ from disk or from raw strings (useful for in-memory files)
- provides a basic Parasolid frustrum implementation to get started

## Project Setup

Because Parasolid is a proprietary CAD kernel, you must have a
Parasolid distribution available on your system in order to use
this project. The location of your Parasolid distribution is
expected to be set by an environmental variable `$PARASOLID_BASE`.


I recommend using CMake's FetchContent to use the frustrum
in your projects:

```
FetchContent_Declare(
  ps_frustrum
  GIT_REPOSITORY   https://github.com/deGravity/parasolid_frustrum.git
  GIT_TAG   v1.0
)

FetchContent_MakeAvailable(ps_frustrum)

...

target_link_libraries(my_target INTERFACE parasolid_frustrum)
```

This _will fail_ if `$PARASOLID_BASE` is not defined.

`$PARASOLID_BASE` should be specific to your parasolid distribution,
and is expected to contain the following files:

- `parasolid_kernel.h`
- `kernel_interface.h`
- `frustrum_ifails.h`
- `frustrum_tokens.h`
- `pskernel_archive.lib`

## Using Parasolid

To use Parasolid in your C++ code, all you need to do is `#include <parasolid.h>`.
This will give you access to the full Parasolid interface (from `parasolid_kernel.h` 
and `kernel_interface.h`), as well as the function `ensure_parasolid_session()`, which you 
*must call* at least once before attempting to use any Parasolid functions. There is
no downside to calling this more than once.
