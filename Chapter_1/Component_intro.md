# Component Introduction

The RT-Thread platform includes a wide array of components that, when activated, facilitate the integration of advanced functionalities, enabling the development of sophisticated embedded systems. It has various per-integrated components, such as C Libraries, network modules, FinSh console components,FAL components,
ulog components and others. Furthermore, RT-Thread provides a comprehensive selection of software packages that can be easily incorporated into projects through online access.

### C Library (LIBC)
The LIBC provided by RT-Thread are consist of three components: 1) compiler's built-in LIBC leveling layer 2) POSIX layer 3) Supporting layers

#### RT-Thread LIBC Architecture Diagram
![image](https://github.com/user-attachments/assets/849f47ec-8612-4c64-a249-c3356f487d2e)

The LIBC leveling layer is responsible for the interface with low level stub fuction of compiler's built-in LIBC and addressing the difference in the implementation of LIBC APIs across various compilers. It provides unified interface for the upper POSIX layer and it is located in components/libc/compiler directory. The need for the leveling arises from the varying level of support for Standard C library function among the built-in LIBC of four different compiler toolchains:

1)GCC 

2)Keil-MDK

3)IAR

4)Visual Studio(WIN32)

LIBC leveling layer ensure that standard C libraries provided by these four toolchains are balanced to consistent level. This leveling process requires no manual intervention from the user; it occurs automatically during project compilation based on the user's chosen platform and toolchain. Thus user can reference the LIBC functions using common header file without needing to differentiate between various compilers and toolchains. With the support of the LIBC library, RT-Thread can operate independently without relying on other third-party libraries. Additionally, due to RT-Thread's extensive support for the POSIX standard, application code developed using the RT-Thread POSIX interface can be easily ported to other platforms that also support POSIX standards.

## Network Framework
As a real-time operating system(RTOS) with extensive network support, RT-Thread provide the net componet to facilitate device connectivity. This component is located in the ./rt-thread/components/net directory. The selection and configuration of network functionalities fall under the management scope of the Kconfig file.

#### RT-Thread Network Components
![image](https://github.com/user-attachments/assets/a57f3d58-dfbe-4412-87d2-e14daf5e957e)

The commonly used functionalities such as AT,LwIP,Netdev and SAL are also loacted in ./rt-thread/components/net directory. These four foundational components enable a wide variety of network devices. They support various wired networking methods, which includes Ethernet interfaces, PHY-equipped ENC28J60,RJ45 Interface and W5500 modules that comes with their own network protocol stack.  All of these can be configured to meet device connectivity requirements through the net component. Wired Connectivity are more options for wireless networking. These includes 2G, 3G, 4G, CAT-1, CAT-4, NB-IoT, and even 5G is relayed on the base station operation for network access. Ex. SIM800, EC20, AIR720, L610, N58 and M5311 modules. Also wifi connectivity are enabled in the module such as ESP,W60x and RW007 which do not requires operator services.
Most functionalities for the network devices are rely on core capabilities: AT and LwIP. For users and developers, the primary concept is Socket Abstraction layer(SAL).

#### RT-Thread SAL Abstraction Layeer
![image](https://github.com/user-attachments/assets/6148ced2-a517-4a55-8652-33e0908b91d7)

SAL provides a programming interface commonly knows as socket interface.Through SAL interface user can use tools such as MQTT(MQ Telemetry Transport), NTP(Network Time Protocol), TFTP(Trivial File Transfer Protocol), TCP Client, TCP Server, WebClient, UDP Client, UDP server and WebNet. For example user can access website using WebClient,simulate Website using WebNet, Connect to various cloud platforms using MQTT, obtain precise time synchronization using NTP and transfer files over TFTP.


## FinSh Console

In the early days of computing, prior to the advent of graphical systems, there were no mice or even keyboards. How did people interact with computers back then? The earliest computers accepted commands via punched cards to input instructions and programs. As computers evolved, monitors and keyboards became standard components. However, operating systems at that time still did not support graphical interfaces. To bridge this gap, pioneers developed software that accepted user-input commands, interpreted them, and relayed them to the operating system, returning the results back to the user. This program acted as a shell, enveloping the operating system.

Embedded devices often require communication between development boards and PCs, utilizing common connection methods such as serial ports, USB, Ethernet, and Wi-Fi. A flexible shell should support operation over various connection interfaces.  With a shell, a communication bridge is established between developers and the computer, allowing developers to easily access system status and control its operation via commands. This is especially beneficial during the debugging phase, as the shell enables developers to quickly identify issues and invoke test functions, adjust parameters, and reduce the frequency of code uploads, ultimately shortening project development time.

## Virtual File System

In early embedded systems, data storage requirements were minimal, and the data types were fairly simple. It was common to store data by writing directly to specific addresses in the storage device. However, as embedded devices evolved and their functionality expanded, the volume and complexity of data grew significantly. Those old method of data storage become difficult,thus new method of data management was needed to simplify the data organization-this is where file systems comes in. A file system is the abstract data type, that impliment the storage, organization, access and data retrival. It servers mechanism that provides user to access underlying data. The basic unit of storage in most file systems is the file, meaning that data is organized in the form of individual files. As the number of files increases, issues such as difficulty in categorization and file name conflicts may arise. To address this, directories (or folders) serve as containers that hold multiple files, helping to organize and manage them more effectively.

#### File system Directory structure
![image](https://github.com/user-attachments/assets/7afef223-c189-4fac-ad47-a4da0f1ae707)

#### Device file system (DFS)
DFS is the virtual file system components provided by RT-Thread. The file system uses naming conventions similar to UNIX-style files and directories. 
In RT-Thread's DFS (Device File System), the file system has a unified root directory, represented by "/". For example, a file named f1.bin in the root directory is referenced as /f1.bin, while a file f1.bin in the 2018 directory is referenced as /data/2018/f1.bin. The directory separator is "/", which is identical to UNIX/Linux but differs from Windows, where "" is used as the directory separator.

The RT-Thread DFS (Device File System) component offers several key features:

1) Provides a unified POSIX interface for file and directory operations, such as read, write, and  poll/select.

2) Supports various types of file systems, including FatFS, RomFS, DevFS, and manages regular files, device files, and network file descriptors.

3) Supports multiple types of storage devices, such as SD cards, SPI Flash, and NAND Flash.

#### Architecture of DFS
The architecture of DFS is primarly divided into three layers.

1) The POSIX Interface Layer: DFS supports the standard POSIX interface. POSIX stands for Portable Operating System Interface of UNIX. It is a set of standards defined by IEEE that specifies the interface an operating system should provide to applications. The POSIX standard is a collection of API specifications designed to ensure software compatibility across different UNIX-based operating systems.
2) The Virtual System Layer: Users can register specific file systems to DFS, such as FatFS, RomFS, DevFS, etc.
3) The Device Abstraction layer: The device abstraction layer abstracts physical devices such as SD Card, SPI Flash, and Nand Flash into devices that are accessible to the file system.

#### The Structure of File System Directory
![image](https://github.com/user-attachments/assets/08db9125-5767-47e8-9c6b-0fdbbad6432a)

### POSIX Layer Interface

The goal of POSIX standard to achieve the seource code level portability. In simple words the program written for a POSIX-compliant operating sysetm should be compile and run on other POSIX-Compliant system even if a different vendor. Since RT-Thread using POSIX Interface, the program written in Linux/Unix to RT-Thread operating system. In Unix-like systems, regular files, device files, and network file descriptors are treated as the same type of file descriptor. RT-Thread achieves this uniformity through DFS (Device File System). With this unified file descriptor mechanism, we can use the poll and select interfaces to perform unified polling across these different types of descriptors, simplifying program development. The poll and select interfaces allow a blocking operation to monitor a group of non-blocking I/O devices for events (such as readiness to read, readiness to write, priority error output, error occurrence, etc.) until one device triggers an event or a specified timeout is reached. This mechanism helps developers identify ready devices, reducing the complexity of programming.

### Virtual File System Layer
User can register specific file system to DFS in RT-Thread such as FatFS, RomFS, DevFS and others

1) FatFS: A file system compatible with Microsoft's FAT format, specifically designed for the small embedded devices. Written in ANSI C it has excellent portability and hardware independance, making it widely used file system type in RT-Thread.

2) RomFS: A traditional, simple, and compact read-only file system. It doesn't support dynamic writting but store data sequentially, allowing application to run with XIP(Excute In Place) during system operation saving RAM space.

3) DevFS (Device File System): Allowing devices in RT-Thread system to virtualized as file under the /dev directory. Once enabled, device can be operated using standaed file operation such as read and write.

4) JFFS2(Journaling Flash File System 2): A log based file system primarly used for NOR flash. It operates on MTD(Memory Technology Device) layer and support read/write operation, data compression, hash-table-based journaling, crash/power failure protection, and wear-leveling.

5) NFS(Networking File System): A technology that enables file sharing between different machines and operating systems over a network. During OS development and debugging, NFS can be used to mount a root file system on an embedded device, simplifying modifications to the root file system from the host machine.

6) UFFS(Ultra low cost flash file system): An open-source file system developed specifically for embedded devices with small memory environments using NAND Flash. Compared to other commonly used file systems like YAFFS, UFFS offers lower resource usage, faster boot speeds, and is free to use.

### Device Abstraction Layer:
The device abstraction layer transforms physical devices, such as SD Cards, SPI Flash, and NAND Flash, into devices that the file system can access. For example, the FAT file system requires that the storage device must be of the block device type. Different types of file systems are implemented independently from the storage device drivers. Therefore, only by connecting the underlying storage device's driver interface to the file system can the file system function properly.

### File system mounting method

The file system initialization process generally consists of the following steps:

1) Initialize the DFS component
2) Initialize the specific type of file system
3) Create a block device on the storage medium
4) Format the block device
5) Mount the block device to the DFS directory

When the file system is no longer needed, it can be unmounted.

### Ulog log

Logging involves capturing and outputting information about the software's operational state and process to various media to viewing and storage. This functionality is servers as a functionality for debugging, issue tracking, performance analysis,system monitoring, fault warning.  It can be said that logging usage accounts for at least 80% of a software's lifecycle. For operating systems, the inherent complexity of software makes single-step debugging unsuitable in many scenarios; hence, a robust logging component is virtually standard in operating systems. An effective logging system significantly enhances the efficiency of operating system debugging. ulog is a straightforward and user-friendly C/C++ logging component, with the first letter "u" representing "μ," indicating its micro nature. It achieves a minimal resource footprint with ROM < 1K and RAM < 0.2K. Despite its small size, ulog offers a comprehensive set of features, drawing design inspiration from another open-source C/C++ logging library, EasyLogger (elog), while making significant improvements in functionality and performance. The main features include:

Diverse Output Backends: Supports various output mediums such as serial ports, networks, files, and flash memory

Thread-Safe Design: Logging output is designed to be thread-safe and supports asynchronous output modes

High Reliability: The logging system remains functional even in complex environments like interrupt service routines (ISR) and hard faults

Flexible Output Level Configuration: Supports setting output levels at runtime or compile time

Global Filtering: Log content can be globally filtered by keywords and tags

Compatibility with Linux Syslog: The API and log format are compatible with Linux syslog

Hexadecimal Dumping: Supports dumping debug data to logs in hex format

API Compatibility: Compatible with the logging output API of rtdbg (RT-Thread's earlier logging header file) and EasyLogger

#### RT-Thread Ulog
![image](https://github.com/user-attachments/assets/80dc0ce7-3cc7-403c-9fc2-a4ea3a2b78dc)

FrontEnd: This layer is closest to application layer, and provide users with two types of API Interfaces, Syslog and Log_X

Core: The main work of the middle core layer is to format and file the logs passed by the upper layer, and then generate the log frames and finally output them to the output to the lower-end back-end devices through various output modules.

Backend: After receiving the log frames sent from the core layer, the logs are output to the registered log backend devices, such as files, consoles, log servers, and so on.

### UTEST(Unit Test) Framework

UTEST is a Unit Test Frmework developed for the RT-Thread. The primary design goal of UTEST is to provide RT-Thread developer with a unified framework interface for the writing test programs, enabling the execution of unit tests, coverage tests, and integration tests efficiently. A test case (abbreviated as "tc") is a single test executed to achieve a specific testing objective. It encompasses the test inputs, execution conditions, testing procedures, and expected outcomes, forming a finite loop with clear termination conditions and defined results.

In the UTEST (unit test) framework, user-defined test programs are defined as test cases. Each test case contains a single test case function (similar to a main function) and may include multiple unit test functions.

#### Application Block Diagram of UTEST Framework
![image](https://github.com/user-attachments/assets/c90ce73f-938c-4cf9-861a-daa437c9f140)

Specifically, the test code targeting a particular functionality is considered a test case when implemented using the APIs provided by the utest testing framework.

A test unit refers to a specific testing point derived from the breakdown of the functionality being tested. Each test point serves as the smallest measurable unit of the functionality under examination. It is important to note that different classification methods can yield varying sets of test units. The application block diagram of the utest framework is shown in the figure on the right.

The UTEST testing framework exports all test cases to the UtestTcTab code segment. In the IAR and MDK compilers, there is no need to define the UtestTcTab section in the linker script. However, when using GCC, it is necessary to explicitly set up the UtestTcTab section in the linker script.

Therefore, for test cases to compile and run under GCC, the UtestTcTab code segment must first be defined in the GCC linker script.

To add the definition of the UtestTcTab section in the .text segment of the GCC linker script, use the following format:

```
/* section information for utest */
. = ALIGN(4);
__rt_utest_tc_tab_start = .;
KEEP(*(UtestTcTab))
__rt_utest_tc_tab_end = .;
```


```
msh />utest_list

[14875] I/utest: Commands list :

[14879] I/utest: [testcase name]:components.filesystem.dfs.dfs_api_tc; [run timeout]:30

[14889] I/utest: [testcase name]:components.filesystem.posix.posix_api_tc; [run timeout]:30

[14899] I/utest: [testcase name]:packages.iot.netutils.iperf.iperf_tc; [run timeout]:30

msh />utest_run components.filesystem.dfs.dfs_api_tc

[83706] I/utest: [==========] [ utest    ] started

[83712] I/utest: [----------] [ testcase ] (components.filesystem.dfs.dfs_api_tc) started

[83721] I/testcase: in testcase func...

[84615] D/utest: [    OK    ] [ unit     ] (test_mkfs:26) is passed

[84624] D/testcase: dfs mount rst: 0

[84628] D/utest: [    OK    ] [ unit     ] (test_dfs_mount:35) is passed

[84639] D/utest: [    OK    ] [ unit     ] (test_dfs_open:40) is passed

[84762] D/utest: [    OK    ] [ unit     ] (test_dfs_write:74) is passed

[84770] D/utest: [    OK    ] [ unit     ] (test_dfs_read:113) is passed

[85116] D/utest: [    OK    ] [ unit     ] (test_dfs_close:118) is passed

[85123] I/utest: [  PASSED  ] [ result   ] testcase (components.filesystem.dfs.dfs_api_tc)

[85133] I/utest: [----------] [ testcase ] (components.filesystem.dfs.dfs_api_tc) finished

[85143] I/utest: [==========] [ utest    ] finished
```
#### Analysis of UTEST Execution Results

![image](https://github.com/user-attachments/assets/00e01f64-1cf3-4671-a4be-6b9ac3cf4dd4)


## Online Packages
RT-Thread offers a diverse array of software packages, categorized primarily into following areas: IoT, Peripherals, Systems, Programming Language, Tools, Miscellaneous, Multimedia, Security, Embedded AI, Signal Processing and Control, RTDuino.

1) IoT: The Internet of Things (IoT) category includes software packages that focus on network connectivity, cloud access, and various aspects of digital communication.

2) Peripherals: It category features software packages that enables intraction between external devices. These packages pertain to the underlying peripheral hardware and include sensor-related packages.

3) System: System level software packages are designed to monitor the system behavior and manage file system efficiently.

4) Programming Languages: This category include various programming language, script and interpreters that can be executed in terminal environment.

5) Tools: Various types of software packages intented to use the developement and testing.

6) Miscellaneous: This category encompasses packages that do not fit into any of the aforementioned categories, including demonstrations and examples.

7) Multimedia: Packages for Audio and Video processing in RT-Thread platform.

8) Security: This category includes encryption algorithms and secure transport layer protocols to enhance system security.

9) Embedded AI: RT-Thread's software packages focus on the Embedded AI applications.

10) RTDuino: RTDuino is the core projects of the Arduino ecosystem library that can be directly executed on the RT-Thread operating system via RTDuino.


