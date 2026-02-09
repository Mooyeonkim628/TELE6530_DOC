# Gateway Device Application (Connected Devices)

## Lab Module 05

Be sure to implement all the PIOT-GDA-* issues (requirements) listed at [PIOT-INF-05-001 - Lab Module 05](https://github.com/orgs/programming-the-iot/projects/1#column-10488421).

### Description

NOTE: Include two full paragraphs describing your implementation approach by answering the questions listed below.

What does your implementation do? 
- This implementation collects system performance telemetry, wraps it in SystemPerformanceData, and forwards it. It also supports converting GDA data objects to and from JSON and store/publish via the persistence adapter.

How does your implementation work?
- The GDA periodically runs telemetry tasks to get utilization values, creates a SystemPerformanceData object and sets data. Then it sends the message to data message listener. For serialization and deserialization, it uses DataUtil to convert data as JSON, and the RedisPersistenceAdapter handles connecting to Redis and publishing or persisting the JSON payloads.

### Code Repository and Branch

NOTE: Be sure to include the branch (e.g. https://github.com/programming-the-iot/python-components/tree/alpha001).

URL: https://github.com/Mooyeonkim628/TELE6530_Lab_GDA/tree/labmodule05

### UML Design Diagram(s)

NOTE: Include one or more UML designs representing your solution. It's expected each
diagram you provide will look similar to, but not the same as, its counterpart in the
book [Programming the IoT](https://learning.oreilly.com/library/view/programming-the-internet/9781492081401/).

![GDA UML](./lab05_gda.drawio(2).png)

### Unit Tests Executed

NOTE: TA's will execute your unit tests. You only need to list each test case below
(e.g. ConfigUtilTest, DataUtilTest, etc). Be sure to include all previous tests, too,
since you need to ensure you haven't introduced regressions.

- (old)
- mvn test -Dtest=ConfigUtilDefaultTest
- mvn test -Dtest=ConfigUtilCustomTest
- mvn test -Dtest=SystemCpuUtilTaskTest
- mvn test -Dtest=SystemMemUtilTaskTest
- (new)
- mvn test -Dtest=ActuatorDataTest
- mvn test -Dtest=SensorDataTest
- mvn test -Dtest=SystemPerformanceDataTest
- mvn test -Dtest=DataUtilTest

### Integration Tests Executed

NOTE: TA's will execute most of your integration tests using their own environment, with
some exceptions (such as your cloud connectivity tests). In such cases, they'll review
your code to ensure it's correct. As for the tests you execute, you only need to list each
test case below (e.g. SensorSimAdapterManagerTest, DeviceDataManagerTest, etc.)

- mvn test -Dtest=SystemPerformanceManagerTest
- mvn test -Dtest=DataIntegrationTest
- mvn test -Dtest=DeviceDataManagerNoCommsTest
- mvn test -Dtest=GatewayDeviceAppTest
- mvn test -Dtest=PersistenceClientAdapterTest

EOF.
