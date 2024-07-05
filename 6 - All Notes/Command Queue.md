2024-06-28 | 19:25  
**Status:** #alpha 
**Tags:** [[DirectX12]]

A command queue is responsible for maintaining and executing commands on the GPU. Typically, these commands are related to rendering graphics, performing compute operations, or handling resource management. Due to the batching of commands on the CPU before sending them to the GPU, command queues prove to be more efficient than traditional separate API calls. Additionally, command queues allow for a parallel workflow, where one command queue can be executed by the GPU, while the CPU populates another.


## Format


## Example


## References
