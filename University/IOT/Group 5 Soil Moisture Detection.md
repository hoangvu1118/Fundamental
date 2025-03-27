## Importance of soil moisture
Water is vital for plants since
+ Optimal plant growth 
+ Boosts Crop Yield 
+ Prevents Water Waste

## Ways to measure soil moisture
**Two types of soil moisture sensors**
+ Resistive sensor
	+ Two probes measure electrical resistance in the soil
	+ Lower resistance -> higher Moisture
+ Capacitive sensor
	+ Measures soil's ability to store electric charge(capacitance - điện dung)
	+ Higher moisture = Lower voltage output
![[Pasted image 20250327231256.png]]

## How sensors communicate with IoT devices 
### General Purpose Input Output (GPIO) pins
- Each GPIO pin can be **configured as Input or Output**.
- When set as **Input**: Reads data from sensors like buttons.
- When set as **Output**: Controls LEDs, relays, or motors.

+ ANALOG PINS CAN SEND OR RECEIVE A VOLTAGE FROM 0 TO 3V3 OR 5V 
+ INPUT PINS USE AN ADC TO CONVERT TO 10-BIT NUMBER (0 - 1023) 
+ OUTPUT PINS USE AN DAC TO CONVERT FROM A 10-BIT NUMBER (0 - 1023)

### I$^2$C (Inter-Integrated Circuit)
- A **serial communication protocol** for connecting multiple devices using only **two wires**:
    - **SDA (Serial Data Line)**
    - **SCL (Serial Clock Line)**
    - Two more wires - VCC & GND give power to sensors/modules
    - VCC can be ignored if "slave" has its own power source
- Uses a **master-slave architecture** (one master, multiple slaves).

How it works:
- **Master (e.g., Arduino, Raspberry Pi) initiates communication.**
- It sends the **7-bit or 10-bit address** of the slave device via SDA.
- The **clock signal (SCL) synchronizes data transfer**.
- The slave responds and sends/receives data as needed.

- **SDA and SCL lines** require **pull-up resistors** (typically **4.7kΩ – 10kΩ**) to **VCC**.
- This ensures that the lines are at a **HIGH (1)** state when no device is pulling them down **LOW(0)**.
- ![[Pasted image 20250327233900.png]]
- So when the switch btw VCC and Data is Open --> it will enter "low" state 
- However devices two will receive fluctuated values. Hence the resistor btw GND and Data is needed to set the signal back to 0 

### UART (Universal Asynchronous Receiver/Transmitter)
- A **serial communication protocol** using **TX (Transmit) & RX (Receive) pins**.
- Used for **device-to-device communication** (no clock needed).
- Commonly seen as **RS-232 (Serial Port)**.
#### ⚙ **How it Works?**
- Devices send data **byte-by-byte** at a fixed baud rate (e.g., 9600, 115200 bps).
- No **clock signal**, so both devices must agree on:
    - Baud rate
    - Start/stop bits
    - Parity settings

### SPI (Serial Peripheral Interface)
A **high-speed serial protocol** using **4 lines**:
- **MOSI (Master Out, Slave In)**
- **MISO (Master In, Slave Out)**
- **SCK (Serial Clock)**
- **SS (Slave Select)** : Select which slaves(devices) to communicate
#### **How it Works?**
- The **master device** generates the clock.
- Data is sent simultaneously between master and slave.
- Faster than I²C, ideal for high-speed communication.

### Wireless 
+ IOT DEVICES CAN ALSO COMMUNICATE OVER WIRELESS BLE, WIFI, LORA, ZIGBEE.

## Calibrate
Convert 12-Bit ADC --> Values from 0-4095 (2^(12))
![[Pasted image 20250327234834.png]]
>[!Formula]
>![[Pasted image 20250327234856.png]]

Steps: 
1. Take soil sample + Weight it --> Weight when WET
2. Take soil moisture reading using capacitive sensor -> ADC
3. Dry the soil in an "oven" for few hours
4. Weigh Again --> weigh when dry 

**THIS is how we can convert an ANALOG to percentage**
