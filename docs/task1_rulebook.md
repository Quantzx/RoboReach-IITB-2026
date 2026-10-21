# Task 1: Rulebook Checks, Technical Justifications & Specifications

## 1. Dimensional Constraints & Kinematic Envelopes

To maintain full compliance with the RoboReach rulebook, the robotic platform strictly adheres to three critical geometric boundaries:

### A. Start-Box Bounding Volume ($300 \times 200 \times 300\text{ mm}$)
* **Constraint:** At the start of the match, the entire robot (chassis, wheels, retracted arm, and gripper) must fit inside a $300 \text{ mm (Length)} \times 200 \text{ mm (Width)} \times 300 \text{ mm (Height)}$ start-box.
* **Engineering Justification:** Fitting within this volume requires a stowed arm configuration where the 3 links fold back onto themselves inside the footprint. The $190\text{ mm}$ track width leaves a $10\text{ mm}$ total tolerance margin along the width ($200\text{ mm}$ limit), preventing contact with the start-box walls during deployment.

### B. Maximum Vertical Reach ($450\text{ mm}$)
* **Constraint:** The manipulator end-effector must reach a minimum height of $450\text{ mm}$ above the ground plane to complete high-level manipulation tasks (such as wire tracing or elevated payload placement).
* **Engineering Justification:** The chosen 3-link revolute arm provides a maximum vertical extension of $z = 470\text{ mm}$ calculated by:
  $$z = h_s + L_1 \sin\theta_1 + L_2 \sin(\theta_1+\theta_2) + L_3 \sin(\theta_1+\theta_2+\theta_3)$$
  With base height $h_s = 80\text{ mm}$, bicep $L_1 = 180\text{ mm}$, forearm $L_2 = 150\text{ mm}$, and gripper $L_3 = 60\text{ mm}$, at full vertical extension ($\theta_1 = 90^\circ, \theta_2 = 0^\circ, \theta_3 = 0^\circ$):
  $$z = 80 + 180(1) + 150(1) + 60(1) = 470\text{ mm}$$
  This $470\text{ mm}$ reach satisfies the $450\text{ mm}$ requirement with a $20\text{ mm}$ safety margin.

### C. Ground Clearance ($\ge 50\text{ mm}$)
* **Constraint:** The lowest point of the chassis frame must maintain a clearance of at least $50\text{ mm}$ off the arena floor.
* **Engineering Justification:** The arena features $40\text{ mm}$ speed breaker obstacles. Standard $100\text{ mm}$ diameter wheels yield a axle-center-to-ground distance (radius) of $50\text{ mm}$. Mounting the main chassis floor flush with or above the wheel centers guarantees $50\text{ mm}$ of clear space underneath, allowing the bot to traverse $40\text{ mm}$ speed breakers without high-centering or scraping the bottom.

---

## 2. Electrical Constraints & Safety Systems

### A. Voltage Limits ($\le 24\text{ V DC}$)
* **Constraint:** The total system operating voltage must not exceed $24\text{ V DC}$ under any operational state.
* **Battery Justification:**
  * **3S LiPo Battery (Compliant):** A 3-series Lithium Polymer battery has a nominal voltage of $11.1\text{ V}$ and a maximum fully charged voltage of $12.6\text{ V}$ ($3 \times 4.2\text{ V}$). This is strictly within the $\le 24\text{ V DC}$ envelope.
  * **6S LiPo Battery (Non-Compliant / Disqualified):** A 6-series LiPo battery has a maximum fully charged voltage of $25.2\text{ V}$ ($6 \times 4.2\text{ V}$). Because $25.2\text{ V} > 24\text{ V}$, using a 6S battery violates safety limits and results in immediate disqualification.

### B. Emergency Failsafe System
* **Constraint:** The robot must feature an active remote-disconnect failsafe mechanism.
* **Engineering Justification:** If the wireless link (2.4 GHz RF / Bluetooth joystick) drops, onboard microcontrollers (e.g., ESP32 / Arduino) execute a watchdog routine. This routine immediately pulls motor driver PWM pins to `LOW` and disables active actuators, preventing unguided motion and ensuring track safety.

---

## 3. Score Target Calculation & Strategy

The total match score is evaluated using the official rulebook equation:

$$\text{Total Score} = A + T - P$$

Where:
* **$A$ (Arena Task Points):** Points awarded for successful task completion. Target = **$180$ Points** (incorporating Robonardo DaVinci marker drawing and Buzzed wire navigation).
* **$T$ (Time Bonus):** Bonus calculated for completing the course under the allotted time limit ($T = \max(0, T_{\text{max}} - T_{\text{completion}})$). Estimated = **$15$ Points**.
* **$P$ (Penalties):** Point deductions for touching obstacle boundaries, wire collisions, or manual restarts. Target = **$\le 40$ Points**.

### Projected Target Score Calculation
$$\text{Total Score} = 180 + 15 - 40 = 155\text{ Points}$$

Targeting a net score of **155 points** ensures competitive selection for the IIT Bombay RoboReach roster while maintaining safety buffers against touch penalties.
