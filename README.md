# Dual Bracket for T41 Modules

 ![Dual Bracket](./Dual_Bracket.png)

This is a Freecad file design of a dual bracket for the T41 Software Defined Transceiver.
This bracket was designed to hold a QSD and a QSE module, however, it could be used to combine
other modules to create a "super module".

Freecad can be downloaded here:

<https://www.freecad.org/>

An STL file is included in the repository in addition to the Freecad design file.

## Divide-by-2 versus Divide-by-4



## Implementation of the Divide-by-2 Quadrature

Once again you don't get something for nothing, and the divide-by-2 quadrature circuit requires a
little more effort.

Divide-by-2 requires a clock signal and the inverted clock signal.  This is easy enough to provide
using an inverter integrated circuit:

<https://www.ti.com/lit/ds/symlink/sn74lvc1g14.pdf>

So providing the inverted clock signal is easy.  However, one solution creates a new problem!
The inverter creates a small delay in the inverted signal.  This affects the quality of the quadrature.
However, this is easy to compensate for.  Simply add another inverter to the output to "match" the delays.
So we have to add two these inexpensive devices in addition to the same flip-flop device used by divide-by-4.

The divide-by-2 circuit was simulated and found to produce acceptable quadrature.

For optimal quadrature circuit performance, the coaxial cable between the Main board and the QSD2 should be
as short as possible.

### Why is it called QSE2DC?


#### Carrier Nulling


### Software Modifications for Divide-by-two


### Software Modifications for Carrier Calibration


### T41EEE Arduino Sketch with Special Features for QSEDC


## A Summary of Methods to Extend the T41 Frequency Range

1.  Change the bias voltage on the 74AC74 from 3.3 volts to 5.0 volts.  Change the multiplexer IC to a part
specified for 5.0 volt operation.  This changes increases the frequency response of the flip-flop device.
2.  Change the 74AC74 to a device specified for higher frequencies while leaving the bias at 3.3 volts.  The
device is the 74LVC74.  The specification sheet is here:  <https://assets.nexperia.com/documents/data-sheet/74LVC74A.pdf>.
3.  Change the divide-by-4 circuit to the divide-by-2 circuit as described above.  This circuit is slightly more complex,
however, it has large margin to the upper frequency limits of the components at 10 meters.  6 meter operation may be possible.
There is no known low-frequency limit to the divide-by-2 (or divide-by-4) circuit.
4.  The T41 V012 design generates quadrature using an internal phase-shift circuit, such that one clock output is in-phase
and another clock output is shifted by 90 degrees.  This is directly applied to the multiplexing (demodulator) device,
and thus this circuit is very simple.  This also exploits the maximum upper frequency range of the Si5351 phase-lock-loop IC.  
On the other hand, this introduces a low frequency limit and it may not be possible to cover the LF and VLF amateur bands with this scheme.

## Other Changes to the QSE2DC Circuit Design

The QSE2DC exciter module circuitry is almost entirely revised compared to its ancestor the V011 QSE.

### Pi RF Attenuator

### Differential Operational Amplifiers with Low-Pass Filter

## Bill Of Material (BOM)

A public Digikey BOM is here:

<https://www.digikey.com/en/mylists/list/0OK3JOSXY7>

Please note that specific parts may or may not be available when attempting to order.  It is the responsibility of the builder
to find subsitutes as required.

### Transformer TR2

The transformer TR2 should be placed with the "dot" at the upper left corner.  If you are using the ADT1-1+, it appears
to be symmetrical, so the orientation shouldn't matter.  However, other transformers may require a specific orientation.

### 74AC74 Dual Flip-Flop U4

Pin 1 should be in the lower left corner.  This is marked with a small white dot on the PCB.

### 3253 Multiplexer U3

Pin 1 is at the upper right.  Look for a small white dot next to pin 1.

### Differential Amplifiers AD8137 U5 and U9

Pin 1 indicated with a dot on the PCB.  Both parts are oriented the same, with Pin 1 towards the upper right.
There is a dot on the parts to indicate Pin 1, however, it is very hard to see.  The package is beveled on the Pin 1 side; this is easy to see.

### Non-placed Parts

Don't place R3.  Placing this jumper implements shutdown of the differential amplifiers during receive.  This feature has not been
tested.

Don't place J7, R5 and R7.  These parts will be used with a future Main board with I2C output for routing to an Si5351 module.

The two-pin header J6 can be optionally placed if it is convenient to route the TXRX signal from the QSEDC board.

### Bottom Side Parts

There are 4 capacitors on the bottom side of the PCB.  These should be soldered last.  I was able to use a hot air gun without
any problems with the top-side components desoldering.

### High Resolution Photos of QSE/QSD/Si5351 Module Assembly using Dual Bracket

Links to photos of a fully constructed QSE2DC follow.  Please note that this board has some small differences compared to the
published design files.

<https://drive.google.com/file/d/1RiFj8eh0M4xpLRnGe3M7R_jGNsO_mgoc/view?usp=sharing>

<https://drive.google.com/file/d/1a_t5G4x1_PzWmMshmwpoerwPoXeARqb_/view?usp=sharing>




