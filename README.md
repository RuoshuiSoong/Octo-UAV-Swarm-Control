# Octo-UAV-Swarm-Control 🚁

**Developer:** Ruoshui Song (formerly Ruoshui Han)  

![Swarm Agile Maneuver Demo]![ezgif-62f96bd080b97114](https://github.com/user-attachments/assets/a1a26ac2-938e-4bfd-8abe-93ae4ad70cdf)


## 🏆 Awards & Recognition
* **First Prize (Junior High Division)** - The 5th Educational Drone Event, China (July 2021)
* **Awarding Body:** Chinese Society of Aeronautics and Astronautics (CSAA)
* **Category:** Rotorcraft Swarm Dance Programming
* **Certificate Name:** Ruoshui Han (Participant's former legal name)
* **Context:** A premier national-level robotics and programming competition in China. Recognized for excellence in algorithm design, 3D multi-agent trajectory planning, and hardware-software integration.

![Award Certificate]![ruishui song](https://github.com/user-attachments/assets/2f2d7cb9-b1ff-4eee-851a-bbfc6e4db98d)


## 📝 Project Overview
This repository contains the system architecture and core control logic for an automated, multi-agent Unmanned Aerial Vehicle (UAV) swarm system. Developed using Python, the program serves as a centralized control hub capable of managing **8 independent UAVs simultaneously** within a restricted physical boundary. 

The swarm executes highly synchronized, pre-programmed 3D flight trajectories based on visual positioning. The project highlights the practical application of kinematics, 3D spatial geometry, network synchronization, and closed-loop feedback systems in a real-world physical environment.

## 🛠 Core Technical Features

### 1. Multi-Agent Synchronization (8 UAVs)
![Synchronized Swiping Demo]![ezgif-3685c06ccb375a90](https://github.com/user-attachments/assets/02400e9e-dd55-4ba9-8f61-3ac3ee90d829)

* **Scalable Swarm Logic:** Engineered control logic to broadcast synchronized flight parameters to an 8-agent swarm with minimal network latency (via UDP).
* **Collision Avoidance:** Implemented rigid spatial buffering and synchronized timing to prevent mid-air collisions among the 8 agents within a highly constrained physical netting.

### 2. Visual Odometry & Coordinate Mapping
* Utilized downward-facing cameras to scan ground-based visual markers (Mission Pads / AprilTags).
* Implemented real-time coordinate transformations to map the physical environment into an absolute `(X, Y, Z)` Cartesian coordinate system, establishing a reliable `(0, 0, 0)` global origin for the entire swarm.

### 3. Kinematics & Synchronized Trajectory Planning
![Formation Stability Demo]![ezgif-6da600591f655538](https://github.com/user-attachments/assets/7f4a2451-0d1e-4b46-9b0b-ae0c57682c6d)

* **4D Navigation:** To ensure strict synchronization with external timeframes (e.g., musical cues) and maintain swarm formations, the system relies on a 4-dimensional navigation protocol: `Maps_to(X, Y, Z, Speed)`.
* **Physics Integration:** By precisely calculating the required velocity vector for each waypoint ($t = d/v$), the program controls the exact duration of each flight phase, demonstrating a deep understanding of physical kinematics.

### 4. Boundary Management & Emergency Hovering
* **RC Velocity Matrix:** Managed raw 4-channel output arrays `(Roll, Pitch, Throttle, Yaw)` for dynamic spatial adjustments.
* **Safety Protocol (Null Vector Lock):** Developed a boundary-detection algorithm. Upon detecting proximity to the physical netting, the system immediately forces the velocity matrix to `(0, 0, 0, 0)`. This counteracts physical inertia and triggers a millisecond-level emergency hover, successfully preventing boundary collisions.

## 🚀 Future Enhancements
* Integrate reinforcement learning algorithms for dynamic obstacle avoidance.
* Implement a localized GUI simulator to preview multi-agent trajectories before physical deployment.
