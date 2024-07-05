2024-07-05 | 15:25  
**Status:** #beta
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
| ```hbrBackground``` | The background of the window.                                                                                                                                                     |
| ```lpszMenuName```  | Resource name of a class menu to use as a default.                                                                                                                                |
| ```hIconSm```       | Handle to a small icon associated with the window class.                                                                                                                          |
```cpp
typedef struct tagWNDCLASSEXW {
    UINT        cbSize;
    UINT        style;
    WNDPROC     lpfnWndProc;
    int         cbClsExtra;
    int         cbWndExtra;
    HINSTANCE   hInstance;
    HICON       hIcon;
    HCURSOR     hCursor;
    HBRUSH      hbrBackground;
    LPCWSTR     lpszMenuName;
    LPCWSTR     lpszClassName;
    HICON       hIconSm;
} WNDCLASSEXW, *PWNDCLASSEXW, NEAR *NPWNDCLASSEXW, FAR *LPWNDCLASSEXW;
```

When the WNDCLASSEX class is filled, we pass it's address to the ```RegisterClass()```function. 

```cpp
RegisterClass(&windowClass);
```

Finally, we create handle to the window by calling the ```CreateWindowEx()```function.

```cpp
CreateWindowEx(
    _In_ DWORD dwExStyle,
    _In_opt_ LPCWSTR lpClassName,
    _In_opt_ LPCWSTR lpWindowName,
    _In_ DWORD dwStyle,
    _In_ int X,
    _In_ int Y,
    _In_ int nWidth,
    _In_ int nHeight,
    _In_opt_ HWND hWndParent,
    _In_opt_ HMENU hMenu,
    _In_opt_ HINSTANCE hInstance,
    _In_opt_ LPVOID lpParam);
```

Showing the window can be achieved by calling the ```ShowWindow()```function and supplying the window handle together with a Boolean. To ensure the window is painted immediately, the ```UpdateWindow()```function can be called, supplying only the window handle.
## Example

```cpp
LPCTSTR title = L"Window Title";
WNDCLASSEX windowClass;

windowClass.cbSize        = sizeof(WNDCLASSEX);
windowClass.style         = CS_HREDRAW | CS_VREDRAW;
windowClass.lpfnWndProc   = WndProc;
windowClass.cbClsExtra    = NULL;
windowClass.cbWndExtra    = NULL;
windowClass.hInstance     = hInstance;
windowClass.hIcon         = LoadIcon(NULL, IDI_APPLICATION);
windowClass.hCursor       = LoadCursor(NULL, IDC_ARROW);
windowClass.hbrBackground = (HBRUSH)(COLOR_WINDOW + 2);
windowClass.lpszMenuName  = NULL;
windowClass.lpszClassName = L"Window class name";
windowClass.hIconSm       = LoadIcon(NULL, IDI_APPLICATION);

RegisterClass(&windowClass);

_handle = CreateWindowEx(
	NULL, 
	title, 
	title, 
	WS_OVERLAPPEDWINDOW, 
	CW_USEDEFAULT, 
	CW_USEDEFAULT, 
	1200, 
	800, 
	NULL, 
	NULL, 
	hInstance, 
	NULL);

ShowWindow(_handle, true);
UpdateWindow(_handle);
```

## References
https://learn.microsoft.com/en-us/windows/win32/learnwin32/creating-a-window
https://learn.microsoft.com/en-us/windows/win32/api/winuser/ns-winuser-wndclassexa
https://learn.microsoft.com/en-us/windows/win32/winmsg/window-class-styles