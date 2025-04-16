### What is IOT
**1. Micro-controllers**
**2. Single board computers**
**3. Components of IOT Apps**
+ internet : apps that receive/ send data
+ thing : devices that sense/act real world
--> IOT : a bridge *connect to* digital to real world

###### The thing: 
Physical devices --> connect to physical world
**Low power / low cost / low speed** 
Ex: Computer --> run for long periods to gather data (sensors) --> take actions (actuators)
+ Measuring Unit : *Microcontroller*
	+ RAM in kB
	+ Speed in MHz
Ex: Thermostat --> turn off the heating when warm --> on when cold
Now : study the habit --> fit with personal preference

###### The internet:
Consists of apps that:
- Process data 
- Send/receive messages
- Take decisions on request to send to actuators
*Typical setup:*
	- Cloud service intermediary
		- Handle security
		- Interact with sensors on one side
		- Connect to apps on the other
**Two types of connection**:
+ Mesh networks: 
	+ Peer to peer routes --> communicate directly with each other and can pass data between them.
	+ No afraid of corruption of single devices --> it can find other route
+ Star network:
	+ All devices connect to a central hub( gateway, router) 
	+ *However*, if hub fails --> entire network can go down
	+ laptop, phones connected to wifi

## Application
**A Smarter thermostat**
Read data --> data message --> use cloud with AI ==> smart decision

**IOT ON THE EDGE**
+ All IOT don't have to connect to the internet
	+ Edge computing in IoT: **processing data** where it is generated **rather** **than** sending all to *central server or cloud*
		+ Devices are "gateways" capable of processing data locally
		+ IOT can collect to edge devices over local networks (wifi, bluetooth)
+ Mechanism: 
	+ Instead of sending raw data to a distant cloud server, an edge device filters, analyzes, or processes it locally 
	+ Only important data or summarized results are sent to the cloud
	--> Reducing bandwidth usage.
+ **Example:**
	+ Wearable devices analyze heart rate locally and **only alert doctors if an abnormal pattern is detected**.
	+ Security cameras detect motion and **only upload clips when necessary**, instead of streaming 24/7.
**IOT security**
- IOT devices connect to the cloud - if the **cloud security is weak or compromised,** the IoT devices connected to it are also at risk.
	- Hackers can gain control of IoT devices, since all the info are published to the cloud
**Solution** AIR Gapping / air wall / air gap/ disconnected network
+ IS a network security measure for computer
+  a secure computer network is physically isolated from unsecured once

## **Microcontrollers: CPU**
The CPU is a brain of the microcontroller  ( run on clock cycle)
-> 1 instruction per clock tick --> millions or billions of ticks per sec
--> Higher the "speed" the more instructions run/sec

**CPU**
On clock tick --> CPU fetches instruction --> decodes it --> execute the task
+ However, some instructions might take **Multiple clock ticks**

**Memory**
2 types of memory  
+ *Program memory* 
	+ Store your code (program)
	+ Persists when there is no power
+ *RAM* : run the codes where there are powers

>[!Note]
>Memory on PC is **significantly larger** than those on microcontroller
>PC                     --> Giga Bytes
>Microcontroller --> Kilo Bytes
>
>A byte = 1 character or number (0, 255)

Example: 
RAM: 
+ WiO Terminal : 192 kB
+ Base PC = 8 GB
Program Storage:
+ WiO = 4 MB
+ PC = 500 GB
>[!Definition] Microcontroller
>Have general purpose I/O pins (GPIO)
>--> Read INPUT from sensors 
>--> Send data to actuators (actions)

**Average Physical Size**

| Microcontroller                                 | PC CPU                | WiO                 |
| ----------------------------------------------- | --------------------- | ------------------- |
| 1.6mm x 2mm x 1mm                               | 136mm x 145mm x 103mm | 72mm x 57 mm x 12mm |
| MCU small enough to fit in dimple of golf balls |                       |                     |
**FRAMEWORKS & OPERATING SYSTEMS**
Microcontrollers **don't** run the traditional OS 
- They have low speed, memory 
- Perform focused tasks
- So they use frameworks
	- Use tools to build core in a way that will run on target microcontroller
	- Use APIs to talk to peripherals

**REAL TIME OPERATING SYSTEMS (RTOS)**
+ It is designed to handle real-time send/receive message tasks
+ It has MULTITHREADED 
	+ Run multiple blocks of code in parallel, on a single or multiple cores
	+ Read sensors, turn on the pump, display LCD, etc. at the same time
+ RTOS:
	+ Lightweight : core features 
+ Networking:
	+ Communicate securely over the internet
+ GUI : Components for screens

**ARDUINO Microcontroller framework**
+ Arduino is an open source electronics platform combining hardware & software
+ Core setup: 
	+ When board powers up
		+ Run setup() once
		+ Run loop() *continuously* till power off

**Architecture: Event Loop**
*setup* : is for one-time initialization code
	--> connected to wifi, cloud services etc.
*loop*: is for processing code- add delay to save power (sleep/ wake cycle)
	--> sensor read | send /receive messages

>[!Note] Code can be recompiled for new compliant hardware with minimal effort

WiO terminal ? 
--> USE Single-board computer over a mircocontroller

###### Single Board Computers
Example : Raspberry Pi
+ 3 Variants:
	+ Full version:
		+ *Complete single-board computers* (SBCs) with built-in ports (HDMI, USB, Ethernet, etc.) and are often used for prototyping, education, or even as desktop replacements.
	+ Pi "zero":
		+ *ultra-compact and low-cost* boards designed for projects where space and power are critical.
	+ Compute module that can be built into your IOT device:
		+ a variation designed for *industrial and commercial products* where you want the computing power of a Raspberry Pi but in a more **integrated, customizable form factor.**
	
**PROGRAMMING the SBC** (single board computer)
+ There is a WIDE RANGE of programming languages, tools and frameworks
	+ Since they run a FULL operating system 
+ Most common language for IOT Apps = PYTHON
**USE CASE**:
+ SBCs are used for both DEV KITS & Professional deployments
	+ Control hardware
	+ Run complex tasks (machine learning models)
###### COMPARISION

|                   | Microcontroller                                   | Single-board computer                |
| ----------------- | ------------------------------------------------- | ------------------------------------ |
| Purpose           | Single                                            | General                              |
| Processing power  | Low, MHz clock speed \| Often single or dual-core | Higher. GHz clock speeds. Multi-core |
| RAM               | Low - KB                                          | More substantial. GB                 |
| OS                | No OS or RTOS                                     | Full-fledged OS (LINUX)              |
| Power consumption | Low, designed for battery operation               | Higher, require powers               |
| Cost              | Low                                               | High                                 |
| Complexity        | Simpler architecture. Runs dedicated firmware     | More complex. Like desktop computer  |
| Heat              | Low                                               | High - require cooling               |

###### Reason to use one over the other

| Microcontroller         | Single-board computer                 |
| ----------------------- | ------------------------------------- |
| Lower Power consumption | Higher processing power & flexibility |
| Lower Cost              | Operating system & software ecosystem |

FGPA 
+ A **Field-Programmable Gate Array (FPGA)** is a special type of **hardware chip** that you can reconfigure **after manufacturing** to perform different tasks.
+ FPGA allows you to **design custom digital circuits** that run in parallel, making them extremely fast and flexible.
Example: 
+ A CPU processes video frames one at a time, but an FPGA can process multiple pixels **simultaneously**, making it ideal for real-time image processing.