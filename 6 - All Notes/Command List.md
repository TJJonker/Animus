2024-07-05 | 13:02  
**Status:** #alpha 
**Tags:** [[DirectX12]]

A command list (otherwise known as a command buffer) is populated with commands that the GPU will execute. For example rendering, GPU computations and setting and clearing the pipeline state. A [[Command Queue]] is then used to execute the command lists by sending them to the GPU.

Command lists can be used for goals. In the table below, all possible command list types can be found with their corresponding use case.

| Type                                        | Use                                                                                                                                                                                       |
| ------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ```D3D12_COMMAND_LIST_TYPE_DIRECT```        | Creates a command buffer that can be directly executed by the GPU. It Doesn't inherit any GPU state.                                                                                      |
| ```D3D12_COMMAND_LIST_TYPE_BUNDLE```        | Creates a command buffer that can only be directly executed by a direct command list. Inherits all GPU state except for the currently set pipeline state object and primitive technology. |
| ```D3D12_COMMAND_LIST_TYPE_COMPUTE```       | Creates a command buffer for computing.                                                                                                                                                   |
| ```D3D12_COMMAND_LIST_TYPE_COPY```          | Creates a command buffer for copying.                                                                                                                                                     |
| ```D3D12_COMMAND_LIST_TYPE_VIDEO_DECODE```  | Creates a command buffer for video decoding.                                                                                                                                              |
| ```D3D12_COMMAND_LIST_TYPE_VIDEO_PROCESS``` | Creates a command buffer for video processing.                                                                                                                                            |

To use command lists, a Command Allocator needs to be created, allocating memory for the command lists. Next, we create the command allocator itself and give the pointer to our allocated memory, allowing it to record and store commands at that pointer. When execute the command list, we need to reset the content, after which we can record new commands and populate the command list.

#### Graphics Command List
A graphics specialized command list is created, encapsulating a list of graphics commands for rendering. This Graphics Command List interface inherits from the generic command list interface.
An elaborate list of functions used with this type of command list can be found in the [graphics command list documentation](https://learn.microsoft.com/en-us/windows/win32/api/d3d12/nn-d3d12-id3d12graphicscommandlist).

## Format
```cpp
HRESULT STDMETHODCALLTYPE CreateCommandList( 
	_In_          UINT nodeMask,
	_In_          D3D12_COMMAND_LIST_TYPE type,
	_In_          ID3D12CommandAllocator *pCommandAllocator,
	_In_opt_      ID3D12PipelineState *pInitialState,
	REFIID        riid,
	_COM_Outptr_  void **ppCommandList
);
```



## Example

```cpp
ID3D12CommandAllocator* commandAllocator[3];

for (int i = 0; i < frameBufferCount; i++) {
	device->CreateCommandAllocator(
		D3D12_COMMAND_LIST_TYPE_DIRECT, 
		IID_PPV_ARGS(&commandAllocator[i]));
}

device->CreateCommandList(
	0, 
	D3D12_COMMAND_LIST_TYPE_DIRECT, 
	commandAllocator[0], 
	NULL, 
	IID_PPV_ARGS(&commandList));
```

## References
https://learn.microsoft.com/en-us/windows/win32/api/d3d12/nn-d3d12-id3d12commandlist
https://learn.microsoft.com/en-us/windows/win32/api/d3d12/ne-d3d12-d3d12_command_list_type
https://learn.microsoft.com/en-us/windows/win32/api/d3d12/nn-d3d12-id3d12graphicscommandlist