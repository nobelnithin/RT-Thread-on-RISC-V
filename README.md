# RT-Thread-on-RISC-V


RT-Thread is a realtime operating system, which is written in C language. RT-Thread has two versions, Standard version and Nano version. For MCU like resource constrained system Nano version is useful because it requires only 3KB flash and 1.2KB RAM memory.

RT-Thread's Architecture 

![image](https://github.com/user-attachments/assets/360864c4-91a5-47df-8452-284756707e9a)

Kernal Layer: 
  RT-Thread Kernal, it is the core part of the RT_Thread, this includes the implimentation of objects in kernal system such as multithreading and it's time scheduling, semophore, mail box message queue, memory management, timer etc. libcpu/BSP (Chip Migration related files/Board support package) is closely related to hardware and consist of peripheral drivers and CPU Porting.

Components and Service Layer: 
  Components are based on upper-level software on top of the RT-Thread kernel, such as [virtual file systems]([url](https://www.ibm.com/docs/en/aix/7.2.0?topic=concepts-virtual-file-systems)), [FinSH command line interface]([url](https://www.rt-thread.io/document/site/programming-manual/finsh/finsh/)) or console, device framework, Network Framework etc. 

Open software Package Platform: 
  Supports over 700 general purpose components to facilitate rapid developement for application developement.
