# bq4847-replacement

**Drop-in replacement for the BQ4847Y DIP RTC chip using the BQ4802Y for 5V legacy systems.**  
Maintains full functionality with modern, readily available components.

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
| 5K Resistor              | Pull-up resistor - 1/4W 5%                       | ~$0.10           | Mouser       |
| Round Pin Headers        | For DIP socket compatibility                     | ~$0.50           | Various      |
| XH 2 pin 2.54mm header   | For hooking up 3V battery & holder (male/female) | $1.00/ea         | [Various - Example](https://www.amazon.com/JST-XH-2-54mm-Connector-Silicone-Cables/dp/B0D6KSMK1Q/) |
| Battery holder - CR2032  | Battery holder w/switch & CR2032 - Backup        | $2.00/ea         | [Various - Example](https://www.amazon.com/LAMPVPATH-cr2032-Battery-Holder-CR2032/dp/B07BXDHT4B) |

---

## License

This project is open hardware. You are free to use, modify, and distribute it, ideally with attribution.  Please see the license file in this repo.

---

## Author

Designed by [hexbus](https://github.com/hexbus).
