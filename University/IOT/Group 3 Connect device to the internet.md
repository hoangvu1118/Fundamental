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
+ The message is delivered *once* at most, without any acknowledgement 
+ If message lost due to network issues -> will not be resent
+ **Fast** but least reliable
+ UseCase: Occasional message loss is acceptable, (sensor data that updates frequently)

*QoS 1*: "At least once" (Acknowledge Delivery)
+ It is guaranteed to deliver at *least once*, -> duplicate may occur
+ Sender stores message until it gets a *PUBACK* or acknowledgement from receiver 
+ If no PUBACK --> resends the message
+ Slower than QoS 0 but more reliable 
+ UseCase: Message loss is not acceptable, but duplicates can be handled, (sending alerts or notifications)

*QoS 2* : "Exactly once" (Guaranteed Delivery)
+ Message is delivered *exactly once*, ensuring no duplicates
+ *4-Step handshake* Publish -> Pubrec -> Pubrel -> Pubcomp
+ More network overhead and latency due to additional acknowledgments
+ UseCase: critical transaction where **duplicate** not acceptable (billing | financial transactions)

>[!Warning] 
>MQTT does not "Queue up" messages for subscribed clients
>--> loses new messages if disconnected

**Solutions:** 
+ Keep alive function : checks if connection btw MQTT client and the broker is alive 
	+ If client do not send any messages within a specified time interval 
	+ It must sent a packet (PINGREQ) to tell "I am still here"
	+ Otherwise, wait for 1.5 times --> disconnect 
+ Retained flag: set it to ensure last message on topic is saved for late subscribers 
	+ Normally, a client receive *new messages* when subscribing to a topic. 
	+ However it a retained message exists for that topic 
	+ --> new subscriber will instantly receive the last retained message
>[!Warning]
>Broker can store only **1 retained message PER topic**
>So it overrides the previous one if there's a new retained message

**Telemetry** : A Greek word : to measure remotely 
It is the act of gathering data from sensors and sending it to the cloud for processing

Flow example:
1. Internet connected thermostat device
2. Sensor telemetry published to cloud
3. Cloud analyzes room telemetry, context to request action(on,off)
4. Action published to IOT device for actuators

**Send telemetry from IoT Devices**
1. Send light level telemetry to /telemetry topic on MQTT
2. Data sent encoded as Json (key/value pairs)

**Receive Telemetry from MQTT Broker**
1. "Sever" code that subscribes to telemetry, analyzes context, send decisions(commands) back to IoT devices
2. Sever typically runs in cloud - for now, run in local server

### How often should telemetry be sent?
Higher frequency has better responses to change **but** use more resources and power
*It still depends* (thermostat should send every 10 minutes)
+ If mission critical --> more frequent

### Loss of connectivity
1. Lose Data
2. Store data | Till it is reconnected

MQTT don't store automatically --> so write client/server code..
Depends on the data which is mandatory to store
Ex :
+ Thermostat --> no need
+ Machinery : data can be used for profiling and predictive maintenance --> store it

### Handle commands on IoT Devices
**IoT devices must**
+ Subscribe to relevant topic
+ Listen for messages on topic
+ Handle messages - Taking appropriate action to controlled

