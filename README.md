# SPECTRUM SEALS

SPECTRUM SEALS is a modular RF/security monitoring prototype built around distributed edge nodes, local evidence collection, and a central operator dashboard.

The project is being built in phases. The current focus is real hardware validation for Node 1 and Node 2 while keeping the architecture ready for a larger UART/MQTT-backed field system.

## Current system status

### Node 0 / Temporary Core

The laptop currently acts as the temporary operator core during development.

It is used for:

- local dashboards
- Python testing tools
- SDR command-line tools
- evidence review
- GitHub/project documentation

The long-term core target is a Raspberry Pi 5 running the main services.

### Node 1 / Ghost Seal

Node 1 is the ESP32/Pi Zero sidecar node.

Current purpose:

- Ghost Seal firmware control
- USB serial command bridge
- GPS/status/event reporting
- future UART backbone support
- future Marauder-compatible command parity

Current working chain:

```
Ghost Seal ESP32
→ USB serial
→ Node 1 Pi Zero
→ LAN/MQTT
→ Core services
```

Future chain:

```
Ghost Seal ESP32
→ Node 1 Pi Zero
→ UART backbone
→ Pi 5 core
```

### Node 2 / RF RAGNAR

Node 2 is the RF evidence and SDR lane.

Current purpose:

- RTL-SDR / NESDR receive evidence
- HackRF sweep evidence
- automatic RF watch
- basic drone-band RF activity scoring
- spectrum/waterfall evidence export

Current Node 2 repo:

```
Spectrum-SEALS-Node2
```

Current milestone:

```
RAGNAR V4 Autowatch
```

The Node 2 detector reports RF-band activity from real sweep artifacts. It does not claim confirmed drone identity without stronger signatures.

## Current hardware lanes

### SEAL-RTL

RTL-SDR / NESDR lane.

Used for:

- `rtl_power` sweeps
- 433 MHz observation
- 902–928 MHz observation
- archived `rtl_433` decode review

### SEAL-HRF

HackRF lane.

Used for:

- `hackrf_info` device detection
- `hackrf_sweep` capture
- 915 MHz sweep coverage
- 2.4 GHz sweep coverage
- 5.8 GHz sweep coverage

## Design rules

- Real evidence must be separated from simulated evidence.
- A detector may report RF activity, but should not claim confirmed drone identity without stronger supporting signatures.
- Node commands and JSON events should stay consistent across USB serial, UART, HTTP, and MQTT transports.
- Every node should eventually expose a UART-ready control/data path to the Pi 5 core.
- Missing optional tools should degrade gracefully instead of breaking the whole system.

## Current milestone

The current milestone is a working Node 2 RF evidence console with:

- RTL-SDR hardware detection
- HackRF hardware detection
- real sweep capture
- spectrum/waterfall evidence
- basic RAGNAR V4 drone-band activity scoring
- evidence JSON export

## Next milestones

1. Clean the GhostSeal repo documentation.
2. Finish Ghost Seal command parity tracking.
3. Keep Node 2 RAGNAR V4 evidence workflow stable.
4. Add stronger RF classification logic.
5. Add UART backbone documentation.
6. Link Node 1 and Node 2 into the main SPECTRUM SEALS architecture map.

## Project framing

This project is a defensive RF/security prototype.

The goal is to build a modular system that can collect, score, visualize, and preserve RF/security evidence from multiple field nodes.
