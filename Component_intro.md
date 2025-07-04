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
