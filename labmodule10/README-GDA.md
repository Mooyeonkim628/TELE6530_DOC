# Gateway Device Application (Connected Devices)

## Lab Module 10

Be sure to implement all the PIOT-GDA-* issues (requirements) listed at [PIOT-INF-10-001 - Lab Module 10](https://github.com/orgs/programming-the-iot/projects/1#column-10488510).

### Description

NOTE: Include two full paragraphs describing your implementation approach by answering the questions listed below.

What does your implementation do? 

This implmentation enables edge messaging between the CDA and GDA using MQTT. The CDA reads sensor data from the device side and reacts immediately to local threshold violations, while the GDA receives sensor messages from the CDA, tracks longer-term trends, and triggers preemptive actuation when needed. GDA apps would subscribes to sensor messages sent by the CDA, analyzes the incoming values and sends actuator commands back to the CDA when the threshold condition met. 

How does your implementation work?

After the MQTT connection, the GDA subscribes to the CDA sensor, actuator response, and system performance topics. When a message arrives, it parses the payload and forwards the data to the appropriate handler.For sensor messages, the GDA processes incoming SensorData and performs analysis. The GDA checks whether humidity is out of bound of threshold. When the value exceeds such range, the GDA creates an ActuatorData command and publishes it back to the CDA.

### Code Repository and Branch

NOTE: Be sure to include the branch (e.g. https://github.com/programming-the-iot/python-components/tree/alpha001).

URL: https://github.com/Mooyeonkim628/TELE6530_Lab_GDA/tree/labmodule10

### UML Design Diagram(s)

NOTE: Include one or more UML designs representing your solution. It's expected each
diagram you provide will look similar to, but not the same as, its counterpart in the
book [Programming the IoT](https://learning.oreilly.com/library/view/programming-the-internet/9781492081401/).

![GDA UML](./lab10_gda.drawio.png)

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

- mvn test -Dtest=MqttClientPerformanceTest
- mvn test -Dtest=CoapClientPerformanceTest
- mvn test -Dtest=MqttClientConnectorTest

### Performance Test Result (MQTT)

INFO: \n\tTesting Publish: QoS = 0 | msgs = 10000 | payload size = 212 | start = 1.7740201E9 | end = 1.7740201E9 | elapsed = 2.2973
Mar 20, 2026 11:21:03 AM programmingtheiot.integration.connection.MqttClientPerformanceTest execTestPublish
INFO: \n\tTesting Publish: QoS = 1 | msgs = 10000 | payload size = 212 | start = 1.77403226E9 | end = 1.77403226E9  | elapsed = 3.3471
Mar 20, 2026 11:21:03 AM programmingtheiot.gda.connection.MqttClientConnector connectClient
INFO: MQTT client connecting to broker: ssl://localhost:8883
Mar 20, 2026 11:21:03 AM programmingtheiot.gda.connection.MqttClientConnector connectComplete
INFO: MQTT connection successful (is reconnect = false). Broker: ssl://localhost:8883
Mar 20, 2026 11:21:10 AM programmingtheiot.gda.connection.MqttClientConnector disconnectClient
INFO: Disconnecting MQTT client from broker: ssl://localhost:8883
Mar 20, 2026 11:21:10 AM programmingtheiot.integration.connection.MqttClientPerformanceTest execTestPublish
INFO: \n\tTesting Publish: QoS = 2 | msgs = 10000 | payload size = 212 | start = 1.7740201E9 | end = 1.7740201E9 | elapsed = 6.6371
Mar 20, 2026 11:21:10 AM programmingtheiot.gda.connection.MqttClientConnector connectClient
INFO: MQTT client connecting to broker: ssl://localhost:8883
Mar 20, 2026 11:21:10 AM programmingtheiot.gda.connection.MqttClientConnector disconnectClient
INFO: Disconnecting MQTT client from broker: ssl://localhost:8883
Mar 20, 2026 11:21:10 AM programmingtheiot.gda.connection.MqttClientConnector connectComplete
INFO: MQTT connection successful (is reconnect = false). Broker: ssl://localhost:8883
Mar 20, 2026 11:21:10 AM programmingtheiot.integration.connection.MqttClientPerformanceTest testConnectAndDisconnect
INFO: Connect and Disconnect [1]: 229 ms
Tests run: 4, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 13.16 s - in programmingtheiot.integration.connection.MqttClientPerformanceTest

Results:

Tests run: 4, Failures: 0, Errors: 0, Skipped: 0

------------------------------------------------------------------------
BUILD SUCCESS
------------------------------------------------------------------------
Total time:  14.389 s
Finished at: 2026-03-20T11:21:10-04:00

- qos 0: 2297.3 ms
- qos 1: 3347.1 ms
- qos 2: 6637.1 ms

- Fastest: qos 0
- Slowest: qos 2

### Performance Test Result (Coap)
CON Mode:
--- resources:3.3.1:resources (default-resources) @ gateway-device-app ---
Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!
skip non existing resourceDirectory /home/mooki/piot/gda-java-components/src/main/resources

--- compiler:3.13.0:compile (default-compile) @ gateway-device-app ---
Nothing to compile - all classes are up to date.

--- resources:3.3.1:testResources (default-testResources) @ gateway-device-app ---
Using platform encoding (UTF-8 actually) to copy filtered resources, i.e. build is platform dependent!
skip non existing resourceDirectory /home/mooki/piot/gda-java-components/src/test/resources

--- compiler:3.13.0:testCompile (default-testCompile) @ gateway-device-app ---
Nothing to compile - all classes are up to date.

--- surefire:3.0.0-M5:test (default-cli) @ gateway-device-app ---
useSystemClassLoader setting has no effect when not forking
The parameter forkCount should likely not be 0, not forking a JVM for tests reduce test accuracy, ensure to have a <forkCount> >= 1.
Running programmingtheiot.integration.connection.CoapClientPerformanceTest
[main] INFO org.eclipse.californium.elements.config.Configuration - defaults added COAP.
[main] INFO org.eclipse.californium.elements.config.Configuration - defaults added SYS.
[main] INFO org.eclipse.californium.elements.config.Configuration - defaults added UDP.
[main] INFO org.eclipse.californium.elements.config.Configuration - loading properties from file /home/mooki/piot/gda-java-components/Californium3.properties
Mar 22, 2026 2:57:50 PM programmingtheiot.gda.connection.CoapClientConnector initClient
INFO: Created client connection to server / resource: coap://localhost:5683
Mar 22, 2026 2:57:50 PM programmingtheiot.gda.connection.CoapClientConnector <init>
INFO: Using URL for server conn: coap://localhost:5683
Mar 22, 2026 2:57:50 PM programmingtheiot.integration.connection.CoapClientPerformanceTest testPostRequestCon
INFO: Testing POST - CON
[main] INFO org.eclipse.californium.core.network.RandomTokenGenerator - using tokens of 8 bytes in length
[main] INFO org.eclipse.californium.ban - Started.
[main] INFO org.eclipse.californium.core.network.CoapEndpoint - coap CoapEndpoint uses udp context
[main] INFO org.eclipse.californium.core.network.stack.BlockwiseLayer - coap BlockwiseLayer uses MAX_MESSAGE_SIZE=1024, PREFERRED_BLOCK_SIZE=512, BLOCKWISE_STATUS_LIFETIME=300000, MAX_RESOURCE_BODY_SIZE=8192, BLOCKWISE_STRICT_BLOCK2_OPTION=false
[main] INFO org.eclipse.californium.core.network.CoapEndpoint - coap Endpoint [coap://0.0.0.0:0] requires an executor to start, using default single-threaded daemon executor
[main] INFO org.eclipse.californium.elements.UDPConnector - UDPConnector starts up 2 sender threads and 2 receiver threads
[main] INFO org.eclipse.californium.elements.UDPConnector - UDPConnector listening on /[0:0:0:0:0:0:0:0]:44070, recv buf = 106496, send buf = 106496, recv packet size = 2048
[main] INFO org.eclipse.californium.core.network.CoapEndpoint - coap Started endpoint at coap://[0:0:0:0:0:0:0:0]:44070
[main] INFO org.eclipse.californium.core.network.EndpointManager - created implicit endpoint coap://[0:0:0:0:0:0:0:0]:44070 for coap
...
INFO: Handling POST. Response: false - {} - 4.04 - 
Mar 22, 2026 2:57:50 PM programmingtheiot.gda.connection.CoapClientConnector sendPostRequest
INFO: Handling POST. Response: false - {} - 4.04 - 
 sendPostRequest
...
INFO: Handling POST. Response: false - {} - 4.04 - 
Mar 22, 2026 2:57:13 PM programmingtheiot.integration.connection.CoapClientPerformanceTest execTestPost
INFO: POST message - useCON = true [10000]: 9009 ms
Tests run: 1, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 9.278 s - in programmingtheiot.integration.connection.CoapClientPerformanceTest

Results:

Tests run: 1, Failures: 0, Errors: 0, Skipped: 0

------------------------------------------------------------------------
BUILD SUCCESS
------------------------------------------------------------------------
Total time:  10.491 s
Finished at: 2026-03-22T14:57:13-04:00
------------------------------------------------------------------------

NON Mode:

--- surefire:3.0.0-M5:test (default-cli) @ gateway-device-app ---
useSystemClassLoader setting has no effect when not forking
The parameter forkCount should likely not be 0, not forking a JVM for tests reduce test accuracy, ensure to have a <forkCount> >= 1.
Running programmingtheiot.integration.connection.CoapClientPerformanceTest
[main] INFO org.eclipse.californium.elements.config.Configuration - defaults added COAP.
[main] INFO org.eclipse.californium.elements.config.Configuration - defaults added SYS.
[main] INFO org.eclipse.californium.elements.config.Configuration - defaults added UDP.
[main] INFO org.eclipse.californium.elements.config.Configuration - loading properties from file /home/mooki/piot/gda-java-components/Californium3.properties
Mar 22, 2026 2:59:32 PM programmingtheiot.gda.connection.CoapClientConnector initClient
INFO: Created client connection to server / resource: coap://localhost:5683
Mar 22, 2026 2:59:32 PM programmingtheiot.gda.connection.CoapClientConnector <init>
INFO: Using URL for server conn: coap://localhost:5683
Mar 22, 2026 2:59:32 PM programmingtheiot.integration.connection.CoapClientPerformanceTest testPostRequestNon
INFO: Testing POST - NON
[main] INFO org.eclipse.californium.core.network.RandomTokenGenerator - using tokens of 8 bytes in length
[main] INFO org.eclipse.californium.ban - Started.
[main] INFO org.eclipse.californium.core.network.CoapEndpoint - coap CoapEndpoint uses udp context
[main] INFO org.eclipse.californium.core.network.stack.BlockwiseLayer - coap BlockwiseLayer uses MAX_MESSAGE_SIZE=1024, PREFERRED_BLOCK_SIZE=512, BLOCKWISE_STATUS_LIFETIME=300000, MAX_RESOURCE_BODY_SIZE=8192, BLOCKWISE_STRICT_BLOCK2_OPTION=false
[main] INFO org.eclipse.californium.core.network.CoapEndpoint - coap Endpoint [coap://0.0.0.0:0] requires an executor to start, using default single-threaded daemon executor
[main] INFO org.eclipse.californium.elements.UDPConnector - UDPConnector starts up 2 sender threads and 2 receiver threads
[main] INFO org.eclipse.californium.elements.UDPConnector - UDPConnector listening on /[0:0:0:0:0:0:0:0]:52967, recv buf = 106496, send buf = 106496, recv packet size = 2048
[main] INFO org.eclipse.californium.core.network.CoapEndpoint - coap Started endpoint at coap://[0:0:0:0:0:0:0:0]:52967
[main] INFO org.eclipse.californium.core.network.EndpointManager - created implicit endpoint coap://[0:0:0:0:0:0:0:0]:52967 for coap
Mar 22, 2026 2:59:32 PM programmingtheiot.gda.connection.CoapClientConnector sendPostRequest
INFO: Handling POST. Response: false - {} - 4.04 - 
Mar 22, 2026 2:59:32 PM programmingtheiot.gda.connection.CoapClientConnector sendPostRequest
INFO: Handling POST. Response: false - {} - 4.04 - 
Mar 22, 2026 2:59:32 PM programmingtheiot.gda.connection.CoapClientConnector sendPostRequest
...

programmingtheiot.integration.connection.CoapClientPerformanceTest execTestPost
INFO: POST message - useCON = false [10000]: 8476 ms
Tests run: 1, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 8.758 s - in programmingtheiot.integration.connection.CoapClientPerformanceTest

Results:

Tests run: 1, Failures: 0, Errors: 0, Skipped: 0

------------------------------------------------------------------------
BUILD SUCCESS
------------------------------------------------------------------------
Total time:  11.556 s
Finished at: 2026-03-22T14:56:13-04:00
------------------------------------------------------------------------

- Percentage difference (NON baseline): 6.29%
- Fastest: NON (8476 ms)
- Slowest: CON (9009 ms)


EOF.
