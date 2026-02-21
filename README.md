# esp8266-wifi-deauthenticator-project

# ESP8266 WiFi Security Testing Device


<img width="654" height="871" alt="image" src="https://github.com/user-attachments/assets/5e22ea88-c599-4c77-85c4-da8fcd219743" />

<img width="1161" height="871" alt="image" src="https://github.com/user-attachments/assets/a2425482-1911-44fa-9b2b-6c54ea4a1ae8" />

<img width="1161" height="871" alt="image" src="https://github.com/user-attachments/assets/77246c81-e18c-4344-aa22-acca3827d402" />

<img width="1161" height="871" alt="image" src="https://github.com/user-attachments/assets/71cb8a38-bdf4-41b1-b14f-57dd01eddb8d" />


A portable, battery-powered WiFi security testing device built around the ESP8266 microcontroller with custom OLED interface and physical button controls.

## Educational Purpose & Legal Disclaimer

**This project is strictly for educational purposes and authorized security testing only.**

This device should only be used:
- On networks you own
- On networks where you have explicit written permission to test
- In controlled lab environments for learning

**Unauthorized access to computer networks is illegal** under:
- India: IT Act 2000, Section 43
- USA: Computer Fraud and Abuse Act
- Japan: Unauthorized Computer Access Law
- Most countries worldwide

**I do not condone or support malicious use of this technology.**

---

## Project Overview

This project began as self-directed learning in network security and embedded systems. I wanted to understand:
- How WiFi networks can be vulnerable to denial-of-service attacks
- The 802.11 deauthentication vulnerability in wireless protocols
- How to design portable security testing hardware
- Embedded systems programming and hardware integration

**Timeline:** Built in 2024 as part of my cybersecurity education

---

## Hardware Design

### Components

- **Microcontroller:** NodeMCU ESP8266 development board
- **Display:** 128x64 OLED (I2C interface)
- **Input:** 3x tactile push buttons for menu navigation
- **Power:** 18650 Li-ion battery with charging circuit
- **Connectivity:** External 2.4GHz antenna with U.FL connector soldered to on-board antenna
- **Circuit Design:** Initial Prototyping done on a breadboard. Currently mounted on a Prototyping board.
- **Enclosure:** Bound in electrical tape and plastic film to allow further adjustments

### Key Features

 **Portable & battery-powered** - No computer needed for operation
 **Physical interface** - OLED display + buttons for standalone use
 **Extended range** - External antenna for better signal
 **Compact design** - Fits in pocket, professional appearance

---

## Software Architecture

### Core Functionality

The device operates by:
1. Scanning for WiFi networks and connected devices
2. Sending deauthentication frames to test network resilience
3. Displaying results on OLED screen in real-time
4. Allowing user control via button-based menu system

### Technical Implementation

**Firmware base:** Built on ESP8266 Deauther firmware (open-source WiFi security tool)

**My modifications:**
- Integrated OLED display driver (I2C communication)
- Developed button-based menu navigation system
- Customized UI for small screen real-time feedback
- Implemented battery management indicators
- Optimized for standalone operation without web interface

**Key libraries used:**
- ESP8266WiFi (network operations)
- Adafruit_SSD1306 (OLED display)
- Wire (I2C communication)

---

## Build Process

### Evolution: Dev Board → Handheld Device

**Phase 1: Breadboard Prototype**
- Tested ESP8266 with basic deauth firmware
- Verified WiFi functionality and range

**Phase 2: OLED Integration**
- Added I2C OLED display
- Developed menu system for button navigation
- Tested display updates and user flow

**Phase 3: Enclosure Design**
- Designed compact case for all components
- Integrated battery and charging circuit
- Added external antenna for improved performance
- Final assembly and testing

---

## Learning Outcomes

### Technical Skills Gained

**1. Embedded Systems Programming**
- ESP8266 Arduino framework
- I2C protocol for peripheral communication
- Memory-constrained programming (OLED buffering)
- Power management for battery operation

**2. WiFi Protocol Understanding**
- 802.11 management frame structure
- Deauthentication attack mechanism
- Why WPA3 with Management Frame Protection (802.11w) prevents this
- Difference between encryption (WPA2) and authentication (management frames)

**3. Hardware Integration**
- Soldering and circuit assembly
- Button debouncing and input handling
- Display multiplexing and refresh rates
- Antenna impedance matching and RF considerations

**4. Security Research Methodology**
- Responsible disclosure principles
- Controlled testing environments
- Documentation and ethical considerations
- Legal frameworks around security research

### Key Insights

**Why This Vulnerability Still Exists:**
- 802.11 deauthentication frames are unauthenticated in WPA2
- Legacy device compatibility prevents immediate protocol changes
- WPA3 solves this with mandatory Management Frame Protection
- Many IoT devices still use vulnerable protocols

**Defense Mechanisms:**
- Enable WPA3 where possible
- Implement 802.11w (Management Frame Protection)
- Use intrusion detection systems to monitor for deauth attacks
- Educate users about WiFi security fundamentals

---

## Ethical Considerations

### Why I Built This

As a high school student interested in cybersecurity, I wanted to:
- Understand network vulnerabilities from first principles
- Learn embedded systems development
- Test my own home network security
- Explore the intersection of hardware and software security

### Responsible Use

**What I learned about ethics in security research:**

1. **Knowledge ≠ Permission**
   - Understanding a vulnerability doesn't justify exploiting it
   - Always obtain explicit authorization before testing

2. **Education Requires Responsibility**
   - Security knowledge is powerful and must be used ethically
   - Projects like this should improve security, not harm users

3. **Transparency Matters**
   - Documenting methodology helps others learn responsibly
   - Open discussion of vulnerabilities drives better security standards

### Moving Forward

This project taught me that **engineers have ethical obligations**. Every tool can be used constructively or destructively. I built this to:
- Learn how systems fail (so I can build better ones)
- Understand defense mechanisms (not to bypass them)
- Pursue formal education in security engineering

This experience solidified my decision to study computer engineering at university, where I can learn proper security research methodologies within ethical frameworks.

---

## How It Works

### 802.11 Deauthentication Attack

**The Vulnerability:**

WiFi networks use management frames to control connections. In WPA2 and older protocols, these frames are **not authenticated**, meaning anyone can send forged deauthentication packets pretending to be the access point.

**Attack Flow:**
1. Device scans for nearby access points and connected clients
2. User selects target network via OLED menu
3. Device sends spoofed deauthentication frames
4. Clients disconnect, thinking the AP requested it
5. OLED displays attack status and results

**Why This Works:**
- Management frames lack cryptographic protection in WPA2
- Clients trust deauth frames without verification
- This is a protocol flaw, not a configuration issue

**Why This Doesn't Work on Modern Networks:**
- WPA3 includes mandatory Management Frame Protection (802.11w)
- Protected frames are encrypted and authenticated
- Spoofed frames are rejected by both AP and clients

---

## Related Resources

### Learning Materials

This project was informed by:
- [ESP8266 Deauther Project](https://github.com/SpacehuhnTech/esp8266_deauther) - Original firmware base
- 802.11 protocol specification (IEEE 802.11-2020)
- Online cybersecurity courses in ethical hacking (Z-Security)
- Network security research papers


---

## Future Improvements

### Planned Modifications

**Hardware:**
- [ ] Add SD card for packet capture logging
- [ ] Integrate GPS module for location tracking
- [ ] Implement rechargeable battery with USB-C
- [ ] Design custom PCB instead of dev board

**Software:**
- [ ] Add WPA3 network detection and reporting
- [ ] Implement packet capture and analysis features
- [ ] Create data visualization for network mapping
- [ ] Develop companion mobile app for configuration

**Research:**
- [ ] Test effectiveness against various router models
- [ ] Measure power consumption for battery optimization
- [ ] Compare external antenna vs. onboard performance
- [ ] Document mitigation strategies for different scenarios

---

## Contact

This project was developed as part of my self-directed cybersecurity education in 2024. For questions about responsible security research or this educational project, feel free to reach out.

**Author:** Sidakdeep Singh Chahal
**GitHub:** [@CrapperDapper](https://github.com/CrapperDapper)

---

## Acknowledgments

- [SpacehuhnTech](https://github.com/SpacehuhnTech) for the ESP8266 Deauther firmware foundation
- Online cybersecurity communities for educational resources
- Open-source contributors to ESP8266 Arduino core and libraries

---

**Final Reminder:** This repository is for educational purposes. The author is not responsible for misuse of this information. Always obtain proper authorization before testing security tools on any network.
