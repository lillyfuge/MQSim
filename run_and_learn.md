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
```
- [ ] 了解整个I/O从host到backend的过程  













I/O流的过程在Host_System类中主要体现在以下几个步骤：
I/O流创建：
在构造函数中，根据提供的参数配置（如流的类型和属性）创建多个I/O流（IO_Flow_Base）。每个流可以是合成流或基于跟踪的流。
合成流的参数包括工作集百分比、请求大小分布等，基于这些参数创建具体的流对象。
跟踪流则使用指定的文件路径读取I/O请求。
I/O流附加到主机系统：
创建的I/O流会被存储在IO_flows向量中，供后续使用。
启动模拟：
在Start_simulation方法中，为每个I/O流设置与SSD的连接。根据SSD的接口类型（NVMe或SATA），初始化相应的提交和完成队列。
如果需要，进行预处理，以确保在正式模拟前SSD状态正确。
执行I/O请求：
在模拟运行期间，I/O流生成请求并将其发送到SSD。每个流会根据其配置（如优先级和地址范围）生成特定的I/O请求。
统计与报告：
I/O流会收集运行期间的统计信息，get_workloads_statistics方法用于提取每个流的统计数据。
在模拟结束时，通过Report_results_in_XML方法将统计信息以XML格式输出，便于分析和记录。



Start LBA
定义：Start LBA 表示请求中数据的起始逻辑块地址。
作用：它指明了从哪个逻辑块开始进行读或写操作。逻辑块是存储设备上的基本访问单位，通常对应于设备上的一小块存储空间（例如，512字节或4KB）。
LBA Count
定义：LBA Count 表示在这个请求中要访问的逻辑块数量。
作用：它指示该请求涉及的逻辑块的数量。例如，如果 LBA Count 为 8，则意味着从 Start LBA 开始，将访问接下来的 8 个逻辑块。

Start LBA: 251016576
LBA Count: 8
LBA如何确定(done)，一个LBA的大小是多少(done)，LBA之后干了什么(?)？

#define SECTOR_SIZE_IN_BYTE 512 一个LBA是512字节

NVME处理IO request
```cpp
void IO_Flow_Base::Submit_io_request(Host_IO_Request* request)
	{
		request->PrintRequestInfo();
		switch (SSD_device_type) {
			case HostInterface_Types::NVME:
				//If either of software or hardware queue is full
				if (NVME_SQ_FULL(nvme_queue_pair) || available_command_ids.size() == 0) {
					waiting_requests.push_back(request);
				} else {
					if (nvme_software_request_queue[*available_command_ids.begin()] != NULL) {
						PRINT_ERROR("Unexpteced situation in IO_Flow_Base! Overwriting an unhandled I/O request in the queue!")
					} else {
						request->IO_queue_info = *available_command_ids.begin();
						nvme_software_request_queue[*available_command_ids.begin()] = request;
						available_command_ids.erase(available_command_ids.begin());
						request_queue_in_memory[nvme_queue_pair.Submission_queue_tail] = request;
						NVME_UPDATE_SQ_TAIL(nvme_queue_pair);
					}
					request->Enqueue_time = Simulator->Time();
					pcie_root_complex->Write_to_device(nvme_queue_pair.Submission_tail_register_address_on_device, nvme_queue_pair.Submission_queue_tail);//Based on NVMe protocol definition, the updated tail pointer should be informed to the device
				}
				break;
		}
	}
```

生成request的函数,是读是写按照比例随机生成的，LBA的大小有两种情况
固定大小: 直接使用平均请求大小 (average_request_size)。
正态分布: 使用正态分布生成一个随机请求大小，如果计算出的大小小于等于0，则设置为1。

根据不同的地址分布策略，决定请求的起始逻辑块地址
Start_LBA的确定：
流式分布: 从上一个地址开始，确保地址不超出设备的结束逻辑块地址 (end_lsa_on_device)。如果超出，循环回到开始地址 (start_lsa_on_device)。
随机热冷分布: 以热区域和冷区域的比例来选择地址。热区域请求占一定比例，冷区域则覆盖剩余比例。
均匀随机分布: 从整个地址空间中随机生成地址。
统计生成的请求数量 (STAT_generated_request_count) 并记录请求的到达时间 (Arrival_time)。

```cpp
	Host_IO_Request* IO_Flow_Synthetic::Generate_next_request()
	{
		if (stop_time > 0) {
			if (Simulator->Time() > stop_time) {
				return NULL;
			}
		} else if (STAT_generated_request_count >= total_requests_to_be_generated) {
			return NULL;
		}
		Host_IO_Request* request = new Host_IO_Request;
		if (random_request_type_generator->Uniform(0, 1) <= read_ratio) {
			request->Type = Host_IO_Request_Type::READ;
			STAT_generated_read_request_count++;
		} else {
			request->Type = Host_IO_Request_Type::WRITE;
			STAT_generated_write_request_count++;
		}

		switch (request_size_distribution) {
			case Utils::Request_Size_Distribution_Type::FIXED:
				request->LBA_count = average_request_size;
				break;
			case Utils::Request_Size_Distribution_Type::NORMAL:
			{
				double temp_request_size = random_request_size_generator->Normal(average_request_size, variance_request_size);
				request->LBA_count = (unsigned int)(ceil(temp_request_size));
				if (request->LBA_count <= 0) {
					request->LBA_count = 1;
				}
				break;
			}
			default:
				throw std::invalid_argument("Uknown distribution type for requset size.");
		}

		switch (address_distribution) {
			case Utils::Address_Distribution_Type::STREAMING:
				request->Start_LBA = streaming_next_address;
				if (request->Start_LBA + request->LBA_count > end_lsa_on_device) {
					request->Start_LBA = start_lsa_on_device;
				}
				streaming_next_address += request->LBA_count;
				if (streaming_next_address > end_lsa_on_device) {
					streaming_next_address = start_lsa_on_device;
				}
				if (generate_aligned_addresses) {
					if(streaming_next_address % alignment_value != 0) {
						streaming_next_address += alignment_value - (streaming_next_address % alignment_value);
					}
				}
				if(streaming_next_address == request->Start_LBA) {
					PRINT_MESSAGE("Synthetic Message Generator: The same address is always repeated due to configuration parameters!")
				}
				break;
			case Utils::Address_Distribution_Type::RANDOM_HOTCOLD:
				// (100-hot)% of requests going to hot% of the address space
				if (random_hot_cold_generator->Uniform(0, 1) < hot_region_ratio) {
					request->Start_LBA = random_hot_address_generator->Uniform_ulong(hot_region_end_lsa + 1, end_lsa_on_device);
					if (request->Start_LBA < hot_region_end_lsa + 1 || request->Start_LBA > end_lsa_on_device) {
						PRINT_ERROR("Out of range address is generated in IO_Flow_Synthetic!\n")
						if (request->Start_LBA + request->LBA_count > end_lsa_on_device) {
							request->Start_LBA = hot_region_end_lsa + 1;
						}
					}
				} else {
					request->Start_LBA = random_hot_address_generator->Uniform_ulong(start_lsa_on_device, hot_region_end_lsa);
					if (request->Start_LBA < start_lsa_on_device || request->Start_LBA > hot_region_end_lsa) {
						PRINT_ERROR("Out of range address is generated in IO_Flow_Synthetic!\n")
					}
				}
				break;
			case Utils::Address_Distribution_Type::RANDOM_UNIFORM:
				request->Start_LBA = random_address_generator->Uniform_ulong(start_lsa_on_device, end_lsa_on_device);
				if (request->Start_LBA < start_lsa_on_device || request->Start_LBA > end_lsa_on_device) {
					PRINT_ERROR("Out of range address is generated in IO_Flow_Synthetic!\n")
				}
				if (request->Start_LBA + request->LBA_count > end_lsa_on_device) {
					request->Start_LBA = start_lsa_on_device;
				}
				break;
			default:
				PRINT_ERROR("Unknown address distribution type!\n")
		}
		
		if (generate_aligned_addresses) {
			request->Start_LBA -= request->Start_LBA % alignment_value;
		}
		STAT_generated_request_count++;
		request->Arrival_time = Simulator->Time();
		DEBUG("* Host: Request generated - " << (request->Type == Host_IO_Request_Type::READ ? "Read, " : "Write, ") << "LBA:" << request->Start_LBA << ", Size_in_bytes:" << request->LBA_count << "")

		return request;
	}
