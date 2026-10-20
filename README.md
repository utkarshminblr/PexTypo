# Pextypo

Pextypo is my full-size mechanical keyboard project using an **Adafruit Feather nRF52840 Express**.

so this started with wanting a keyboard with all the keys still there.. function row numpad the navigation stuff everything. then i added a little screen and wireless plans and suddenly there was a whole pcb and a case to figure out lol. the electronics are in KiCad and the enclosure is in Fusion 360, with a KMK firmware file for the keyboard side

![Pextypo PCB](Img/Screenshot%202026-10-20%20133006.png)

## why i made this

i wanted to try making the actual keyboard instead of only picking switches and putting them in something already made. keeping the full layout was part of it because i didnt really want to lose the numpad just to make the board smaller

main goals :

- make a custom full-size keyboard PCB
- use the Feather nRF52840 for USB and Bluetooth support
- connect the key matrix through MCP23017 I2C expanders
- add a small colour display above the keys
- include lock indicators and battery status lights
- make a case with seperate printable parts
- keep the firmware, manufacturing files and parts list in the project

the screen is probably my favourite extra bit.. theres code for a pink blossom scene with falling petals so it has a little more personality than a plain status readout. getting the keyboard itself working still comes first obviously

## project status

the saved project has the schematic, routed PCB, case files, screenshots and a firmware implementation. assembly and testing on the actual hardware are still the next step, so the screenshots here show the design rather than a finished working keyboard

whats in this repo :

- `CAD/` - the assembly export and printable case pieces
- `Firmware/` - keyboard source code
- `Fusion File/` - editable Fusion design
- `Img/` - schematic, PCB and case screenshots
- `PCB/` - KiCad project files
- `PDFs/` - exported schematic and board-layer documents
- `production/` - fabrication outputs and component placement data
- `BOM img/` - component sourcing screenshots
- `bom.csv` - shopping list with quantities, prices and suppliers

## hardware summary

| | |
|---|---|
| Project | Pextypo |
| Layout | Full-size mechanical keyboard with numpad |
| Controller | Adafruit Feather nRF52840 Express |
| Connectivity target | USB and Bluetooth LE |
| Matrix | 6 rows x 21 columns in the firmware |
| GPIO expansion | Two MCP23017 devices addressed at 0x20 and 0x21 |
| Switch diodes | 1N4148W in SOD-123 packages |
| Display | Waveshare 1.9-inch SPI IPS LCD, 170 x 320 |
| Indicators | Caps Lock, Num Lock and battery status outputs |
| Battery | 3.7 V 500 mAh LiPo listed in the BOM |
| Switches | Akko V3 Creamy Blue Pro tactile switches |
| Keycaps | XVX Plum Blossom Cherry-profile set listed in the BOM |
| Stabilizers | DUROCK V3 Smokey 80% kit listed in the BOM |
| CAD | Fusion 360, STEP assembly and STL parts |

the two expanders handle the matrix lines so the Feather still has connections available for the display and indicators. the BOM has spare quantities for some parts, so its not a count of exactly whats soldered onto one board

## images

### PCB and switch layout

![Pextypo board layout](Img/Screenshot%202026-10-20%20132538.png)

### PCB routing and board layers

![Pextypo PCB detail](Img/Screenshot%202026-10-20%20132816.png)

![Pextypo routing view](Img/Screenshot%202026-10-20%20132826.png)

![Pextypo board view](Img/Screenshot%202026-10-20%20132848.png)

### schematic

the schematic is split into the matrix and the smaller support sections.. much easier to follow than trying to put every single connection in one tangled block

![Pextypo schematic section](Img/Screenshot%202026-10-20%20131939.png)

![Pextypo support circuit](Img/Screenshot%202026-10-20%20132010.png)

![Pextypo schematic overview](Img/Screenshot%202026-10-20%20132129.png)

### firmware and build screenshots

![Pextypo firmware source view](Img/Screenshot%202026-10-20%20134207.png)

the actual code is in `Firmware/code.py`. this is a source screenshot, so it doesnt mean the full keyboard has passed a hardware test yet

### CAD and case

![Pextypo case assembly](Img/Screenshot%202026-10-20%20171753.png)

![Pextypo case detail](Img/Screenshot%202026-10-20%20171801.png)

![Pextypo enclosure part](Img/Screenshot%202026-10-20%20171810.png)

![Pextypo case part view](Img/Screenshot%202026-10-20%20171814.png)

![Pextypo CAD view](Img/Screenshot%202026-10-20%20171824.png)

## repo file checklist

- `PCB/PexTypo.kicad_pro` - KiCad project
- `PCB/PexTypo.kicad_sch` - schematic
- `PCB/PexTypo.kicad_pcb` - PCB layout
- `CAD/Full/Pextypo.step` - complete exported model
- `CAD/Printable/` - bottom, plate and top plate STLs
- `Fusion File/Pextypo.f3d` - editable enclosure model
- `Firmware/code.py` - KMK keyboard code
- `production/` - manufacturing archive, positions, netlist and generated BOM
- `PDFs/` - schematic and layer exports
- `Img/` - project pictures
- `BOM img/` - sourcing pictures
- `bom.csv` - purchasing BOM

the BOM inside `production/` is the generated board parts list. the one at the repo root is the shopping list with the switches, keycaps and other build parts too

## cad

the enclosure has a bottom shell, a switch plate and a top plate. the editable model is in `Fusion File/` and the print exports are in `CAD/Printable/`

there is also a STEP assembly in `CAD/Full/` for looking at how it all fits together. check the port opening, mounting positions and room around the screen before printing.. a part looking good in the assembly doesnt automatically mean a printed screw fit will be perfect

## firmware note

`Firmware/code.py` uses KMK and the Adafruit MCP23017 library. it defines the 6 x 21 matrix, the base keymap, a second layer and USB/BLE startup with the Bluetooth name `PexTypo`

theres also code for the ST7789 display, blossom animation, battery voltage reading and indicator outputs. those are implemented in the source but still need checking on the actual board with the matching CircuitPython version and libraries

before flashing anything, compare the pins in the file with the schematic and install the required KMK and Adafruit dependencies. there isnt a hardware test result here to say every feature is already sorted

## bom

the parts and supplier links are in [`bom.csv`](bom.csv), and the sourcing screenshots are in `BOM img/`

the saved BOM includes the PCB and printed case along with the electronics and keyboard parts. prices are recorded in USD and are a sourcing snapshot.. shipping, taxes and supplier pack sizes can change what the order actually costs

some of the main bits :

| Part | Purpose |
|---|---|
| Adafruit Feather nRF52840 Express | Run the keyboard and handle USB/BLE |
| MCP23017 | Provide the extra matrix connections |
| 1N4148W | Isolate switches in the matrix |
| Waveshare 1.9-inch IPS LCD | Show the display scene and status information |
| 3 mm LEDs | Lock and battery indicators |
| 500 mAh LiPo | Rechargeable power |
| Akko V3 Creamy Blue Pro | Mechanical switches |
| XVX Plum Blossom set | Keycaps |
| DUROCK V3 kit | Support the larger keys |

