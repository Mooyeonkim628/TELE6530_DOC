# Lab Module 12 - Semester Project Proposal

## Description

Describe your idea in 1 paragraph (at least 2 or 3 sentences).

This project implements a smart home environmental control system using a Raspberry Pi 4 as the Constrained Device App and computer running the Gateway Device App. The system monitors real-time temperature, humidity, and air pressure using a Sense HAT, and automatically controls a air conditioner or heater via IR signal transmission and a humidifier via a smart plug. A Camera module provides continuous RTSP video streaming with motion detection. All sensor data and actuator events are forwarded to Ubidots cloud for remote monitoring and control.

## What - The Problem 

What problem are you trying to solve and why does it matter? Write 1 to 2 paragraphs in response.

When a home is left unoccupied for long periods, maintaining proper temperature and humidity becomes critical. Without active control, indoor climate can drift into ranges that promote mold growth, corrosion, and material degradation, causing irreversible damage to clothing, electronics. Most existing smart home devices address only one aspect of this problem in isolation, with no shared logic or unified response.

Security is an equally important concern. An unattended home has no way to detect or report unauthorized entry in real time. A system that combines automated climate control with motion-based monitoring addresses both problems together, providing a practical solution for resident who need to leave their property unoccupied for days, weeks, or months.  This is particularly relevant for homes with older air conditioners that have no Wi-Fi capability, where remote control is not possible without an additional layer of hardware and software.

## Why - Who Cares? 

Why do you care about this particular problem? Write 1 to 2 paragraphs in response.

As a international student living between South Korea and Boston, my apartment is left unoccupied for months at a time. During those absences, there is no way to know whether the indoor climate has damaged belongings or whether the space has been entered without authorization. This project addresses that problem by enabling remote monitoring and control from anywhere in the world. It also demonstrates that reliable home automation can be built on open, layered architecture without depending on expensive systems.

## How - Expected Technical Approach

How do you plan to tackle this problem technically?

Include a high-level design diagram depicting your planned technical approach - it does not need to be final, but it must include the CDA, GDA, and cloud services you plan to use, as well as the protocol(s) you will use for communicating between the devices and the cloud.

![Diagram](./Project_Proposal.drawio.png)

Write 1 to 2 paragraphs describing your diagram.

The CDA (Raspberry Pi 4) collects sensor data from the Sense HAT every 5 seconds including temperature, humidity, and pressure, and applies seasonal threshold logic locally. In summer mode, the AC turns on above 23°C and turns off below 20°C, via IR LED transmission. In winter mode, a heater turns on below 24°C and turns off above 27°C. The humidifier is controlled via the TP-Link Kasa cloud API, turning on below 40% humidity and turning off above 60%. A Camera Module 3 streams RTSP video and detects motion by comparing consecutive frames. All sensor data, actuator responses, and motion events are published to the GDA via MQTT over TLS. Since the CDA and GDA are located in different areas, Tailscale VPN is used to create a secure virtual network between the two devices, allowing MQTT communication as if they were on the same local network.

The GDA receives CDA data, collects its own internal system performance data (CPU, memory, and disk utilization), stores samples in Redis, and forwards data to Ubidots via MQTT over TLS. When a user triggers an actuator command from the Ubidots dashboard, the cloud notifies the GDA, which forwards the command to the CDA. A 10 minute cloud override timer prevents local logic from conflicting with cloud-initiated commands. 


## Results - Expected Outcomes 

If your project is successful, what outcome do you expect (e.g. what will happen if everything works)? Write 1 to 2 paragraphs describing your expected outcomes.

The system will autonomously maintain indoor temperature and humidity within the configured seasonal ranges without intervention. The Sense HAT LED will display actuator status messages, the Camera Module 3 will stream live RTSP video viewable via Tailscale VPN, and motion detection events will be published to Ubidots in real time, triggering an automated email alert to notify the user of any detected movement. All data will be stored in Redis on the GDA and visualized on the Ubidots dashboard.


EOF.
