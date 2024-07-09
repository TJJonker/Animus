2024-07-09 | 15:53  
**Status:** #alpha 
**Tags:** [[DirectX12]]

An Input Data Layout object describes the layout of the data sent to the GPU. Most often, this corresponds with the vertex buffer data used to render object in the scene. This vertex buffer usually contains information like (but not limited to) vertex data, normal coordinates, tangents and texture coordinates.

DirectX12 requires the programmer to describe the Input Data Layout in an array of  ```D3D12_INPUT_ELEMENT_DESC``` instance, which can be supplied to the [[The Pipeline State Object (PSO)]] through a ```D3D12_INPUT_LAYOUT_DESC``` object. 

## Format
The ```D3D12_INPUT_ELEMENT_DESC``` contains the following attributes:


## Example


## References
