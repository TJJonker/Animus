2024-06-26 | 18:34  
**Status:** #beta
**Tags:** [[DirectX12]] 

A root signature is a data structure that contains parameters and corresponding data, which can be used in the shader. Shaders can be seen as functions and root signatures as the arguments supplied in the 'shader function'. The root signature can be split up into three parts: The Root Parameters, Static Samplers and the visibility flags.

#### Root Parameters
[[Root Parameters]] are the parameters supplied to the shader. From within the shader, these parameters can be accessed and their content can be read *(and changed?)*. These parameters can be split up into three groups:
1. **Root Constants** are inline constant values with the size of 1 [[DWORD]]. Since they are inline, thus not needing any redirection, they are extremely fast to access. The downside is that there is not a lot of memory allocated for root constants, which means this space is most often reserved for small regularly accessed data which changes often. 
2. **Root Descriptors** are pointers (2 [[DWORD]]s) to data used inside the shader. They have a single redirection since we need to access the pointer to retrieve the data, making them perfect for bigger, regularly accessed shader data.
3. **Descriptor tables** are collections of descriptors that are accessed as a group. They all have the size of a single [[DWORD]], holding just a 16-bit offset and a 16-bit length. Descriptor Tables are perfect for a collection of data that is accessed as a group like multiple textures (diffuse, normal, specular), which are bound together often. 

#### Static Samplers 
Static samplers are a list of [[Sampling State Object|Sampling State Objects]] that shaders can use without binding them dynamically, improving performance and simplicity when binding sample states. Once bound to the Root Signature, sampling states can be used when the root signature is bound.

#### Flags
Root signature flags are primarily used for setting data visibility and allowing certain pipeline stages to execute. The root signature flags offer the following options.

```cpp
enum D3D12_ROOT_SIGNATURE_FLAGS
    {
        D3D12_ROOT_SIGNATURE_FLAG_NONE	= 0,
        D3D12_ROOT_SIGNATURE_FLAG_ALLOW_INPUT_ASSEMBLER_INPUT_LAYOUT	= 0x1,
        D3D12_ROOT_SIGNATURE_FLAG_DENY_VERTEX_SHADER_ROOT_ACCESS	= 0x2,
        D3D12_ROOT_SIGNATURE_FLAG_DENY_HULL_SHADER_ROOT_ACCESS	= 0x4,
        D3D12_ROOT_SIGNATURE_FLAG_DENY_DOMAIN_SHADER_ROOT_ACCESS	= 0x8,
        D3D12_ROOT_SIGNATURE_FLAG_DENY_GEOMETRY_SHADER_ROOT_ACCESS	= 0x10,
        D3D12_ROOT_SIGNATURE_FLAG_DENY_PIXEL_SHADER_ROOT_ACCESS	= 0x20,
        D3D12_ROOT_SIGNATURE_FLAG_ALLOW_STREAM_OUTPUT	= 0x40,
        D3D12_ROOT_SIGNATURE_FLAG_LOCAL_ROOT_SIGNATURE	= 0x80,
        D3D12_ROOT_SIGNATURE_FLAG_DENY_AMPLIFICATION_SHADER_ROOT_ACCESS	= 0x100,
        D3D12_ROOT_SIGNATURE_FLAG_DENY_MESH_SHADER_ROOT_ACCESS	= 0x200,
        D3D12_ROOT_SIGNATURE_FLAG_CBV_SRV_UAV_HEAP_DIRECTLY_INDEXED	= 0x400,
        D3D12_ROOT_SIGNATURE_FLAG_SAMPLER_HEAP_DIRECTLY_INDEXED	= 0x800
    } 	D3D12_ROOT_SIGNATURE_FLAGS;
```


## Example

```cpp
	CD3DX12_ROOT_SIGNATURE_DESC rootSignatureDesc;
	rootSignatureDesc.Init(
		_countof(rootParameters), 
		rootParameters, 
		0, 
		nullptr,
		D3D12_ROOT_SIGNATURE_FLAG_ALLOW_INPUT_ASSEMBLER_INPUT_LAYOUT | 
		D3D12_ROOT_SIGNATURE_FLAG_DENY_HULL_SHADER_ROOT_ACCESS |
		D3D12_ROOT_SIGNATURE_FLAG_DENY_DOMAIN_SHADER_ROOT_ACCESS |
		D3D12_ROOT_SIGNATURE_FLAG_DENY_GEOMETRY_SHADER_ROOT_ACCESS |
		D3D12_ROOT_SIGNATURE_FLAG_DENY_PIXEL_SHADER_ROOT_ACCESS
	);

	ID3DBlob* signature;
	hr = D3D12SerializeRootSignature(
			&rootSignatureDesc, 
			D3D_ROOT_SIGNATURE_VERSION_1, 
			&signature, 
			nullptr
		);
	
	if (FAILED(hr))
		return false;

	hr = device->CreateRootSignature(
			0, 
			signature->GetBufferPointer(), 
			signature->GetBufferSize(), 
			IID_PPV_ARGS(&rootSignature)
		);
		
	if (FAILED(hr))
		return false;
```

## References

https://learn.microsoft.com/en-us/windows/win32/direct3d12/root-signatures