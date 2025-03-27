### Outline: Learn to 
+ Send & Receive messages
+ Connect light to MQTT Broker
+ Connect device to internet

## Introduction
IoT Device typically *connect to a single cloud* IoT service - using a standard communication protocol (~ speaking the same language)

So, IoT device sends "telemetry" and receive "commands" to and from the cloud platform
-> That service then connects to the rest of your IoT App
*Analogy* : 
IoT devices send sensor data to cloud  "telemetry"
Cloud sends request for action to device "command"

### Communication Protocol 
**MQTT**  Message Queuing Telemetry Transport
Pub/Sub messaging protocols involve a broker
All of the devices  publish "telemetry" to the broker 
The cloud service who subscribe to that "telemetry" will receive data and publish the "command to execute" 
Then those devices that subscribe to those topic will receive the commands
>[!Note] Messages routed by topics -> Not by target endpoints

Problems : Provided with bunch of IoT devices -> How to handle all message
**Solution**:
+ Choose scalable MQTT Broker (EMQX, Mosquitto)
+ Optimize MQTT quality of service (QoS) levels 
+ Efficient topic design

**AMQP** : Advanced Message Queuing Protocol
It’s used for **asynchronous communication** between distributed systems
+ **Message queuing**: Messages don’t require an immediate response.  
+ **Reliable delivery**: Messages can be stored and resent if needed.  
+ **Publish-subscribe**: Supports multiple consumers processing the same message.  
+ **Routing**: Messages can be routed based on topics and rules.

**HTTP/ HTTPS**
HTTP is a **request-response protocol** used for communication between **clients (browsers, apps)** and **servers**. HTTPS is the secure version, encrypting data with **SSL/TLS**.

| Feature           | AMQP                               | HTTP/HTTPS                             |
| ----------------- | ---------------------------------- | -------------------------------------- |
| **Communication** | Asynchronous (message queue)       | Synchronous (request-response)         |
| **Use Case**      | Background jobs, event-driven apps | Web browsing, APIs                     |
| **Reliability**   | High (message persistence)         | Lower (depends on server availability) |
| **Security**      | Can be secured with TLS            | HTTPS provides encryption              |

### IoT Edge Computing
Similar to the previous presentation by Hưng
It can run and process the data locally instead of exploiting the use of cloud 

### Deeper dive into MQTT
MQTT topics can have a hierarchy
+ Get only message from a subset : *single-level wildcard*
	+ /telemetry/humidity
	+ /telemetry/temperature
+ Getting all message from the topic: *multi-level wildcard*
	+ /telemetry/#

### Message "QoS" determines *delivery guarantees*
Ensure reliable, timely data transmission from IoT devices to the internet
**Key metrics for IoT**:
+ Bandwidth: supports telemetry data volume
+ Latency: Speeds up real-time data delivery
+ Jitter: Keeps data flow consistent
+ Packet Loss : Prevents Telemetry Gasp
+ Availability: Maintains constant connection

*QoS* matters in IoT due to :
+ Prioritizing telemetry traffic
+ Reserving bandwidth for IoT data
+ Manages network congestion

*QoS 0* : "At most once" (Fire and Forget)
+ The message is dilive
