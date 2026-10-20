# SONOFF ZBM5-1C-86W: Always-On Blue LED Modification

A simple hardware modification for the SONOFF ZBM5 Zigbee smart wall switch (1-, 2- and 3-gang versions) that makes its blue LED stay on continuously.

The modification described here was tested by the author on their own switch. The physical location of the blue LED varies by gang/version, but the same LED-drive circuit is used.

In SONOFF ZBM5 switches, the position of the blue LED depends on the number of gangs the switch has (LEDs 6–8). There is a single blue LED in each unit, and it is driven by the same circuit.

![default](images/source-image-01.png)

![default](images/source-image-02.png)

> **Warning — mains-powered equipment.** This modification requires opening and soldering a mains-powered wall switch. Disconnect it completely from mains power before opening it. Do not work on the device while it is connected to mains. This modification is at your own risk and may damage the device, affect its warranty, and compromise its safety if performed incorrectly.

## What this modification does

The blue LED is driven through this path:

`Zigbee IC GPIO → R10 (1 kΩ) → Q4 (A2SHB MOSFET) → blue LED → R14 (1.5 kΩ) → +3.3 V`

In the original circuit, the Zigbee IC controls Q4, which switches the LED. The modification removes Q4 and installs a **680 Ω resistor** in its place between the LED's switched side and GND. This provides a permanent current path, so the blue LED remains on.

**Trade-off:** the switch's blue network-indicator function is lost. The LED no longer indicates Zigbee network status.

## Parts and tools

- 680 Ω resistor (for the always-on blue LED modification)
- Soldering tools suitable for small SMD components
- Magnification and suitable ESD precautions

The board also has an existing R14 current-limiting resistor marked as 1.5 kΩ.

## Procedure

1. Disconnect the switch completely from mains power and remove it from its installation.
2. Open the enclosure carefully.
3. Locate Q4, marked **A2SHB**, in the blue-LED driver circuit. The blue LED's physical position differs between 1-, 2- and 3-gang versions; consult the photos and trace the circuit rather than relying only on the LED reference number.
4. Remove Q4.
5. Solder a **680 Ω resistor in the place of Q4**, connecting the LED's switched-side pad to GND as shown in the modified schematic.
6. Inspect the soldering carefully for bridges, lifted pads and unintended connections before reassembly.
7. Reassemble the switch fully before reconnecting it to mains power.

Do not rely on component position alone: verify the actual pads and circuit connections on your board before soldering.

## Adding an extra indicator LED on multi-gang versions

For multi-gang versions, an additional LED can be installed under a button, if desired. The author's notes specify an LED with approximately **2.5 V forward voltage at 5 mA**. In this arrangement, the additional 680 Ω resistor may be omitted, as shown in the author's diagram.

Verify the LED polarity and current path for your particular board before making this change.

## Reference images

The images in [`images/`](images/) were extracted from the author's original document and show the switch variants, PCB locations, original driver circuit and modified circuit.

## Scope and limitations

- This is a hardware modification, not a Zigbee2MQTT or Home Assistant software setting.
- The network-indicator function is sacrificed.
- Board layouts and blue-LED placement can vary between versions.
- The component values and procedure reflect the author's documented build; they are not a manufacturer-approved modification.

## Contributions

If you test this on another ZBM5 variant, please share the exact model/board revision, clear photos before and after modification, and the measured result.
