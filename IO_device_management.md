# I/O Device Management Framework
The majority of embedded device includes various Input/Output devies. Ex. Display screen on Consumer/Insturmentation products, Serial Communication interface on industrial equipment, Flash memory or SD card used for data aquisition devices, Ethernet interface on network equipments. RT-Thrread treats peripherals scuch as PIN, USB, UART, I2C and SPI all these are managed through unified device registration system. It implements device management subsystems that enable access by name, allowing hardware device to access through API Interface. On the device driver interface, an event is attached to the different devices. When this device event is triggered, the driver notifies the upper-layer application accordingly.

### Device Driver Framework in RT-Thread
![image](https://github.com/user-attachments/assets/8ef1da30-9aa4-4d25-9d9a-43c67bbb9438)

The device object of RT-Thread is built upon the kernel object, where all the devices are regarded as class of object and fall under the object manager's scope. Each device object is derived from a base object, allowing each specific device to inherit attributes from its parent class while also deriving its own private attributes.

### Inheritance and Derivation Relationships of Device Objects Diagram
![image](https://github.com/user-attachments/assets/1c999259-5608-4bdb-9644-b5681cb71d21)


