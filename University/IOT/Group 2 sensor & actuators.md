## Sensor definition
>[!Definition] 
>Hardware devices that sense the physical world
>They **measure** physical properties and **send** that information to an IOT device

*Common sensors* : 
+ temperature sensors
+ Humidity sensors 
+ Accelerometers
*2 primary types* 
+ Analog sensors 
	+ Produce continuous signals that change smoothly
+ Digital sensors
	+ Output discreet signals, ON or OFF

##### ANALOG SENSORS:
*Continuous Output* - Signal changes smoothly with the measured parameter for real-time monitoring
*Voltage or Current Output* - Outputs a corresponding voltage or current but may be affected by noise
*Limited Precision* - Susceptible to interference, making them less precise than digital sensors
*Direct Connection* - can connect to analog devices or an ADC for digital conversion
![[Pasted image 20250327200000.png | 300]]
The sensor receives *voltage* from IOT devices, adjust and returns it to reflect data

*Voltage* : the force that pushes electricity from one point to another
+ In analog sensors, voltage varies with the measured condition, enabling IoT devices to interpret real-world data

**IOT use analog sensors**
+ It *constantly monitors the sensor's* voltage output
+ If the *voltage drops or increases*, the device recognizes the change and takes action
	<u>Application:</u>
	+ *Potentiometer*
		+ Rotate the dial between two fixed ends (0V to 5V)
		+ Sensor measures rotation by sending reduced voltage (or numeric mapping) corresponding to shift
	+ *Thermistor* 
		+ Special type of temperature sensor that operates based on resistance changes
		+ Two types 
			+ NTC: negative temperature coefficient
				+ resistance decreases as temperature get warmer
			+ PTC : positive temperature coefficient
				+ Resistance increases when they get warmer
>[!Warning]
>When output voltage exceeds input
>Potential Issues:
>+ Circuit malfunction
>+ Sensor damage
>+ External power supply interference
>
Consequences : Damaging connected electronics / incorrect readings

*Solution* : Use voltage limiters or regulators 

**ANALOG-TO-DIGITAL** ADC
Many IoT Devices have *built-in* ADC and many sensors can *work with ADCs* via a connector board
![[Pasted image 20250327201441.png | 200]]
When it sends analog signal -> similar to sending digital signal but at a shorter clock cycle (like rapid sending speed)

**Digital sensors**
+ Detect electrical changes like analog sensors
+ But they output digital signals instead of continuous signals (0 | 1)
*Advanced digital sensors* : 
Read analog signals -> Convert using on-board ADC --> Output purely digital signals 

Benefits : 
+ Enhanced complexity & Details
+ Improved Security 
+ Higher immunity to Noise
+ Greater Flexibility

![[Pasted image 20250327202058.png]]
## Actuators
>[!Definition]
>Devices that make things move or operate
>They *convert* electrical signals from IOT devices into *action* in the real world
>Ex: LED, Speaker, Screen, Relay, Motor

**Actuators Types** 
They have a *control signal* and a source of energy
Based on *signal*, they *convert energy* into some *motion or interaction*

**Categories**
Actuators can be categorized by the function they serve and how they convert energy
+ Pneumatic
+ Hydraulic
+ Electric
+ Thermal
+ Magnetic
### Analog Actuators
Analog actuator *converts* analog signal into some interaction that is proportionate to the voltage supplied
--> DAC : Digital to Analog converter
Ex: The light brightness is proportionate to the voltage level 
![[Pasted image 20250327202746.png | 450]]

### Pulse Width Modulation PWM
+ Switch digital signals from IOT devices between 2 states creating pulses ( up and down)
+ Varying the duty cycle (ON/OFF duration) modulates pulse width 
--> Creating an output signal that acts analog
![[Pasted image 20250327203027.png]]
**Applications**
+ Change Screen's Brightness  - Switching Power Supplies
+ Heating Systems                    - Battery Charging
+ Motor Control                        - Audio amplifiers
**2-State Actuators** : On / Off devices
+ Relay - Buzzer
+ Led - Stepper Motor

**Solenoid**
Electromagnet formed by a helical coil of wire which generates a controlled magnetic field
+ automatically lock/unlock a door via a smartphone app or voice assistant.
+ The solenoid coil generates a magnetic field, pulling or pushing a plunger to engage/disengage the lock.
+ The movement of the solenoid either locks or unlocks the door.



