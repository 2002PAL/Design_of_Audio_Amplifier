# Design and Implementation of Audio Amplifier

**---------------------------------------------------------------------------------------------------------------**



## Project Overview

**-------------------------------------**



This project covers the design, simulation, PCB fabrication, and testing of a **Class AB Audio Amplifier** capable of driving a 5W, 4Ω speaker. The system includes a pre-amplifier stage (UA741 op-amp), a high-pass filter to suppress low-frequency noise, and a complementary Class AB push-pull output stage using BD139/BD140 transistors — all implemented on a custom-etched PCB.


## Circuit Architecture

**----------------------------------------------**


\[Audio Input] → \[HPF (fc ≈ 160 Hz)] → \[Pre-Amplifier (Av = 9.2)] → \[Class AB Power Amplifier] → \[Speaker]


### 1\. High-Pass Filter

**--------------------------------------**

* Topology: RC passive filter
* Components: R = 2kΩ, C = 0.5µF (two 1µF caps in series)
* Cutoff frequency: **fc ≈ 160 Hz**
* Purpose: Block DC offset and suppress low-frequency noise/bass



### 2\. Pre-Amplifier (UA741 Op-Amp)

**--------------------------------------------------------------**

* Configuration: Non-inverting amplifier
* Gain: **Av = 1 + Rf/R2 = 1 + 82kΩ/10kΩ ≈ 9.2**
* Input impedance: 1 MΩ (inherent to UA741)
* A virtual ground (voltage divider) is used to enable dual-swing operation from a single 12V supply



### 3\. Class AB Power Amplifier

**------------------------------------------------------**

* Output transistors: **BD139 (NPN)** and **BD140 (PNP)**
* Diode biasing: Two 1N4007 diodes in series (\~1.4V total) to eliminate crossover distortion
* Emitter resistors: 11Ω (limits peak collector current to \~0.8A)
* Inter-stage coupling: 22µF electrolytic capacitor (DC blocking)
* Output coupling: 1000µF electrolytic capacitor



## Design Parameters \& Calculations



|Parameter|Value|
|-|-|
|Supply Voltage (VCC)|12V|
|Speaker Load|5W, 4Ω|
|Peak Output Current|0.8A|
|Power Delivered to Speaker|≈ 1.3W|
|Power Gain|**42.1 dB**|
|Efficiency|**≈ 13.3%**|
|Total Power Drawn|9.8W|
|Pre-amp Voltage Gain|9.2×|

&#x20; \*\*Note:\*\* Efficiency is limited by the high 11Ω emitter resistors (only available value). Lower emitter resistance would significantly improve both output power and efficiency.



## Components Used



|Component|Value / Part No.|
|-|-|
|Op-Amp|UA741|
|NPN Power Transistor|BD139|
|PNP Power Transistor|BD140|
|NPN Switch (relay driver)|BC547|
|Diodes|1N4007|
|Resistors|22Ω, 120Ω, 680Ω, 1kΩ, 16kΩ, 22kΩ, 10kΩ, 82kΩ|
|Capacitors|1µF, 22µF, 1000µF (electrolytic)|
|Speaker|5W, 4Ω|
|Relay|12V|
|Heat Sink|For BD139/BD140|
|PCB|Custom-etched copper cladding board|



## Implementation Tools Used

**----------------------------------------------------------**

* **Multisim** — Circuit simulation and verification
* **EasyEDA** — Schematic design and PCB layout (top + bottom layers)
* **Hantek 6022BE** — Oscilloscope for signal measurement



### PCB Fabrication Process

**----------------------------------------------**

1. Designed schematic in EasyEDA
2. Routed PCB layout (top and bottom copper layers)
3. Printed layout on photo paper, transferred to copper-clad board
4. Etched using **FeCl₃ (Ferric Chloride) solution**
5. Drilled holes and soldered all components



### Power Supply Design

**--------------------------------------**

The circuit supports **dual power input** — battery or 12V DC adapter:

* A **relay** (driven by BC547 in saturation mode) switches between sources
* Normal operation: battery (relay normally closed)
* On 12V DC input: transistor turns on, relay opens to disconnect battery



## Results

**----------------**

* Input signal (≈ 0.2V audio) successfully amplified to drive the speaker
* Output waveform verified on oscilloscope — no significant crossover distortion observed
* **Power Gain: 42.1 dB**
* **Efficiency: \~13.3%**



## Discussion \& Known Limitations

**---------------------------------------------------------------------**

* **Reversed electrolytic capacitors in series** are used at AC stages — this creates an effective bipolar capacitor (halved capacitance, doubled voltage rating), preventing reverse-bias damage
* The 11Ω emitter resistors were used due to component availability; lower values would improve efficiency substantially
* A virtual ground (voltage divider from 12V supply) enables the UA741 to provide symmetric output swing without a dual supply



## References

**-----------------------**

1. *Electronic Principles*, 7th Edition — Albert Malvino \& David J. Bates
2. *Microelectronic Circuits* — Sedra \& Smith
3. Wikipedia, Google



### Author

**------------**



###### **Ritam Pal** — **B.Sc(H) Physics**, University of Calcutta (2022) \&

###### 

###### &#x20;           **B.Tech(ECE)**, Institute of Radiophysics \& Electronics, University of Calcutta (2026)



## License

**----------------**

This project was submitted as part of the B.Tech curriculum at the Institute of Radio Physics and Electronics, University of Calcutta. For academic reference only.

