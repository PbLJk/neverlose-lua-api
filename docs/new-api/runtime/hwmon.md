> Reference specification from docs.zip. This page is NOT a claim that every listed API is implemented in betav3. See the compatibility page.

[Compatibility](../../compatibility.md) · [Index](../../../README.md)


# Hardware Monitor


## hwmon — global table

Read only values about the frame rate and the hardware of the computer.

The frame rate values are measured over the last second. If a value is not available, it is
`0`.

Load and usage values are fractions. `0` means idle and `1` means 100 percent.


  

### `hwmon.average_fps`

The average frame rate in the last second.


  

### `hwmon.cpu_base_frequency`

The rated maximum frequency of the CPU, in MHz.


  

### `hwmon.cpu_cores`

Information for each logical processor, sorted by `processor_id` and then by `core_id`.


  

### `hwmon.cpu_cores_count`

The number of entries in `cpu_cores`.


  

### `hwmon.cpu_count`

The number of logical processors.


  

### `hwmon.cpu_frequency`

The average current frequency of all logical processors, in MHz.


  

### `hwmon.cpu_load`

The average load of all logical processors, as a fraction. The value can be above `1` when the CPU runs faster than its base frequency.


  

### `hwmon.cpu_max_frequency`

The highest current frequency of a single logical processor, in MHz.


  

### `hwmon.cpu_max_load`

The highest load of a single logical processor, as a fraction.


  

### `hwmon.frame_smoothness`

How even the frame times are, from 0 to 1. A higher value means more even frame times.


  

### `hwmon.gpu_count`

The number of graphics adapters.


  

### `hwmon.gpu_list`

Information for each graphics adapter.


  

### `hwmon.max_fps`

The highest frame rate in the last second.


  

### `hwmon.memory_load`

The part of the physical memory that is in use, as a fraction.


  

### `hwmon.memory_total`

The total physical memory, in megabytes.


  

### `hwmon.memory_usage`

The physical memory that is in use, in megabytes.


  

### `hwmon.min_fps`

The lowest frame rate in the last second.


  

### `hwmon.one_percent_low_fps`

The 1 percent low frame rate. This is the frame rate of the slowest 1 percent of frames in the last second.


## hwmon.CPUCoreInfo — object type

Information about one logical processor.


  

### `hwmon.CPUCoreInfo.core_id`

The index of the logical processor in its processor group.


  

### `hwmon.CPUCoreInfo.frequency_mhz`

The current frequency of this logical processor, in MHz.


  

### `hwmon.CPUCoreInfo.processor_id`

The index of the processor group. On most computers this is `0`.


  

### `hwmon.CPUCoreInfo.usage`

The current load of this logical processor, as a fraction.


## hwmon.GPUAdapterInfo — object type

Information about one graphics adapter.


  

### `hwmon.GPUAdapterInfo.adapter_luid`

The locally unique identifier of the adapter. It is valid until Windows restarts.


  

### `hwmon.GPUAdapterInfo.adapter_name`

The name of the adapter, such as the model of the graphics card.


  

### `hwmon.GPUAdapterInfo.dedicated_vram_mb`

The dedicated video memory of the adapter, in megabytes. It includes system memory that is reserved only for the adapter.


  

### `hwmon.GPUAdapterInfo.device_id`

The PCI device ID.


  

### `hwmon.GPUAdapterInfo.gpu_usage_percent`

The current load of the adapter, as a fraction from 0 to 1.


  

### `hwmon.GPUAdapterInfo.shared_memory_mb`

The system memory that the adapter can share with the CPU, in megabytes.


  

### `hwmon.GPUAdapterInfo.unique_id`

An identifier for the adapter made from its device ID and vendor ID, such as `"0x00002684_0x000010DE"`.


  

### `hwmon.GPUAdapterInfo.vendor_id`

The PCI vendor ID.


## LUID — cdata


  

### `LUID.HighPart`


  

### `LUID.LowPart`


## PLUID — cdata
