2024-07-07 | 15:10  
**Status:** #alpha 
**Tags:** [[DirectX12]]

A descriptor heap is a collection of contiguous allocated memory for descriptors. Prior to creating a descriptor, a descriptor heap is necessary to assign a memory address to the descriptor. While all types of descriptors can be stored in a descriptor heap, there are some restrictions on what can go in the same descriptor. CBV, UAV and SRV entries can be stored in the same descriptor heap, but can't be stored together with Samplers. Typically, there are two sets of descriptor heaps, one for the common resources and the second for Samplers.

#### Shader Visibility
All descriptor heaps are accessible for the CPU, meaning the CPU can read and write to these heaps, but descriptor heaps can also be configured be accessible for shaders. This can be done by setting the heap flag to ```D3D12_DESCRIPTOR_HEAP_FLAG_SHADER_VISIBLE```. The default flag is ```D3D12_DESCRIPTOR_HEAP_FLAG_NONE```, making the descriptor heap invisible for shaders.

## Format

```cpp
struct D3D12_DESCRIPTOR_HEAP_DESC
{
	D3D12_DESCRIPTOR_HEAP_TYPE     Type;
	UINT                           NumDescriptors;
	D3D12_DESCRIPTOR_HEAP_FLAGS    Flags;
	UINT                           NodeMask;
} 	D3D12_DESCRIPTOR_HEAP_DESC;
```

## Example

```cpp
D3D12_DESCRIPTOR_HEAP_DESC rtvHeapDesc = {};

rtvHeapDesc.NumDescriptors = 1;
rtvHeapDesc.Type = D3D12_DESCRIPTOR_HEAP_TYPE_RTV; 
rtvHeapDesc.Flags = D3D12_DESCRIPTOR_HEAP_FLAG_NONE;

device->CreateDescriptorHeap(&rtvHeapDesc, IID_PPV_ARGS(&rtvDescriptorHeap));
```


## References

https://learn.microsoft.com/en-us/windows/win32/direct3d12/descriptor-heaps