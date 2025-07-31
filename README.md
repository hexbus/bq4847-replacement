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
  - [TI-99/4A IDE Card](#bq4852-ti99-ide-card)
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

### BQ4852 TI99 IDE Card

Many early TI-99/4A IDE cards were populated with the **BQ4852**, a combination real-time clock (RTC) and 512K SRAM chip with an internal, non-replaceable battery. At this point, most of these batteries are long dead.

These instructions assume you're replacing the BQ4852 with a modern alternative using one of the other supported clock headers on the IDE card—most commonly the **BQ4802** in the **BQ4847-compatible socket**. Unlike the BQ4852, the BQ4802 (and most other supported options) do **not** include integrated SRAM. To maintain compatibility, the card’s original designer included a footprint at **IC23** to add external 512K SRAM.

If you're installing a clock chip **without built-in SRAM**, you'll need to populate IC23 with a compatible SRAM chip. The following steps walk through the full replacement process.

---

1. **Remove the Original BQ4852**  
   Carefully remove the BQ4852 from **IC27** by pulling it straight up. This removes both the clock and built-in SRAM.

2. **Install External SRAM**  
   Populate **IC23** with a [512Kx8 SRAM chip](https://www.mouser.com/ProductDetail/727-CY2148ELL45ZSXIT).

3. **Install Required Capacitors**  
   Solder two [0805 0.1uf surface-mount capacitors](https://www.mouser.com/ProductDetail/KEMET/C0805C104M5RAC7210?qs=sGAEpiMZZMvsSlwiRhF8qsKzCboK%252BzaMcQGghezj1XY%3D):
   - **C23** — decoupling for the SRAM at IC23
   - **C25** — decoupling for the new clock chip at the BQ4847 socket

4. **Insert the BQ4802 Clock Chip**  
   Insert the BQ4802 into the **BQ4847 socket**:
   - Align the dot on the chip with the notch in the silkscreen (facing **C25** and the top edge of the IDE card).
   - The crystal and resistor should be installed just above the chip.

5. **Attach and Secure the [Battery Holder](https://www.amazon.com/Alinan-Button-Battery-Storage-Container/dp/B09KTVG1Y5?th=1)**  
   - Connect a CR2032 battery holder to the 2-pin XH 2.54mm female header and insulate appropriately.
   - Ensure correct polarity (**+ on the left**, per the silkscreen).
   - Mount the battery holder securely nearby using double-sided tape.
   - Leave the **battery switch OFF** during initial testing.

6. **Set the IDE Card Switch**  
   - Set the rear **IDE switch** to the **OFF** position (usually the center setting).

7. **Power On the System**  
   - Power on your **Peripheral Expansion System (PEB)**.
   - Power on your **TI-99/4A** and wait for the Master Title Screen.
   - Flip the IDE card’s switch to **TI** (if using a TI-compatible configuration).

8. **Load the IDE DSR**  
   - Run `IDELOAD` to detect and initialize the IDE card’s DSR (Device Service Routine).

9. **Test Battery Backup Functionality**  
   - If the DSR loads successfully:
     - Turn the **battery switch ON**.
     - Power down the system, then power it back up.
     - In BASIC, run `CALL IDEST` or `CALL IDETD` to verify the date and time were retained.

10. **Troubleshooting Tips**  
    - If the DSR does not load or the clock fails to retain time:
      - Recheck all IC placements and capacitor installations.
      - Use a multimeter to verify connectivity and power.
      - Confirm the DSR is still present by rerunning `IDELOAD`.
      - Seek help via community resources like the [TI-99/4A Forum on AtariAge](https://forums.atariage.com/forum/164-ti-994a-computers/).

---

## License

This project is open hardware. You are free to use, modify, and distribute it, ideally with attribution. Please see the license file in this repo.

---

## Author

Designed by [hexbus](https://github.com/hexbus).
