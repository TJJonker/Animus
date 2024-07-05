2024-07-05 | 17:09  
**Status:** #alpha 
**Tags:** [[DirectX12]]

A device is used to enumerate the functionality of a display adapter. A device can be thought of as a pointer to the GPU, allowing the user to communicate with the GPU drivers. A device allows the user to create a [[Command Queue]], [[Descriptor Heap]], [[Render Target View]], [[Command List]], etc.

To create a device, an adapter, to which a graphics processing unit is connected, must de found. This can be done with the help of an [[DirectX Graphics Infrastructure (DXGI))|IDXGIFactory]] by iterating over de adapters until a physical video adapter is found. This adapter can be used to create a device by calling the ```D3D12CreateDevice()```function.
## Format

```cpp
HRESULT D3D12CreateDevice( 
	[in, optional]  IUnknown          *pAdapter, 
				    D3D_FEATURE_LEVEL MinimumFeatureLevel, 
	[in]            REFIID riid, 
	[out, optional] void **ppDevice );
```

## Example


## References

https://learn.microsoft.com/en-us/windows/win32/direct3d11/overviews-direct3d-11-devices-intro
https://learn.microsoft.com/en-us/windows/win32/api/d3d12/nf-d3d12-d3d12createdevice