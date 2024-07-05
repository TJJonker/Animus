2024-06-30 | 21:16
**Source:** [How does Computer Memory Work](https://www.youtube.com/watch?v=7J7X7aZvMXQ&pp=ygUdaG93IGRvZXMgY29tcHV0ZXIgbWVtb3J5IHdvcms%3D) 
**Status:** #beta
**Tags:** [[Computer Hardware]]

DRAM is an abbreviation for Dynamic Random Access Memory, which is otherwise known as 'main memory' or 'working memory'.  In order to use data, it needs to be moved from any long term storage module to the DRAM. 

Long term storage permanently stores data in massive 3D arrays, while DRAM temporarily stores data in 2D arrays. Fetching data from an SSD can take 50 microseconds (10$^-$$^6$ seconds), while fetching data from DRAM takes 17 nanoseconds (10$^-$$^9$ seconds), which makes DRAM data fetching about 3000 times faster. 

Downsides of DRAM is that it requires power to maintain and refresh its data, and that it stores a single bit per memory cell in a 2D array. Because of the power requirement, shutting down the computer will reset DRAM data. Regarding the storage, storing a single bit per memory cell is space inefficient, requiring large physical space on the module to store bigger chunks of data. 

The CPU will use data by moving the data from the SSD to the DRAM and prefetching the data to the CPU's cache. Prefetching is the process of fetching data before it is used in order to eliminate the overhead of having to fetch the data right before it is used.

>*"Why is it called Dynamic Random Access Memory? Also, why didn't we just call it RAM or just Memory throughout the video? Well, Random Access, means the computer can access any section of data with an equal amount of time before the data is read or written compared to any other section. The opposite is Linear Access Memory, which like a cassette tape. It's 'Dynamic' because the data cells lose charge over time, and thus have to be refreshed multiple times a second. Finally, we didn't call it RAM, because there are many types of RAM. SSDs are technically NVRAM [Non-Volatile RAM] Cache memory in the CPU is SRAM [Static RAM], GPUs use VRAM [Video RAM], which is VERY close in design to DRAM, and additionally there lesser known ones like MRAM [Magnetoresistive RAM] , and many more. Also, why not SDRAM [Synchronous Data RAM]? Because all DDR 1,2,3,4,5 is SD, and non-SDRAM for computers is obsolete by 20ish years- although I'm sure there is non-SD RAM for other applications."*

A stick of DRAM is also called a DIMM (Dual Inline Memory Module). The black squares on the DRAM are the DRAM chips, which there are often 8 of on a stick. Most generic motherboards have 4 DIMM slots, holding space for 4 DRAM modules. The DIMM slots directly connect the DRAM with the CPU via two memory channels that run on the motherboard. The left two DIMM slots share the same memory channels, and the right two share other memory channels.

The CPU contains a memory controller called a DRAM interface, which communicates with the DRAM. The CPU also has a separate section responsible for communication with long term storage like M2 and SATA SSDs. Along with data mapping tables, the CPU manages the dataflow from SATA to DRAM and from DRAM to local cache storage. 

DRAM in DDR5 is split up into two channels (Channel A and Channel B). Both channels independently move 32 bits of memory using 32 data wires, 21 additional wired to define read and/or write addresses and over 7 control signal wires, commands are relayed. Since each DRAM stick contains 4 memory chips, bandwidth has to be shared between the 4 chips, meaning every chip can transfer 8 bits of memory in parallel. The required power to run DRAM is provided by the motherboard and internally managed by the DRAM.

Inside a memory chip, 32 data banks can be found, each with a size of 65536 rows and 8192 columns. Each cell here represents a data cell that can hold a single bit while powered. Using a 31 bit address, we can define the data address we want to retrieve. The first three bits are used for specifying the bank group, the next two for the databank and the next 16 bits (2$^1$$^6$ = 65536) for specifying the row. Since the bandwidth is 8 bit, the memory will be retrieved per 8 bits, which can be done with the last 10 bits. (8192 / 8 = 1024 = 2$^1$$^0$)  

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


### Memory Cell
The memory cell inside DRAM is called a '1T1C DRAM Memory Cell'. It contains a single Transistor to read or write data and a single Capacitator to store data. The cell is connected to two lines: the wordline, which enables the channel, and the bitline, which can read or change the value of the cell when the channel is enabled.

Over every row spans a wordline, and over every column spans a bitline, creating a grid like structure. If a single wordline and 8 consecutive bitlines are enabled, we can read or update the content of these 8 cells. The ends of every bitline is connected to the Column Multiplexer which, depending on the last 10 bits of the memory address, connects these bitlines to the I/O Data Wires of the chip.

#### Reading
To detect the content of a cell, a wordline is enabled and the bitlines are prepared with a voltage of 0,5V. At the end of the bitline, a Sense Amplifer is placed to amplify the signal form the bitline. When a cell channel is opened and the cell holds 1V, the bitline will slowly drain the content of the cell. The Sense Amplifier will sense the change of current through the bitline and set the bitline to 1, recharging the cell again. The opposite happens when the cell holds 0V; the cell will drain charge from the bitline, the Sense Amplifier senses the change and drain all the current from the bitline, discharging the cell in its process. All the charges of the Sense Amplifier are read and sent to the read driver on the chip.

#### Writing
Setting the charge of the cells happens in mostly the same way. A single wordline is enabled and the content is read through the bitlines, by the Sense Amplifiers. Instead of linking the Sense Amplifiers to the read driver, they're linked to the write driver, which takes the data from the CPU and overrides the Sense Amplifiers, which will charge/discharge the cells.

#### Refreshing
Refreshing is done by precharging all the bitlines and, row by row, open every wordline, read the content, amplify the content with the Sense Amplifier, taking about 50ns for each row, totaling to about 3ms per refresh. Refreshing happens at least once every 64ms since that's how look it would take for a cell to idle discharge and lose its content. 

> **Note that the charge of 1V and ,5V is used for ease of use. In reality, the charge differs between the DDR version. The different charges can ben read in the table below**:

|       | Full charge | Bitline precharge | Empty charge |
| ----- | ----------- | ----------------- | ------------ |
| DDR-5 | 1.1V        | 0.55V             | 0V           |
| DDR-4 | 1.2V        | 0.6V              | 0V           |
| DDR-3 | 1.5V        | 0.75V             | 0V           |
| DDR-2 | 1.8V        | 0.9V              | 0V           |
| DDR-1 | 2.5V        | 1.25V             | 0V           |

#### Row hit optimization 
Opening and closing rows takes (relatively speaking) a lot of time. When a row is already open and different bitlines are read from the same row, It's called a row hit. If a different row needs to be opened, it's called a row miss. On a package, a couple of analytics can be found which are measured in clock cycles:
- **Cas Latency:** Time for a row hit
- **RAS to CAS Delay**: Time for a column to open if the bitlines are precharged and wordlines are isolated
- **Precharge:** Time to precharge
- **Active to Precharge Delay:** Accumulated time to open a column and read hit a row

Row hits can easily be recognized by splitting the address into two parts, where the first 21 bits are the RAS (Row Address Strobe) and the next 10 bits are the CAS (Column Address Strobe). If the RAS is the same as the current selected/opened row, the CAS only has to be sent to the Column Multiplexer, which can easily link the requested columns to the right driver. To increase the likelihood of a row hit, the CPU, programs and compilers are optimize to increase the number of subsequent row hits. The DRAM helps optimizing the likelihood of row hits by allowing every memory bank to independently keep a Row open. 

Another optimization is regarding the refreshing, which, again, can take about 3ms. Since the DRAM is working with bank groups of 4 memory banks. Every time a refresh is necessary, the CPU can refresh one bank in each bank group at a time, while using the other three, reducing the impact of refreshing.

#### Burst buffer
The concept of a burst buffer it to place a buffer between the Column Multiplexer and the drivers. Instead of reading 8 bits at a time, N columns can be read, temporarily stored inside the buffer and send to the CPU in quick succession. The same goes for writing: The CPU can sent a bigger chunk of data to the DRAM, which can read from the buffer and quickly change the content of the memory bank. Since all the read and write commands can be executed in a single action, the burst buffer improves the overall performance of reading and writing.

#### Subdividing
Since the bitlines are long, the capacitator of the cells has to be big to accord for the long distance they need to travel to the Sense Amplifier. The same checks out for the wordline: bigger wordlines mean longer times to enable all the channel transistors. To tackle this, each memory bank is split up into chunks of 1024 by 1024, with a Sense Amplifier at the end of every chunk and the use of wordline division and a 'hierarchical row decoder' to reduce the charge, thus the time, necessary to open all channels. 

#### Differential Pair
Another optimization is the creation of a Differential Pair. Each bitline is split up into two bitlines, connecting to the same Sense Amplifier. The cells now alternate between the left and the right bitline, using just the bitline which they're connected to. Inside the Sense Amplifier, a [[Cross-Coupled Inverter]] can be found, which inverts the charge of the first bitline and outputs the result to the other bitline. Since no other cell's channel transistor is active, it won't change the charge of any other cell. There are three benefits to this design:
1. Since one bitline is always charged and the other is always discharged, precharging can simply be done by establishing a connection between the two bitlines, evening out the charge, which results in the precharge charge, which is always half of a full charge. (See table above)
2. Since the two bitlines are now two oppositely charged wires, an electric field is created between the two wires, which can reduce the amount of electric fields emitted in stray directions, thus creating Noise Immunity and reducing Parasitic Capacitance.