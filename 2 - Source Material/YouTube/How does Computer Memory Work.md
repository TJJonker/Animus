2024-06-30 | 21:16
**Source:** [How does Computer Memory Work](https://www.youtube.com/watch?v=7J7X7aZvMXQ&pp=ygUdaG93IGRvZXMgY29tcHV0ZXIgbWVtb3J5IHdvcms%3D) 
**Status:** #alpha #beta #release
**Tags:** 

DRAM is an abbreviation for Dynamic Random Access Memory, which is otherwise known as 'main memory' or 'working memory'.  In order to use data, it needs to be moved from any long term storage module to the DRAM. 

Long term storage permanently stores data in massive 3D arrays, while DRAM temporarily stores data in 2D arrays. Fetching data from an SSD can take 50 microseconds (10$^-$$^6$ seconds), while fetching data from DRAM takes 17 nanoseconds (10$^-$$^9$ seconds), which makes DRAM data fetching about 3000 times faster. 

Downsides of DRAM is that it requires power to maintain and refresh its data, and that it stores a single bit per memory cell in a 2D array. Because of the power requirement, shutting down the computer will reset DRAM data. Regarding the storage, storing a single bit per memory cell is space inefficient, requiring large physical space on the module to store bigger chunks of data. 

The CPU will use data by moving the data from the SSD to the DRAM and prefetching the data to the CPU's cache. Prefetching is the process of fetching data before it is used in order to eliminate the overhead of having to fetch the data right before it is used.

>*"Why is it called Dynamic Random Access Memory? Also, why didn't we just call it RAM or just Memory throughout the video? Well, Random Access, means the computer can access any section of data with an equal amount of time before the data is read or written compared to any other section. The opposite is Linear Access Memory, which like a cassette tape. It's 'Dynamic' because the data cells lose charge over time, and thus have to be refreshed multiple times a second. Finally, we didn't call it RAM, because there are many types of RAM. SSDs are technically NVRAM [Non-Volatile RAM] Cache memory in the CPU is SRAM [Static RAM], GPUs use VRAM [Video RAM], which is VERY close in design to DRAM, and additionally there lesser known ones like MRAM [Magnetoresistive RAM] , and many more. Also, why not SDRAM [Synchronous Data RAM]? Because all DDR 1,2,3,4,5 is SD, and non-SDRAM for computers is obsolete by 20ish years- although I'm sure there is non-SD RAM for other applications."*

A stick of DRAM is also called a DIMM (Dual Inline Memory Module). The black squares on the DRAM are the DRAM chips, which there are often 8 of on a stick. Most generic motherboards have 4 DIMM slots, holding space for 4 DRAM modules. The DIMM slots directly connect the DRAM with the CPU via two memory channels that run on the motherboard. The left two DIMM slots share the same memory channels, and the right two share other memory channels.

The CPU contains a memory controller called a DRAM interface, which communicates with the DRAM. The CPU also has a separate section responsible for communication with long term storage like M2 and SATA SSDs. Along with data mapping tables, the CPU manages the dataflow from SATA to DRAM and from DRAM to local cache storage. 

DRAM in DDR5 is split up into two channels (Channel A and Channel B). Both channels independently move 32 bits of memory using 32 data wires, 21 additional wired to define read and/or write addresses and over 7 control signal wires, commands are relayed. Since each DRAM stick contains 4 memory chips, bandwidth has to be shared between the 4 chips, meaning every chip can transfer 8 bits of memory in parallel. The required power to run DRAM is provided by the motherboard and internally managed by the DRAM.

Inside a memory chip, 32 data banks can be found, each with a size of 65536 rows and 8192 columns. Each cell here represents a data cell that can hold a single bit while powered. Using a 31 bit address, we can define the data address we want to retrieve. The first three bits are used for specifying the bank group, the next two for the databank and the next 16 bits (2$^1$$^6$ = 65536) for specifying the row. Since the bandwidth is 8 bit, the memory will be retrieved per 8 bits, which can be done with the last 10 bits. (8192 / 8 = 1024 = 2$^1$$^0$)  

Inside a memory chip, 32 data banks can de found, each with a size of 65536 x 8192 data cells, forming a grid structure. Using a 32 bit address, the first three bits are used to select the bank group, the next two bits to select the bank, 16 bits exact row.
```python
DRAM Chip
+-----------------------------------------------------------------------------+
|  Bank Group 0                                                               |
|  +-----------------------------------------------------------------------+  | 
|  |    Bank 0       |    Bank 1       |    Bank 2       |    Bank 3       |  |
|  |    +-------+    |    +-------+    |    +-------+    |    +-------+    |  |
|  |    | Row 0 |    |    | Row 0 |    |    | Row 0 |    |    | Row 0 |    |  |
|  |    | Cell  |    |    | Cell  |    |    | Cell  |    |    | Cell  |    |  |
|  |    | ...   |    |    | ...   |    |    | ...   |    |    | ...   |    |  |
|  |    | Row N |    |    | Row N |    |    | Row N |    |    | Row N |    |  |
|  |    +-------+    |    +-------+    |    +-------+    |    +-------+    |  |
|  +-----------------------------------------------------------------------+  |
|                                                                             |
|  Bank Group 1                                                               |
|  +-----------------------------------------------------------------------+  |
|  |    Bank 0       |    Bank 1       |    Bank 2       |    Bank 3       |  | 
|  |    +-------+    |    +-------+    |    +-------+    |    +-------+    |  | 
|  |    | Row 0 |    |    | Row 0 |    |    | Row 0 |    |    | Row 0 |    |  | 
|  |    | Cell  |    |    | Cell  |    |    | Cell  |    |    | Cell  |    |  | 
|  |    | ...   |    |    | ...   |    |    | ...   |    |    | ...   |    |  | 
|  |    | Row N |    |    | Row N |    |    | Row N |    |    | Row N |    |  | 
|  |    +-------+    |    +-------+    |    +-------+    |    +-------+    |  | 
|  +-----------------------------------------------------------------------+  |
|                                                                             |
|  Bank Group 2 ... 7                                                         | 
|                                                                             |
+-----------------------------------------------------------------------------+
```






## References 
 
