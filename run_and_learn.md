compiler and run command
```bash
make
./MQSim -i <SSD Configuration File> -w <Workload Definition File>
```
examle
>./MQSim -i ssdconfig.xml -w workload.xml 

the output is workload_scenario_1.xml.


workload.xml
```xml
<MQSim_IO_Scenarios>：根元素包含了所有的I/O场景。
<IO_Scenario>：表示一个I/O场景，可以包含多个<IO_Flow_Parameter_Set_Synthetic>或<IO_Flow_Parameter_Set_Trace_Based>子元素。
<IO_Flow_Parameter_Set_Synthetic>：定义了一个基于合成（synthetic）生成器的I/O流参数集。这些参数用于生成模拟的I/O请求。
<Priority_Class>：定义了I/O请求的优先级。

<Device_Level_Data_Caching_Mode>：定义了设备级别的数据缓存模式。

<Channel_IDs>、<Chip_IDs>、<Die_IDs>、<Plane_IDs>：定义了模拟中使用的通道、芯片、晶片和平面的ID。

<Initial_Occupancy_Percentage>：定义了存储设备的初始占用百分比。

<Working_Set_Percentage>：定义了工作集大小的百分比。

<Synthetic_Generator_Type>：定义了合成生成器的类型。

<Read_Percentage>：定义了读请求的百分比。

<Address_Distribution>：定义了地址分布的类型。

<Percentage_of_Hot_Region>：定义了热点区域的百分比。

<Generated_Aligned_Addresses>：表示生成的地址是否对齐。

<Address_Alignment_Unit>：定义了地址对齐的单位。

<Request_Size_Distribution>：定义了请求大小的分布类型。

<Average_Request_Size>：定义了平均请求大小。

<Variance_Request_Size>：定义了请求大小的方差。

<Seed>：定义了随机数生成器的种子。

<Average_No_of_Reqs_in_Queue>：定义了队列中平均请求的数量。

<Intensity>：定义了I/O流的强度。

<Stop_Time>：定义了模拟的停止时间。

<Total_Requests_To_Generate>：定义了要生成的总请求数。

<IO_Flow_Parameter_Set_Trace_Based>：定义了一个基于跟踪（trace-based）生成器的I/O流参数集。这些参数

用于从跟踪文件中生成I/O请求。

<File_Path>：定义了跟踪文件的路径。

<Percentage_To_Be_Executed>：定义了要执行的跟踪文件的百分比。

<Relay_Count>：定义了中继计数。

<Time_Unit>：定义了时间单位。