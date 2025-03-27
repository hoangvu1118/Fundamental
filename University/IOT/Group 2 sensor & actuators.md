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
	+ POTENTIOMETER
		+ Rotate the dial between two fixed ends (0V to 5V)
		+ Sensor measures rotation by sending reduced voltage (or numeric mapping) corresponding to shift



