# Constrained Device Application (Connected Devices)

## Lab Module 04

Be sure to implement all the PIOT-CDA-* issues (requirements) listed at [PIOT-INF-04-001 - Lab Module 04](https://github.com/orgs/programming-the-iot/projects/1#column-10488386).

### Description

NOTE: Include two full paragraphs describing your implementation approach by answering the questions listed below.

What does your implementation do? 
- This implementation adds Sense HAT emulator to the CDA, let program can collect temperature, pressure, and humidity data from an emulated hardware environment instead of simulated datasets.

How does your implementation work?
- The SensorAdapterManager reads configuration to determine whether emulator mode is enabled. If mode is enabled, it loads the Sense HAT emulator sensor tasks and periodically polls them with a scheduler. Each sensor task generates telemetry through the emulator, combines it into a SensorData object, and forwards it to the listener, enabling data collection continously.

### Code Repository and Branch

NOTE: Be sure to include the branch (e.g. https://github.com/programming-the-iot/python-components/tree/alpha001).

URL: https://github.com/Mooyeonkim628/TELE6530_Lab_CDA/tree/labmodule04

### UML Design Diagram(s)

NOTE: Include one or more UML designs representing your solution. It's expected each
diagram you provide will look similar to, but not the same as, its counterpart in the
book [Programming the IoT](https://learning.oreilly.com/library/view/programming-the-internet/9781492081401/).

![CDA UML](./lab04_cda.drawio.png)

### Unit Tests Executed

NOTE: TA's will execute your unit tests. You only need to list each test case below
(e.g. ConfigUtilTest, DataUtilTest, etc). Be sure to include all previous tests, too,
since you need to ensure you haven't introduced regressions.

- python -m unittest tests/unit/common/test_ConfigUtilDefault.py
- python -m unittest tests/unit/common/test_ConfigUtilCustom.py
- python -m unittest tests/unit/system/test_SystemCpuUtilTask.py
- python -m unittest tests/unit/system/test_SystemMemUtilTask.py
- python -m unittest tests/unit/data/test_ActuatorData.py
- python -m unittest tests/unit/data/test_SensorData.py
- python -m unittest tests/unit/data/test_SystemPerformanceData.py
- python -m unittest tests/unit/sim/test_HumiditySensorSimTask.py
- python -m unittest tests/unit/sim/test_PressureSensorSimTask.py
- python -m unittest tests/unit/sim/test_TemperatureSensorSimTask.py
- python -m unittest tests/unit/sim/test_HumidifierActuatorSimTask.py
- python -m unittest tests/unit/sim/test_HvacActuatorSimTask.py

### Integration Tests Executed

NOTE: TA's will execute most of your integration tests using their own environment, with
some exceptions (such as your cloud connectivity tests). In such cases, they'll review
your code to ensure it's correct. As for the tests you execute, you only need to list each
test case below (e.g. SensorSimAdapterManagerTest, DeviceDataManagerTest, etc.)

- python -m unittest tests/integration/emulated/test_SenseHatEmulatorQuick.py
- python -m unittest tests/integration/emulated/test_HumidityEmulatorTask.py
- python -m unittest tests/integration/emulated/test_PressureEmulatorTask.py
- python -m unittest tests/integration/emulated/test_TemperatureEmulatorTask.py
- python -m unittest tests/integration/emulated/test_HumidifierEmulatorTask.py
- python -m unittest tests/integration/emulated/test_HvacEmulatorTask.py
- python -m unittest tests/integration/emulated/test_LedDisplayEmulatorTask.py
- python -m unittest tests/integration/emulated/test_SensorEmulatorManager.py
- python -m unittest tests/integration/emulated/test_ActuatorEmulatorManager.py

EOF.
