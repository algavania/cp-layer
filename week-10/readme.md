## Table of Contents

- [Table of Contents](#table-of-contents)
- [Physical Design](#physical-design)
  - [**1. Router 0**](#1-router-0)
  - [**2. Router 1**](#2-router-1)
  - [**3. PC 0**](#3-pc-0)
  - [**4. PC 1**](#4-pc-1)
  - [**5. PC 2**](#5-pc-2)
- [Winbox](#winbox)



## Physical Design
![Switch](../assets/week-10/cisco-mikrotik.png)

### **1. Router 0**
    - Static
        Network     : 192.168.1.0
        Mask        : 255.255.255.0
        Next Hop    : 10.252.108.11
    - Fe 0/0
        IPv4 Address: 10.252.108.1
        Subnet Mask : 255.0.0.0

### **2. Router 1**
    - Fe 0/0
        IPv4 Address: 10.252.108.11
        Subnet Mask : 255.0.0.0
    - Fe 1/0
        IPv4 Address: 192.168.1.1
        Subnet Mask : 255.255.255.0

### **3. PC 0**
    IPv4 Address    : 192.168.1.2
    Subnet Mask     : 255.255.255.0
    Default Gateway : 192.168.1.1

### **4. PC 1**
    IPv4 Address    : 192.168.1.3
    Subnet Mask     : 255.255.255.0
    Default Gateway : 192.168.1.1

### **5. PC 2**
    IPv4 Address    : 192.168.1.4
    Subnet Mask     : 255.255.255.0
    Default Gateway : 192.168.1.1

## Winbox
![](../assets/week-10/winbox%20(1).png)

![](../assets/week-10/winbox%20(2).png)

![](../assets/week-10/winbox%20(3).png)

![](../assets/week-10/winbox%20(4).png)

![](../assets/week-10/winbox%20(5).png)

![](../assets/week-10/winbox%20(6).png)

![](../assets/week-10/winbox%20(7).png)

![](../assets/week-10/winbox%20(8).png)

![](../assets/week-10/winbox%20(9).png)

![](../assets/week-10/winbox%20(10).png)

![](../assets/week-10/winbox%20(11).png)

![](../assets/week-10/winbox%20(12).png)

![](../assets/week-10/winbox%20(13).png)

![](../assets/week-10/winbox%20(14).png)

![](../assets/week-10/winbox%20(15).png)

![](../assets/week-10/winbox%20(16).png)

![](../assets/week-10/winbox%20(17).png)

![](../assets/week-10/winbox%20(18).png)

![](../assets/week-10/winbox%20(19).png)

![](../assets/week-10/winbox%20(20).png)

![](../assets/week-10/winbox%20(21).png)

![](../assets/week-10/winbox%20(22).png)

![](../assets/week-10/winbox%20(23).png)

![](../assets/week-10/winbox%20(24).png)

![](../assets/week-10/winbox%20(25).png)

![](../assets/week-10/winbox%20(26).png)

![](../assets/week-10/winbox%20(27).png)

![](../assets/week-10/winbox%20(28).png)

![](../assets/week-10/winbox%20(29).png)

![](../assets/week-10/winbox%20(30).png)

![](../assets/week-10/winbox%20(31).png)