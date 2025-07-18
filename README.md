# RePromontory - Reuse Promontory
### Aims to reduce e-waste by reusing old EOL motherboard chipsets on PC accessories
---
## Repo Contents:
1. Python script for extracting firmware from UEFI BIOS images
2. Fusion360/KiCad Library (footprints, symbols)
3. Reference Schematic(s)
4. Excel file(s) containing pinout and strapping information

### Proof of Concept
NTR? YES IT WORKS!\
![B660_POC](/images/prom21_on_b660.png?raw=true)\
![M4_POC](/images/prom21_on_mac_via_tbt5.png?raw=true)

### About the firmware
The firmware can be loaded in 3 ways
1. By CPU PSP ABL, Black Box mystery, Who knows how PSP/ABL/SMU works lol
2. By UEFI PEI, PCIe MMIO (ASMIO works too, lol)
3. By OnBoard SPI NOR Flash (We are using this method)


The 8051 boot ROM will read the NOR Flash on the SPI bus after HW-Strapping is done\
The SPI bus is 10MHz, Most SPI NOR Flash will work\
The boot ROM will first read for the header (XXXXX_RCFG) at address 0x06,\
If header, checksum and CRC-32 is correct, ROM will load FW from the SPI NOR Flash.\
Firmware header can be added automaticly by the Python script (extractfw.py)


### About the chipset
The microcontroller inside the Promontory is a mcs-51 compatible core\
Responsible for xHCI/AHCI, PCIe settings, SerDes SI settings and more\
Basic settings can be done via hard-strapping, and SPI FW header\
Complex setting can be done via PCIe MMIO, usually by PEI/DXE module.

More information can be found on:\
PROM Software Programming Note,\
AGESA PI Packages (PEI/DXE)\
But sadly it's all under NDA, and it's not available to the general public :/\
![NDA_NONSENSE](/images/nda_nonsense.png?raw=true)

## Chipset models:
Myth: low-end chipset is not a "defective silicon" but rather has its functionality disabled by eFuse?
| Codename | Part Number | Marketing |
| --- | --- | --- |
| Prom    | 218-0891004 | A320 |
| Prom    | 218-0891005 | B350 | 
| Prom    | 218-0891006 | X370 |
| Prom LP | 218-0891011 | B450 |
| Prom LP | 218-0891008 | X470 |
| Prom 19 | 218-0891015 | A520 | 
| Prom 19 | 218-0891014 | B550 | 
| Prom 19 | 218-0891005 | A620A| 
| Prom 19 | 218-0891026 | B840 | 
| Prom 21 | 218-0891020 | A620 | 
| Prom 21 | 218-0891018 | B650/X670 |


## Author
Rei (霊) (rei@kolabo.dev)\
GitHub / Discord [@himko9] 

## License
This project is licensed under the MIT License - see the LICENSE file for details
