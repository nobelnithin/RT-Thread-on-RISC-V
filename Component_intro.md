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

The commonly used functionalities such as AT,LwIP,Netdev and SAL are also loacted in ./rt-thread/components/net directory. These four foundational components enable a wide variety of network devices. 

