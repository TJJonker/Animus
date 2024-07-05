2024-07-05 | 17:09  
**Status:** #alpha 
**Tags:** [[DirectX12]]

A device is used to enumerate the functionality of a display adapter. A device can be thought of as a pointer to the GPU, allowing the user to communicate with the GPU drivers. A device allows the user to create a [[Command Queue]], [[Descriptor Heap]], [[Render Target View]], [[Command List]], etc.

To create a device, an adapter, to which a graphics processing unit is connected, must de found. This can be done with the help of an [[IDXGIFactory Interface]] by iterating over de adapters until a physical video adapter is found. This adapter can be used to create a device by calling the ```D3D12CreateDevice()```function.
## Format

```cpp
HRESULT D3D12CreateDevice( 
	[in, optional]  IUnknown          *pAdapter, 
				    D3D_FEATURE_LEVEL MinimumFeatureLevel, 
	[in]            REFIID            riid, 
	[out, optional] void              **ppDevice );
```

## Example

```cpp
IDXGIAdapter1* adapter; // Link to a graphics unit 

int adapterIndex = 0;
bool adapterFound = false;

while (dxgiFactory->EnumAdapters1(adapterIndex, &adapter)
	   != DXGI_ERROR_NOT_FOUND) 
{
	DXGI_ADAPTER_DESC1 desc;
	adapter->GetDesc1(&desc);

	// Check for software device and skip it
	if (desc.Flags & DXGI_ADAPTER_FLAG_SOFTWARE) {
		adapterIndex++;
		continue;
	}

	// Check for Physical device and return the index
	hr = D3D12CreateDevice(
		adapter, D3D_FEATURE_LEVEL_11_0, _uuidof(ID3D12Device), nullptr);
	
	if (SUCCEEDED(hr)) {
		adapterFound = true;
		break;
	}

	adapterIndex++;
}

if (adapterFound)
	D3D12CreateDevice(adapter, D3D_FEATURE_LEVEL_11_0, IID_PPV_ARGS(&device));

```

## References

https://learn.microsoft.com/en-us/windows/win32/direct3d11/overviews-direct3d-11-devices-intro
https://learn.microsoft.com/en-us/windows/win32/api/d3d12/nf-d3d12-d3d12createdevice
https://www.braynzarsoft.net/viewtutorial/q16390-03-initializing-directx-12