# RFID-Authenticated-Mini-Music-Player-with-Cloud-Powered-Recommendations
Final Embedded Systems Project   
EGR 3328 – Embedded Systems  
Al Akhawayn University  
---
## Project Overview

This project presents a portable embedded music player that integrates RFID-based authentication with cloud-powered personalized recommendations.
The system identifies users through RFID tags, communicates with a cloud backend to retrieve individualized playlists, and delivers offline audio playback through a microcontroller-based architecture built around the Particle Photon.

The objective was to combine tangible user interaction, embedded systems engineering, and cloud-based intelligence into a cohesive IoT product.
---

## Team Project & Individual Contributions

This project was developed as part of a team for the Embedded Systems course at Al Akhawayn University.

My primary technical contributions included:

- Designing and implementing the firmware state machine architecture
- Integrating cloud communication via Particle Cloud events
- Engineering reliable playback state tracking mechanisms
- Debugging DFPlayer Mini library limitations
- Implementing OLED-based user interface logic
- Coordinating multi-protocol peripheral communication (SPI, I²C, UART, IR)

Due to collaborative development and academic integrity considerations, the full source code is not publicly released. This repository documents the system architecture, technical decisions, and implementation details.
---
## Problem Statement
Modern music consumption primarily relies on multifunctional devices such as smartphones, which introduce:
- Distraction-heavy listening environments  
- Dependence on Wi-Fi and battery availability  
- Limited tangible interaction  

This project addresses these limitations by designing a dedicated, RFID-triggered music player that:
- Enables offline playback reliability  
- Supports personalized recommendation retrieval via cloud integration  
- Promotes focused, interruption-free listening  
---
## System Architecture
The system follows a layered embedded architecture:
### 1. Input Layer
- RFID Reader (ISO/IEC 14443-A)
- IR Remote Receiver (38 kHz)
### 2. Processing Layer
- Particle Photon Microcontroller
  - ARM Cortex-M3 @ 120 MHz
  - 1 MB Flash
  - 128 KB RAM
### 3. Communication Layer
- Wi-Fi module (integrated)
- Particle Cloud event publishing/subscription
- REST-based recommendation retrieval
### 4. Output Layer
- DFPlayer Mini MP3 Decoder
- PAM8406 Class-D Audio Amplifier
- SSD1306 OLED Display
### 5. Power Layer
- 5V USB power supply
- Shared-ground design to ensure signal stability
- 
(Architecture diagram available in `/docs/architecture-diagram.png`)
---
## Firmware Architecture
The firmware implements a deterministic state-driven architecture.
### System States
- `LOCKED`
- `TRACK_SELECTION`
- `NOW_PLAYING`
- `LOADING`
- `RECOMMENDATIONS`
State transitions are triggered by:
- RFID authentication events
- IR input signals
- Track completion signals (BUSY pin monitoring)
- Cloud response callbacks

This modular state-machine design ensured:
- Predictable system behavior
- Simplified debugging
- Clear separation of UI and playback logic
---
## Peripheral Communication
The system coordinates multiple communication protocols simultaneously:
- SPI → RFID Reader
- I²C → OLED Display
- UART → DFPlayer Mini
- Digital Input → IR Receiver
- Wi-Fi → Cloud communication
Managing timing and synchronization across heterogeneous protocols was a key engineering challenge.
---
## Cloud Integration Workflow
1. User taps RFID card
2. UID is validated locally
3. Device publishes recommendation request event
4. Cloud backend generates personalized playlist
5. Device subscribes to and processes the recommendation response
6. UI updates dynamically
Cloud latency was evaluated qualitatively under varying network conditions and remained acceptable for user-triggered interactions.
---
## Engineering Challenges & Solutions
### 1. DFPlayer Library Limitations
**Problem:** Unreliable playback status reporting  
**Solution:** Replaced getter-based logic with internal state tracking and BUSY pin monitoring
### 2. FAT File Ordering Instability
**Problem:** File playback order inconsistent due to FAT indexing  
**Solution:** Applied FAT sorting after each SD card modification
### 3. Lack of Native Pause/Resume
**Problem:** No hardware-level resume support  
**Solution:** Implemented silent-track workaround to simulate pause behavior
### 4. Limited OLED Display Space
**Problem:** Text overflow and UI constraints  
**Solution:** Implemented pagination and ping-pong scrolling algorithm
---
## Performance Evaluation
- RFID detection range: 3–5 cm (consistent with module specifications)
- Authentication reliability: No false positives observed
- Audio output quality: Significantly improved with an external Class-D amplifier
- Cloud responsiveness: Stable under moderate Wi-Fi conditions
---
## Technical Highlights
- Multi-protocol embedded system coordination
- Event-driven IoT architecture
- Deterministic state-machine firmware design
- Hardware-software co-debugging
- Real-time peripheral synchronization
- Practical mitigation of third-party hardware limitations
---
## Design Trade-Offs
- Wi-Fi dependence introduces latency but enables personalization
- DFPlayer module simplicity limits advanced playback control
- OLED resolution constrains UI richness but minimizes power consumption
These constraints influenced architectural decisions throughout development.
---
## Future Improvements
- Multi-user RFID profile database
- Custom PCB implementation
- Offline recommendation caching
- Bluetooth audio streaming
- Alternative audio module with true pause/resume
- Mobile companion application
---
## Demonstration
Functional prototype demonstration video:
https://youtu.be/llldBQZ3HOI
---
## Key Learning Outcomes
- Hardware constraints strongly influence software architecture
- Embedded UI design requires memory-aware rendering strategies
- Cloud integration introduces latency-reliability trade-offs
- State-machine modeling significantly simplifies complex interaction logic
- Real-world debugging often requires creative engineering workarounds
---

