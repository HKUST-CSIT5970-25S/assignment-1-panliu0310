[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/IAASVEAZ)
# CSIT5970 Assignment-1: EC2 Measurement (2 questions, 4 marks)

### Deadline: 11:59PM, Feb, 28, Friday

---

### Name: Liu Hoi Pan
### Student Id: 21099999
### Email: hpliu@connect.ust.hk

---

## Question 1: Measure the EC2 CPU and Memory performance

1. (1 mark) Report the name of measurement tool used in your measurements (you are free to choose *any* open source measurement software as long as it can measure CPU and memory performance). Please describe your configuration of the measurement tool, and explain why you set such a value for each parameter. Explain what the values obtained from measurement results represent (e.g., the value of your measurement result can be the execution time for a scientific computing task, a score given by the measurement tools or something else).

    > The measurement tool I used would be Phoronix Test Suite. The CPU test I used is 7-zip compression (pts/compress-7zip). The Memory test I used is ramspeed (pts/ramspeed).

    > For CPU test, the configurations of the measurement tools are all from default. I didn't set anythings. For Memory test, I choose to test on "Copy Integer". I don't have concern on choosing which parameters but just randomly choose the first options in type and benchmark. I would like to make the test as simple as possible, just need to make sure it is fair - I will use same test on different instance type.

    > For CPU test, the results obtained by 7-zip compression test is in the unit of MIPS (Millions of Instructions per Second). Higher means better performance. 3 times of compression tests and decompression tests are performed in default. I take the average result from compression test only. For Memory test, the results obtained by ramspeed test is in the unit of MB/s (MegaBytes per second). Higher means better performance. 3 times of "Copy Integer" test is performed and the average result is taken.

2. (1 mark) Run your measurement tool on general purpose `t2.micro`, `t2.medium`, and `c5d.large` Linux instances, respectively, and find the performance differences among these instances. Launch all the instances in the **US East (N. Virginia)** region. Does the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource?

    In order to answer this question, you need to complete the following table by filling out blanks with the measurement results corresponding to each instance type.

    | Size        | CPU performance | Memory performance |
    | ----------- | --------------- | ------------------ |
    | `t2.micro` |3694 MIPS        |10728.23 MB/s       |
    | `t2.medium`  |10059 MIPS       |20131.71 MB/s       |
    | `c5d.large` |7060 MIPS        |12355.98 MB/s       |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI.

    > t2.micro has 1 vCPU and 1 GiB Memory. t2.medium has 2 vCPU and 4 GiB Memory. c5d.large has 2 vCPU and 4 GiB Memory. The performance of EC2 instances increase with the number of vCPUs and memory resource increases, but it is not commensurate. Note that t2.medium and c5d.large share same numbers of vCPUs and memory resource, but t2.medium has a better performance.

## Question 2: Measure the EC2 Network performance

1. (1 mark) The metrics of network performance include **TCP bandwidth** and **round-trip time (RTT)**. Within the same region, what network performance is experienced between instances of the same type and different types? In order to answer this question, you need to complete the following table.

    | Type                      | TCP b/w        | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | `t3.medium` - `t3.medium` |3.26 Gbps/sec   |0.383     |
    | `m5.large` - `m5.large`   |4.88 Gbps/sec   |0.282     |
    | `c5n.large` - `c5n.large` |4.96 Gbps/sec   |0.132     |
    | `t3.medium` - `c5n.large` |2.13 Gbps/sec   |0.805     |
    | `m5.large` - `c5n.large`  |3.23 Gbps/sec   |0.469     |
    | `m5.large` - `t3.medium`  |1.77 Gbps/sec   |0.941     |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. Note: Use private IP address when using iPerf within the same region. You'll need iPerf for measuring TCP bandwidth and Ping for measuring Round-Trip time.
    
    > Same type of instances have better network performance than that of different instances.

2. (1 mark) What about the network performance for instances deployed in different regions? In order to answer this question, you need to complete the following table.

    | Connection                | TCP b/w        | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | N. Virginia - Oregon      |31.2 Mbps/sec   |64.332    |
    | N. Virginia - N. Virginia |9.46 Gbps/sec   |0.098     |
    | Oregon - Oregon           |4.94 Gbps/sec   |0.153     |
 
    > Region: US East (N. Virginia), US West (Oregon). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. All instances are `c5.large`. Note: Use public IP address when using iPerf within the same region.

    > The network performance of instances deployed in different regions is much worse than that of instances deployed in the same region.
