# Software Requirements Specification (SRS)
**Project:** Octo-UAV-Swarm-Control
**Version:** 1.0

## 1. Introduction
### 1.1 Purpose
The purpose of this document is to define the functional and non-functional requirements for the Octo-UAV-Swarm-Control system. This system is designed to autonomously choreograph and control a swarm of 8 micro-UAVs within a confined physical space using visual odometry and absolute coordinate mapping.

### 1.2 Scope
The software will run on a central control computer, communicating with 8 independent UAVs via UDP network protocols. It handles initialization, coordinate translation, synchronized path execution, and emergency collision avoidance.

## 2. Functional Requirements (FR)
### FR-1: System Initialization & Calibration
* **FR-1.1:** The system must establish a stable UDP connection with all 8 UAVs simultaneously.
* **FR-1.2:** The system must command all UAVs to take off to an initial safe hover altitude (e.g., 1.2 meters).
* **FR-1.3:** The system must utilize downward-facing cameras to scan ground-based Mission Pads and establish a global `(0, 0, 0)` origin point for the swarm.

### FR-2: Swarm Navigation & Synchronization
* **FR-2.1:** The system must support a 4D navigation array: `Maps_to(X, Y, Z, Speed)`.
* **FR-2.2:** The system must independently calculate the velocity vector for each UAV based on target coordinates to ensure simultaneous arrival (time-axis synchronization).
* **FR-2.3:** The system must support yaw, pitch, roll, and throttle adjustments for mid-air choreography.

### FR-3: Boundary Management & Safety
* **FR-3.1:** The system must define an electronic geofence corresponding to the physical netting dimensions.
* **FR-3.2:** Upon detecting proximity to the geofence, the system must immediately override current flight paths and send a null matrix `(0, 0, 0, 0)` to trigger an emergency hover.

## 3. Non-Functional Requirements (NFR)
### 3.1 Performance & Latency
* Command broadcast latency to the 8-agent swarm must not exceed 50 milliseconds to maintain choreographic synchronization.
* Visual coordinate recalculation must occur at a minimum of 10 Hz.

### 3.2 Safety & Reliability
* The collision avoidance algorithm must have a 100% success rate within the defined operational boundary.
* In the event of network loss, individual UAVs must auto-trigger a slow-descent landing protocol.

## 4. Hardware Interfaces
* **UAV Hardware:** Compatible with open-SDK micro-drones (e.g., DJI Tello EDU).
* **Positioning:** Ground-based AprilTag/Mission Pad grid.
