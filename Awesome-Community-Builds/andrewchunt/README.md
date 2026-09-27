# PLC Trainer Kit — C-more CM5 HMI Build

This repository documents my personal build and extension of the **Packets-or-it-didn't-happen PLC Trainer Kit**, originally created by [Oren Niskin / oniskin](https://github.com/oniskin/PLC-Trainer-Kit).

The original project provides an excellent hands-on platform for learning about **Industrial Control Systems (ICS), Operational Technology (OT), PLC programming, industrial networking, Modbus TCP, HMI operation, and OT cybersecurity**.

My build expands on the original design by adding a **physical AutomationDirect C-more CM5-T7W 7-inch HMI**, creating an environment that more closely resembles a small industrial control panel.

> **Original Project:**  
> https://github.com/oniskin/PLC-Trainer-Kit

---

## 🏭 About This Build

The goal of this build was to create a compact but realistic OT/ICS training environment using actual industrial control components.

In addition to the original PLC Trainer Kit concepts, this version incorporates a dedicated physical HMI rather than relying exclusively on a software-based HMI.

The physical HMI allows the lab to demonstrate the interaction between:

**Operator → HMI → PLC → Field Devices**

This provides a useful environment for learning both **industrial automation** and **OT cybersecurity** concepts.

---

## 🖥️ C-more CM5 HMI

The primary addition to this build is an:

**AutomationDirect C-more CM5-T7W**

The CM5-T7W is a 7-inch industrial touchscreen HMI that communicates directly with the PLC over the OT network.

The HMI provides operator controls and process visualization for the trainer.

### HMI Functions

The HMI interface can be used to:

- Start the simulated motor/process
- Stop the simulated motor/process
- Display motor/process status
- Display PLC input and output states
- Monitor control logic
- Demonstrate HMI-to-PLC communications
- Demonstrate the relationship between physical controls and HMI controls
- Observe process behavior during OT cybersecurity demonstrations

The HMI communicates with the PLC over Ethernet, providing a realistic example of how operator interfaces interact with controllers in industrial environments.

---

## ⚙️ Lab Components

My version of the trainer includes the following major components:

| Component | Purpose |
|---|---|
| 24 VDC Power Supply | Provides control power for the trainer |
| AutomationDirect CLICK PLC | Executes the control logic |
| AutomationDirect C-more CM5-T7W | Physical operator HMI |
| Ethernet Switch | Provides the OT network |
| Circuit Breaker | Electrical protection |
| Terminal Blocks | Field wiring distribution |
| Control Relays | Interface between PLC outputs and field devices |
| Start Pushbutton | Physical process start |
| Stop Pushbutton | Physical process stop |
| Emergency Stop | Simulated emergency shutdown |
| Reset Pushbutton | Resets the process after an emergency stop |
| 24 VDC Fan / Motor | Represents a plant motor or industrial process |

---

## 🏗️ Simplified Architecture

```text
                     OT / ICS Network
                           │
                    ┌──────┴──────┐
                    │   Ethernet  │
                    │    Switch   │
                    └──────┬──────┘
                           │
              ┌────────────┴────────────┐
              │                         │
        ┌─────▼─────┐             ┌─────▼─────┐
        │   CLICK   │◄───────────►│   C-more  │
        │    PLC    │   Ethernet  │  CM5-T7W  │
        └─────┬─────┘             │    HMI    │
              │                   └───────────┘
              │
       Physical I/O
              │
    ┌─────────┼──────────┐
    │         │          │
 Pushbuttons  Relays   E-Stop
              │
              ▼
        Fan / Motor
```

The trainer represents a simplified industrial environment where an operator interacts with a physical process through both **local controls** and an **HMI**.

---

## 🎛️ Physical Controls

The trainer includes several physical controls commonly found in industrial environments.

### Start

Pressing the **START** pushbutton commands the PLC to start the simulated motor/process.

### Stop

Pressing the **STOP** pushbutton commands the PLC to stop the motor/process.

### Emergency Stop

The **EMERGENCY STOP** is a latching pushbutton.

When activated:

1. The running process is stopped.
2. The emergency-stop condition remains active.
3. Normal start commands are prevented.

To recover:

1. Rotate the Emergency Stop button to unlatch it.
2. Press the **RESET** pushbutton.
3. The PLC clears the emergency-stop condition.
4. The system returns to its normal operating state.

> ⚠️ **Training Lab Notice**
>
> This trainer is intended for educational purposes. The emergency-stop implementation in this lab should not be interpreted as a design example for an actual industrial safety system. Production machinery requires appropriate safety-rated components, engineering, risk assessment, and compliance with applicable standards.

---

## 🧠 PLC Logic

The AutomationDirect CLICK PLC controls the simulated process.

The PLC program handles functions such as:

- Start/stop control
- Motor output control
- Emergency-stop status
- Reset logic
- HMI commands
- HMI status indicators
- Physical pushbutton inputs
- Process state

This makes it possible to compare commands originating from the physical controls with commands originating from the HMI.

---

## 🖥️ HMI Interface

The C-more HMI provides a graphical representation of the process.

Example HMI objects can include:

- START button
- STOP button
- RESET button
- Motor RUNNING indicator
- Motor STOPPED indicator
- Emergency-stop indicator
- PLC communications status
- PLC input indicators
- PLC output indicators
- Process status information

### Screenshot

Add a screenshot of the C-more interface here:

```text
/images/cmore-main-screen.png
```

Example Markdown:

```markdown
![C-more CM5 Main Screen](images/cmore-main-screen.png)
```

---

## 🌐 Network Communications

The PLC and HMI communicate across the trainer's Ethernet network.

Example lab addressing:

| Device | IP Address |
|---|---|
| CLICK PLC | `192.168.x.x` |
| C-more CM5-T7W | `192.168.x.x` |
| Engineering Workstation | `192.168.x.x` |
| Security Workstation | `192.168.x.x` |

> Replace the example addresses above with the addressing used by your build.

The network architecture makes it possible to observe normal PLC/HMI communications and understand how industrial protocols operate.

---

## 🔐 OT Cybersecurity Training

In addition to automation training, this build can be used as an isolated environment for learning about OT cybersecurity.

Potential learning topics include:

- OT network discovery
- Industrial protocol analysis
- PLC/HMI communications
- Packet captures using Wireshark
- Modbus TCP analysis
- Network segmentation
- Asset identification
- Passive OT monitoring
- Detection engineering
- Process manipulation concepts
- Differences between IT and OT security

One of the most important lessons from the lab is that cybersecurity events in an OT environment can have consequences beyond computers and data.

Changes to PLC communications or control logic can potentially affect a **physical process**.

---

## 🦈 Wireshark

Wireshark can be used to observe traffic between components in the lab.

This provides an opportunity to examine:

```text
HMI → PLC
PLC → HMI
Engineering Workstation → PLC
Security Workstation → OT Network
```

Capturing normal traffic first provides a baseline for understanding how the system behaves before experimenting with security scenarios.

---

## 🧪 Example Training Workflow

A typical lab session might look like:

1. Power on the trainer.
2. Verify PLC operation.
3. Verify HMI communication.
4. Start the motor using the physical START button.
5. Stop the motor using the physical STOP button.
6. Start the motor from the C-more HMI.
7. Observe the PLC state from the HMI.
8. Capture PLC/HMI traffic using Wireshark.
9. Activate the Emergency Stop.
10. Observe the PLC and HMI response.
11. Reset the Emergency Stop.
12. Compare normal network traffic with traffic generated during cybersecurity exercises.

This allows students to understand the process **before attempting to analyze or manipulate it**.

---

## 📂 Repository Structure

A suggested structure for this fork is:

```text
PLC-Trainer-Kit/
│
├── CMore-HMI/
│   ├── CMore-Project/
│   ├── Screenshots/
│   └── README.md
│
├── CLICK-PLC/
│   ├── PLC-Program/
│   └── README.md
│
├── Wiring-Diagrams/
│   ├── Electrical/
│   └── Network/
│
├── Images/
│   ├── trainer-front.jpg
│   ├── trainer-back.jpg
│   ├── cm5-hmi.jpg
│   └── cm5-screen.png
│
├── Labs/
│   ├── Basic-Operation/
│   ├── Wireshark/
│   └── OT-Security/
│
└── README.md
```

---

## 📸 My Build

Add several photos showing the completed trainer.

### Front View

```markdown
![PLC Trainer Front](Images/trainer-front.jpg)
```

### C-more HMI

```markdown
![C-more CM5-T7W](Images/cm5-hmi.jpg)
```

### Internal Wiring

```markdown
![PLC Trainer Wiring](Images/trainer-wiring.jpg)
```

Good build photos are particularly useful for others who want to reproduce the modification.

---

## 🔌 Wiring

Wiring diagrams for my build can be found in:

```text
/Wiring-Diagrams/
```

The diagrams document the connections between the:

- Power supply
- PLC
- C-more HMI
- Pushbuttons
- Emergency Stop
- Reset button
- Relays
- Fan/motor
- Ethernet network

---

## 📚 What You Can Learn

This trainer can help demonstrate several layers of an industrial control environment.

### Industrial Automation

- PLC programming
- Ladder logic
- Digital inputs and outputs
- Relays
- Motor control concepts
- HMI development
- Operator controls

### Industrial Networking

- Ethernet-based industrial communications
- PLC/HMI communication
- Modbus TCP
- IP addressing
- Packet analysis

### OT Cybersecurity

- Asset discovery
- Protocol analysis
- Network monitoring
- OT traffic baselining
- Security detection
- Process manipulation concepts
- Network segmentation
- Understanding cyber-physical impact

---

## ⚠️ Safety and Responsible Use

This project is intended for:

- Education
- Cybersecurity training
- Industrial automation training
- Home labs
- Controlled demonstrations
- Authorized security research

All cybersecurity exercises should be performed only against systems that you **own or have explicit authorization to test**.

Do not connect this trainer or security-testing equipment to production OT environments.

Industrial systems control physical processes. Techniques that appear harmless in a laboratory can cause equipment damage, process interruption, or safety hazards when performed against real industrial systems.

---

## 🙏 Credits

This project is based on the excellent **PLC Trainer Kit** created by **Oren Niskin / Packets-or-it-didn't-happen**.

Original repository:

https://github.com/oniskin/PLC-Trainer-Kit

The original project inspired this build and provided the foundation for creating an affordable, hands-on environment for learning PLCs, industrial networking, and OT cybersecurity.

My contribution focuses primarily on extending the trainer with a **physical AutomationDirect C-more CM5-T7W HMI** and documenting how a dedicated operator interface can be integrated into the lab.

If you're interested in building your own trainer, I strongly recommend reviewing the original project and its build guides.

---

## 🚀 Future Improvements

Some additions I may explore in the future include:

- Additional C-more HMI screens
- Alarm and event screens
- Historical process data
- Additional PLC tags
- Network monitoring
- OT intrusion detection
- Additional simulated process equipment
- More realistic plant process scenarios
- Additional cybersecurity labs
- Expanded network segmentation
- Remote engineering workstation
- Industrial firewall integration

---

## 🤝 Contributing

This repository is intended to share ideas with the OT and cybersecurity community.

If you build your own variation, improve the C-more interface, create new PLC logic, develop additional training scenarios, or find another way to expand the trainer, feel free to open an issue or submit a pull request.

One of the best parts of projects like this is seeing how the community takes the original idea and builds something new from it.

---

## 📜 License

This fork retains the licensing requirements of the original PLC-Trainer-Kit project.

See the `LICENSE` file for details.