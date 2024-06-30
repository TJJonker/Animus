2024-06-30 | 21:16
**Source:** [How does Computer Memory Work](https://www.youtube.com/watch?v=7J7X7aZvMXQ&pp=ygUdaG93IGRvZXMgY29tcHV0ZXIgbWVtb3J5IHdvcms%3D) 
**Status:** #alpha #beta #release
**Tags:** 

DRAM is an abbreviation for Dynamic Random Access Memory, which is otherwise known as 'main memory' or 'working memory'.  In order to use data, it needs to be moved from any long term storage module to the DRAM. 

Long term storage permanently stores data in massive 3D arrays, while DRAM temporarily stores data in 2D arrays. Fetching data from an SSD can take 50 microseconds (10$^-$$^6$ seconds), while fetching data from DRAM takes 17 nanoseconds (10$^-$$^9$ seconds), which makes DRAM data fetching about 3000 times faster. 

Downsides of DRAM is that it requires power to maintain and refresh its data, and that it stores a single bit per memory cell in a 2D array. Because of the power requirement, shutting down the computer will reset DRAM data. Regarding the storage, storing a single bit per memory cell is space inefficient, requiring large physical space on the module to store bigger chunks of data. 

The CPU will use data by moving the data from the SSD to the DRAM and prefetching the data to the CPU's cache. Prefetching is the process of fetching data before it is used in order to eliminate the overhead of having to fetch the data right before it is used.

>*"Why is it called Dynamic Random Access Memory? Also, why didn't we just call it RAM or just Memory throughout the video? Well, Random Access, means the computer can access any section of data with an equal amount of time before the data is read or written compared to any other section. The opposite is Linear Access Memory, which like a cassette tape. It's 'Dynamic' because the data cells lose charge over time, and thus have to be refreshed multiple times a second. Finally, we didn't call it RAM, because there are many types of RAM. SSDs are technically NVRAM [Non-Volatile RAM] Cache memory in the CPU is SRAM [Static RAM], GPUs use VRAM [Video RAM], which is VERY close in design to DRAM, and additionally there lesser known ones like MRAM [Magnetoresistive RAM] , and many more. Also, why not SDRAM [Synchronous Data RAM]? Because all DDR 1,2,3,4,5 is SD, and non-SDRAM for computers is obsolete by 20ish years- although I'm sure there is non-SD RAM for other applications."*






## References 
 
