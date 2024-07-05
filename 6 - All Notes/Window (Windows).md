2024-07-05 | 15:25  
**Status:** #alpha
**Tags:** [[Windows Programming]]

Windows has a designated window class, containing all the basic functionality it needs so the operating system can communicate with it. When a window is created, we reference to it as a *window instance*. A window class isn't a typical C++ class, instead, it's a data structure used internally by the operating system, which we need to create at runtime. Instead of creating a window, it's more like *registering* a window.

#### Creating a window
To register a window, the WNDCLASSEX class must be filled. Although this class offers a variety of settings, 4 of them are mandatory:
- **lpfnWndProc** which is a pointer to the [[window procedure]]. 
- **hInstance** is the handle to the application instance.
- **lpszClassname**, which is a string that identifies the window class.
- **cbSize**, which defines the size of the structure, which can be set to ```sizeof(WNDCLASSEX)```

Other settings found in the WNDCLASS can be set to zero, or populated to achieve the following results:

| Setting             | Effect                                                                                                                                                                            |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ```style```         | Bitfield with more window related settings like redraw-on-resize, window dropshadow, etc. See [docs](https://learn.microsoft.com/en-us/windows/win32/winmsg/window-class-styles). |
| ```cbClsExtra```    | Number of extra bytes to allocate after the window-class structure.                                                                                                               |
| ```cbWndExtra```    | Number of extra bytes to allocate after the window instance.                                                                                                                      |
| ```hIcon```         | A handle to a class icon. If null, the system provides a default icon.                                                                                                            |
| ```hCursor```       | A handle to a class cursor. If null, the application must explicitly set the cursor shape.                                                                                        |
| ```hbrBackground``` |                                                                                                                                                                                   |
| ```lpszMenuName```  |                                                                                                                                                                                   |
| ```hIconSm```       |                                                                                                                                                                                   |

## Format


## Example


## References
https://learn.microsoft.com/en-us/windows/win32/learnwin32/creating-a-window
https://learn.microsoft.com/en-us/windows/win32/api/winuser/ns-winuser-wndclassexa
https://learn.microsoft.com/en-us/windows/win32/winmsg/window-class-styles