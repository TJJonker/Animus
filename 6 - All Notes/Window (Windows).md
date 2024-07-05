2024-07-05 | 15:25  
**Status:** #alpha
**Tags:** [[Windows Programming]]

Windows has a designated window class, containing all the basic functionality needs so the operating system can communicate with it. When a window is created, we reference to it as a *window instance*. A window class isn't a typical C++ class, instead, it's a data structure used internally by the operating system, which we need to create at runtime. So instead of creating a window, it's more like *registering* a window.

#### Creating a window
To register a window, the WNDCLASSEX class must be filled. th 

## Format


## Example


## References
https://learn.microsoft.com/en-us/windows/win32/learnwin32/creating-a-window