# 🤖 3D Robotic Gripper Design & Analysis

Welcome to the official repository for the **3D Parallel Robotic Gripper Project**. This repository contains the complete mechanical design, physics calculations, component selection, AutoCAD 3D modeling guides, circuit schematics, control firmware, and motion demonstration links for a two-finger parallel robotic gripper engineered to manipulate a $50 \text{ mm} \times 50 \text{ mm} \times 50 \text{ mm}$ target cube.

---

## 📁 Repository Directory Map

```text
repo/
├── README.md               # Executive summary, specifications, math calculations, BOM, standards
├── docs/
│   ├── task1_rulebook.md   # Design rules, functional constraints, performance metrics
│   ├── task2_mechanism/
│   │   ├── decision_matrices.md   # Concept evaluation matrix & mechanism selection rationale
│   │   └── sketches.md            # Kinematic concept diagrams and joint definitions
│   └── task3_circuit/
│       ├── schematic_and_bom.md   # Wiring schematic, power budget, datasheet checks, troubleshooting
│       └── bonus_firmware.py      # Python sketch: Joystick mixing with dead-zone & 300 ms watchdog
├── design/
│   ├── calculations_and_bom.md    # Physics friction model, grip-force math, actuator sizing, BOM
│   ├── CAD_Guide_AutoCAD.md       # Complete step-by-step AutoCAD 3D modeling guide
│   └── dimensions_and_drawing.md  # 2D engineering drawing layout & dimensioning specs
└── media/
    ├── README.md                  # Visual assets overview & motion breakdown
    └── links.md                   # Public Google Drive links for CAD files & MP4 animation renders
