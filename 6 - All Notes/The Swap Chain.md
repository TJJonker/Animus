2024-06-28 | 16:10  
**Status:** #beta 
**Tags:** [[DirectX12]]
 
A swap chain is a rendering technique used to reduce or even eliminate the effects of [[screen tearing]] by using two or more render buffers and swapping between them (hence the name 'swap chain'). In a swap chain, we make use of a single screen/front buffer and n - 1 back buffers. The screen buffer will be shown on the display, while the GPU writes to the next back buffer. Once the GPU is finished, the current screen buffer will swap with the next back buffer, rendering the the new screen buffer to the screen when the display requests a refresh.  

##### Command Queue
A powerful expansion on the swap chain is the addition of a [[Command Queue]]. By creating a separate command queue for every buffer in the swap chain, command can be prepare without having to wait for the GPU to finish doing it's tasks, allowing the CPU to run parallel with the GPU. Precautions have to be taken when using parallelism. In this case, the CPU might want to change data used by the GPU, possibly causing issues if the data is in use. This problem can be solved by using [[Fence events]], forcing the CPU to stall the action until the Fence event is called by the GPU.  

#### Swap effects
Swap effects describe how the content of the back buffer is presented in the front buffer and what happens to the content after the swap. There are 4 effects of which 2 are supported by DirectX12:
- **DXGI_SWAP_EFFECT_DISCARD** *(Not supported)*: Discards the content of the back buffer after being presented.
- **DXGI_SWAP_EFFECT_SEQUENTIAL** *(Not supported)*: Preserves the content of the back buffer after being presented and presents the swap chain in order.
- **DXGI_SWAP_EFFECT_FLIP_SEQUENTIAL**: Flips the front and back buffer when presented and preserves the content of the back buffer after being presented.
- **DXGI_SWAP_EFFECT_FLIP_DISCARD**: Flips the front and back buffer when presented and discards the content of the back buffer after being presented.

> **Note that sequential effects do not support [[multisampling|Multisampling]]** 


## Format
 
```cpp
typedef struct DXGI_SWAP_CHAIN_DESC
{
	DXGI_MODE_DESC BufferDesc;
	DXGI_SAMPLE_DESC SampleDesc;
	DXGI_USAGE BufferUsage;
	UINT BufferCount;
	HWND OutputWindow;
	BOOL Windowed;
	DXGI_SWAP_EFFECT SwapEffect;
	UINT Flags;
} 	DXGI_SWAP_CHAIN_DESC;
```


## Example

```cpp
DXGI_MODE_DESC backBufferDesc = {};
backBufferDesc.Width = Width; 
backBufferDesc.Height = Height;
backBufferDesc.Format = DXGI_FORMAT_B8G8R8A8_UNORM; 

DXGI_SAMPLE_DESC sampleDesc = {};
sampleDesc.Count = 1; 

DXGI_SWAP_CHAIN_DESC swapChainDesc = {};
swapChainDesc.BufferCount = frameBufferCount; 
swapChainDesc.BufferDesc = backBufferDesc; 
swapChainDesc.BufferUsage = DXGI_USAGE_RENDER_TARGET_OUTPUT; 
swapChainDesc.SwapEffect = DXGI_SWAP_EFFECT_FLIP_DISCARD; 
swapChainDesc.OutputWindow = hwnd; 
swapChainDesc.SampleDesc = sampleDesc; 
swapChainDesc.Windowed = !FullScreen; 

IDXGISwapChain* tempSwapChain;

dxgiFactory->CreateSwapChain(commandQueue, &swapChainDesc, &tempSwapChain);
swapChain = static_cast<IDXGISwapChain3*>(tempSwapChain);
```

## References

https://learn.microsoft.com/nl-nl/windows/win32/api/dxgi/ne-dxgi-dxgi_swap_effect?redirectedfrom=MSDN