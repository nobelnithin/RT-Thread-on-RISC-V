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





