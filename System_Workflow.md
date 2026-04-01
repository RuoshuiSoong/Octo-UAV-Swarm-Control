# System Architecture & How It Works

**Note:** As mentioned in the main readme, the original scripts from 2021 were lost during my hardware transition to Canada. This document outlines the actual logical workflow I designed for the swarm choreography.

## 1. Getting Off the Ground
* **Connecting the Swarm:** My central laptop acted as the brain, establishing a UDP wireless connection with all 8 drones simultaneously.
* **Finding the Origin (0,0,0):** This was the tricky part. Without GPS indoors, I used the drones' downward-facing cameras to scan Mission Pads on the floor. This visual feedback helped the system build a reliable `(0,0,0)` 3D coordinate map in real-time.

## 2. The Choreography Logic
To make 8 drones dance to the same musical beat, I couldn't just tell them to "fly forward." I had to calculate dynamic speeds.
* **Target Mapping:** The system loaded a list of 3D coordinates for the next formation.
* **Simultaneous Broadcast:** The system sent the target coordinates to all 8 drones at the exact same time.
* **Math in Action:** To ensure they all arrived at the same second (to match the music), the system calculated the exact distance each drone had to travel, and dynamically adjusted their required flight speed (v = d/t).

## 3. The Electronic Net (Collision Avoidance)
We were flying in a tight physical netting, and crashes were my biggest nightmare.
* **Virtual Geofence:** I programmed an invisible "electronic wall" safely inside the physical net.
* **Emergency Hover:** The central computer constantly tracked the `X` and `Y` coordinates of every drone. If a drone was pushed too close to the virtual boundary, the system instantly overrode its current path and sent a `(0, 0, 0, 0)` velocity matrix (zero pitch, roll, yaw, throttle). This forced an immediate mid-air hover, completely canceling its momentum.

## 4. The Biggest Challenge: Airflow Interference
When I first tested the system, the drones kept drifting and crashing into each other even when the code was perfectly synchronized. I quickly realized that the downwash (airflow) from the higher drones was destabilizing the lower ones. 

To fix this, I had to completely rewrite the formation blueprints. I added a strict rule in the trajectory planning: no two drones could ever share the same `X, Y` vertical column within a 50cm altitude difference. This hard-learned lesson taught me that perfect code on a screen doesn't always translate to perfect physics in the real world.
