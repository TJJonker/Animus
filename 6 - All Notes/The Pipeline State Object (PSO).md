2024-06-26 | 16:41  
**Status:** #beta
**Tags:** [[DirectX12]] 


The Pipeline State Object is a data structure that describes the current state of the rendering pipeline. It's power is in the initialization at the start of the runtime and efficient assignment when the state needs to be changed. This way, states can easily be managed, reducing the likelihood of making mistakes when changing states and encapsulating logic to a single data structure.

This data structure usually contains the following data:
- [[The Root Signature]]
- [[Shader bytecode]]
- [[Input Data Layout]]
- [[Primitive Topology]]
- [[Rasterization State]]
- [[Blending State]]
- [[Depth-Stencil State]]
- [[Data Formats|Render Target Formats]]
- [[Sample Mask]]
- [[Node Mask]]
- [[Cached Pipeline State Object]]

## Example

```cpp
// Create a description for the PSO
D3D12_GRAPHICS_PIPELINE_STATE_DESC psoDesc = {};

psoDesc.InputLayout = inputLayoutDesc; // Describe the data layout
psoDesc.pRootSignature = rootSignature; // Bind a Root Signature
psoDesc.VS = vertexShaderBytecode; // Add vertex shader bytecode
psoDesc.PS = pixelShaderBytecode; // Add pixel shader bytecode
psoDesc.HS = hullShaderBytecode; // Add hull shader bytecode
psoDesc.DS = domainShaderBytecode; // Add domain shader bytecode
psoDesc.GS = geometryShaderBytecode; // Add geometry shader bytecode
psoDesc.PrimitiveTopologyType = D3D12_PRIMITIVE_TOPOLOGY_TYPE_TRIANGLE; // Set primitive topology type
psoDesc.RTVFormats[0] = DXGI_FORMAT_B8G8R8A8_UNORM; // Set rendertarget dataformat
psoDesc.SampleDesc = sampleDesc; // Describe sample settings
psoDesc.SampleMask = 0xffffffff; // Add a sampling mask
psoDesc.RasterizerState = CD3DX12_RASTERIZER_DESC(D3D12_DEFAULT); // Control rasterization settings
psoDesc.BlendState = CD3DX12_BLEND_DESC(D3D12_DEFAULT); // Control blend settings
psoDesc.DepthStencilState = CD3DX12_DEPTH_STENCIL_DESC(D3D12_DEFAULT); // Set depth and stencil buffer settings.
psoDesc.NumRenderTargets = 1; // Define the amount of render targets

// Create the PSO
hr = device->CreateGraphicsPipelineState(
	&psoDesc, 
	IID_PPV_ARGS(&pipelineStateObject)
	);

// Check if initialization succeeded
if (FAILED(hr))
	return false;
```





## References
