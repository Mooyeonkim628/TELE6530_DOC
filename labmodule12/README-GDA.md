# Gateway Device Application (Connected Devices)

## Lab Module 12 - Semester Project - GDA Components

Be sure to implement all the PIOT-GDA-* issues (requirements) listed at [PIOT-INF-12-001 - Lab Module 12](https://github.com/orgs/programming-the-iot/projects/1#column-10488565).

### Description

NOTE: Include two full paragraphs describing your implementation approach by answering the questions listed below.

What does your implementation do? 

The GDA acts as a bridge between the CDA and Ubidots cloud, receiving sensor data from the CDA and forwarding it upstream to Ubidots for visualization. Actuators can also be manually controlled via the Ubidots dashboard, with a 10-minute cloud override lock to prevent conflicts between manual and automatic control.

How does your implementation work?

The GDA connects to the local Mosquitto MQTT broker over TLS and subscribes to CDA sensor and actuator response topics. Sensor data is parsed and forwarded to Ubidots via MQTT. The GDA also subscribes to Ubidots last-value topics to receive manual actuator commands from the cloud dashboard and publishes them back to the CDA via the local broker. System performance data (CPU, memory, disk) is persisted locally in Redis. A cloud override mechanism sets a 10-minute timer when a manual command is received, during which local threshold-based actuator logic is suppressed to prevent race conditions.

### Code Repository and Branch

NOTE: Be sure to include the branch (e.g. https://github.com/programming-the-iot/python-components/tree/alpha001).

URL: URL: https://github.com/Mooyeonkim628/TELE6530_Lab_GDA/tree/labmodule12

### UML Design Diagram(s)

NOTE: Include one or more UML designs representing your solution. It's expected each
diagram you provide will look similar to, but not the same as, its counterpart in the
book [Programming the IoT](https://learning.oreilly.com/library/view/programming-the-internet/9781492081401/).

![GDA UML](./lab11_gda.drawio.png)

### Unit Tests Executed

NOTE: TA's will execute your unit tests. You only need to list each test case below
(e.g. ConfigUtilTest, DataUtilTest, etc). Be sure to include all previous tests, too,
since you need to ensure you haven't introduced regressions.

- (old)
- mvn test -Dtest=ConfigUtilDefaultTest
- mvn test -Dtest=ConfigUtilCustomTest
- mvn test -Dtest=SystemCpuUtilTaskTest
- mvn test -Dtest=SystemMemUtilTaskTest
- mvn test -Dtest=ActuatorDataTest
- mvn test -Dtest=SensorDataTest
- mvn test -Dtest=SystemPerformanceDataTest
- mvn test -Dtest=DataUtilTest

### Integration Tests Executed

NOTE: TA's will execute most of your integration tests using their own environment, with
some exceptions (such as your cloud connectivity tests). In such cases, they'll review
your code to ensure it's correct. As for the tests you execute, you only need to list each
test case below (e.g. SensorSimAdapterManagerTest, DeviceDataManagerTest, etc.)

- no new test

EOF.
