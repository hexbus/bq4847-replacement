# BQ4847 Replacement Module

**Drop-in replacement for the BQ4847Y DIP RTC chip using the BQ4802Y for 5V legacy systems.**  
Maintains full functionality with modern, readily available components.

---

## Table of Contents

- [Overview](#overview)
- [Photos](#photos)
  - [Assembled Replacement Module](#assembled-replacement-module)
  - [BQ4802Y Module (Modern)](#bq4802y-module-modern)
  - [BQ4847Y Chip (Original)](#bq4847y-chip-original)
- [Project Status](#project-status)
- [Bill of Materials (BOM)](#bill-of-materials-bom)
- [Installation Instructions](#installation-instructions)
- [License](#license)
- [Author](#author)

---

## Overview

Many legacy computer systems used the BQ4847 real-time clock (RTC) chip—an integrated lithium coin-cell battery-backed chip with a typical 10-year lifespan. Today, most of these original chips are well beyond their intended service life.

This project provides a drop-in replacement using the newer BQ4802Y clock chip. It includes support for a replaceable 3V CR2032 battery via an XH 2-pin connector. Note that while the original BQ4847 supported an external 512K SRAM module, this project does **not** include that memory. However, the BQ4802Y can still manage external SRAM if present.

This design was created specifically for use in the [TI-99/4A IDE Card](http://www.mainbyte.com/ti99/ide_card/ide_card.html), which has a dedicated footprint for the BQ4847.

---

## Photos

### Assembled Replacement Module  
![Replacement Module](https://github.com/hexbus/bq4847-replacement/blob/main/front.png)

### BQ4802Y Module (Modern)  
![BQ4802Y](https://github.com/hexbus/bq4847-replacement/blob/main/bq4802.png)

### BQ4847Y Chip (Original)  
![BQ4847Y](https://github.com/hexbus/bq4847-replacement/blob/main/bq4847.png)

---

## Project Status

🛠️ **Current Status: Prototype phase**  
This design has not yet been tested in hardware. Boards are on order and manual builds are pending.

---

## Bill of Materials (BOM)

| Component                 | Description                                      | Est. Cost (USD) | Source/Link |
|--------------------------|--------------------------------------------------|------------------|-------------|
| PCB                      | Found in `gerbers.zip` in this repo              | —                | —           |
| BQ4802Y RTC chip         | Main RTC IC                                      | ~$6.25           | [Mouser](https://www.mouser.com/ProductDetail/Texas-Instruments/BQ4802YPW?qs=YxwvVplHM%2FnrYmh0JbPldA%3D%3D) |
| 32.768 kHz Crystal       | Standard watch crystal for RTC - 8mm tall        | $0.20–$0.40      | Mouser       |
| 5K Resistor              | Pull-up resistor - 1/4W 5%                        | ~$0.10           | Mouser       |
| Round Pin Headers        | For DIP socket compatibility                     | ~$0.50           | Various      |
| XH 2 pin 2.54mm header   | For hooking up 3V battery & holder (male/female) | $1.00/ea         | [Example](https://www.amazon.com/JST-XH-2-54mm-Connector-Silicone-Cables/dp/B0D6KSMK1Q/) |
| Battery holder - CR2032  | Battery holder w/switch & CR2032 - Backup        | $2.00/ea         | [Example](https://www.amazon.com/Alinan-Button-Battery-Storage-Container/dp/B09KTVG1Y5) |

---

## Installation Instructions

### BQ4802 Clock Installation for the TI-99/4A IDE Card

1. **Remove the original BQ4852**  
   Carefully remove the original clock chip and SRAM from IC27 by pulling straight up.

2. **Install SRAM**  
   Ensure a [512Kx8 SRAM chip](https://www.mouser.com/ProductDetail/727-CY2148ELL45ZSXIT) is installed at IC23.

3. **Install Capacitors**  
   Make sure two 0805 SMD capacitors are installed:
   - **C23** — for the SRAM
   - **C25** — for the new clock chip (BQ4802)

4. **Insert the BQ4802 Clock Chip**  
   Place the BQ4802 into the BQ4847 socket:
   - Align the dot on the BQ4802 with the cutout on the silkscreen (facing C25 and the top edge of the IDE card).
   - The crystal and resistor should be located above the BQ4802 chip.

5. **Attach the Battery**  
   - Connect the battery to the 2-pin connector, observing polarity (**+ is on the left**, per silkscreen).
   - Mount the battery holder nearby using double-stick tape.
   - Leave the battery switch **OFF** for now.

6. **Set the IDE Switch**  
   - Turn the primary IDE switch (rear of the card) to the **OFF** position (usually the middle setting).

7. **Power On System**  
   - Power on your **Peripheral Expansion System**.
   - Power on your **TI-99/4A** and wait for the Master Title Screen.
   - Flip the IDE card switch to **TI** (if using a TI system).

8. **Load the DSR**  
   - Run `IDELOAD` to detect and load the DSR.

9. **Verify Battery Backup**  
   - If successful:
     - Turn the **battery switch ON**
     - Power down and back up.
     - Run `CALL IDEST` or `CALL IDETD` in BASIC to check if date/time was retained.

10. **Troubleshooting**  
    - If unsuccessful:
      - Double-check all connections.
      - Use a multimeter to verify continuity.
      - Confirm that the DSR is still loaded.
      - Use community forums such as the [TI-99/4A Forum on AtariAge](https://forums.atariage.com/forum/164-ti-994a-computers/) for assistance.

---

## License

This project is open hardware. You are free to use, modify, and distribute it, ideally with attribution. Please see the license file in this repo.

---

## Author

Designed by [hexbus](https://github.com/hexbus).
