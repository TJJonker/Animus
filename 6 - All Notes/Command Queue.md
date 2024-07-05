2024-06-28 | 19:25  
**Status:** #beta
**Tags:** [[DirectX12]]

A command queue is responsible for submitting [[Command List|command lists]], synchronizing command list execution, collecting performance data or debug information, and updating resource tile mapping. 

The command queue has two commonly used functions:
- **ID3D12CommandQueue::ExecuteCommandLists:** Submits an array of command lists to the GPU for execution.
- **ID3D12CommandQueue::Signal:** Updates a [[Fence]] to a specified value.


## Format

```cpp
typedef struct D3D12_COMMAND_QUEUE_DESC {
	D3D12_COMMAND_LIST_TYPE         Type;
	INT                             Priority;
	D3D12_COMMAND_QUEUE_FLAGS       Flags;
	UINT                            NodeMask;
} D3D12_COMMAND_QUEUE_DESC;

HRESULT CreateCommandQueue( 
	const D3D12_COMMAND_QUEUE_DESC  *pDesc, 
	REFIID                          riid, 
	void                            **ppCommandQueue );
```

## Example

```cpp
ID3D12CommandQueue* commandQueue;
D3D12_COMMAND_QUEUE_DESC cqDesc = {};

HRESULT hr = device->CreateCommandQueue(&cqDesc, IID_PPV_ARGS(&commandQueue));
```

## References

https://learn.microsoft.com/en-us/windows/win32/api/d3d12/nn-d3d12-id3d12commandqueue
