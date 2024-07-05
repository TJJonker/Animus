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




## Format


## Example


## References
https://learn.microsoft.com/en-us/windows/win32/api/d3d12/nn-d3d12-id3d12commandlist
https://learn.microsoft.com/en-us/windows/win32/api/d3d12/ne-d3d12-d3d12_command_list_type