2024-06-28 | 16:10  
**Status:** #alpha
**Tags:** [[DirectX12]]
 
A swap chain is a rendering technique used to reduce or even eliminate the effects of [[screen tearing]] by using two or more render buffers and swapping between them (hence the name 'swap chain'). In a swap chain, we make use of a single screen buffer and n - 1 back buffers. The screen buffer will be shown on the display, while the GPU writes to the next back buffer. Once the GPU is finished, the current screen buffer will swap with the next back buffer, rendering the the new screen buffer to the screen when the display requests a refresh.  

##### Command Queue
A powerful expansion on the swap chain is the addition of a [[Command Queue]]. By creating a separate command queue for every buffer in the swap chain, command can be prepare without having to wait for the GPU to finish doing it's tasks, allowing the CPU to run parallel with the GPU. Precautions have to be taken when using parallelism. In this case, the CPU might want to change data used by the GPU, possibly causing issues if the data is in use. This problem can be solved by using [[Fence events]], forcing the CPU to stall the action until the Fence event is called by the GPU.  


## Example




## References
