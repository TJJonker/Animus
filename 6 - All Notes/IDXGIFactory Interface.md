2024-07-05 | 17:43  
**Status:** #beta
**Tags:** [[DirectX12]]

An IDXGIFactory Interface implements method for the creation of DXGI objects, which are responsible for full screen transitions. It can be created by calling the ```CreateDXGIFactory()``` and supplying a pointer where the instance should be stored.

The variable of the IDXGIFactory ends with 1, 2, 3 or 4, which is the version number. The higher numbers most often means a more recent version, which is advisable to use. Keep in mind that some other interfaces might require earlier versions of another interface.

The IDXGIFactory interface contains the following functions:

| Function                                                                                                                                                  |
| --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ```IDXGIFactory::CreateSoftwareAdapter```<br>Creates an adapter interface that represents a software device.<br>‎                                         |
| ```IDXGIFactory::CreateSwapChain```<br>Creates a swap chain.<br>‎                                                                                         |
| ```IDXGIFactory::EnumAdapters```<br>Enumerates the video card adapters.<br>‎                                                                              |
| ```IDXGIFactory::GetWindowAssociation```<br>Get the window that goes in or out of full screen.<br>‎                                                       |
| ```IDXGIFactory::MakeWindowAssociation```<br>Allows lDXGI to monitor an application's message queue to check if it's going in or out of full screen.<br>‎ |

## Format

```cpp
HRESULT WINAPI CreateDXGIFactory(
	REFIID             riid, 
	_COM_Outptr_ void  **ppFactory);
```
## Example

```cpp
IDXGIFactory4* dxgiFactory;
hr = CreateDXGIFactory(IID_PPV_ARGS(&dxgiFactory));
```




## References

https://learn.microsoft.com/en-us/windows/win32/api/dxgi/nn-dxgi-idxgifactory