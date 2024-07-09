2024-07-09 | 15:53  
**Status:** #alpha 
**Tags:** [[DirectX12]]

An Input Data Layout object describes the layout of the data sent to the GPU. Most often, this corresponds with the vertex buffer data used to render object in the scene. This vertex buffer usually contains information like (but not limited to) vertex data, normal coordinates, tangents and texture coordinates.

DirectX12 requires the programmer to describe the Input Data Layout in an array of  ```D3D12_INPUT_ELEMENT_DESC``` instance, which can be supplied to the [[The Pipeline State Object (PSO)]] through a ```D3D12_INPUT_LAYOUT_DESC``` object. 

## Format
The ```D3D12_INPUT_ELEMENT_DESC``` contains the following attributes:

| Functions                                                                                                                                                                                                |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ```SemanticName```<br>HLSL semantic associated with this element.<br>‎‎                                                                                                                                  |
| ```SemanticIndex```<br>Index of the semantic in case multiple elements have the same semantic.<br>‎                                                                                                      |
| ```Format```<br>```DXGI_Format``` of the element.<br>‎                                                                                                                                                   |
| ```InputSlot```<br>Integer value identifying the input-assemblers input slot, in case multiple vertex buffers are used.<br>‎                                                                             |
| ```AlignedByteOffset```<br>Offset in bytes from the start of the vertex.<br>‎                                                                                                                            |
| ```InputSlotClass```<br>Defines the data class; Per vertex or per instance.<br>‎                                                                                                                         |
| ```InstanceDataStepRate```<br>Number of instances to draw using the same instance data before advancing to the next element in the buffer. Must be ```0``` for an element that contains per-vertex data. |
```cpp
typedef struct D3D12_INPUT_ELEMENT_DESC { 
	LPCSTR                      SemanticName; 
	UINT                        SemanticIndex; 
	DXGI_FORMAT                 Format; 
	UINT                        InputSlot; 
	UINT                        AlignedByteOffset; 
	D3D12_INPUT_CLASSIFICATION  InputSlotClass; 
	UINT                        InstanceDataStepRate; 
} D3D12_INPUT_ELEMENT_DESC;
```

## Example

```cpp
D3D12_INPUT_ELEMENT_DESC inputLayout[] =
{
	{ "POSITION", 0, DXGI_FORMAT_R32G32B32_FLOAT, 0, 0,
	  D3D12_INPUT_CLASSIFICATION_PER_VERTEX_DATA, 0	},
	{ "COLOR", 0, DXGI_FORMAT_R32G32B32A32_FLOAT, 0, 12,
	  D3D12_INPUT_CLASSIFICATION_PER_VERTEX_DATA, 0	}
};

D3D12_INPUT_LAYOUT_DESC inputLayoutDesc = {};

inputLayoutDesc.NumElements = 
	sizeof(inputLayout) / sizeof(D3D12_INPUT_ELEMENT_DESC);
inputLayoutDesc.pInputElementDescs = inputLayout;
```


## References

https://learn.microsoft.com/en-us/windows/win32/api/d3d12/ns-d3d12-d3d12_input_element_desc