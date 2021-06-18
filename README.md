Radio Net
<table>
  <tr>
    <td><img src="hardware/rev1/DSC_1044.jpg" alt="Top View"></td>
  </tr>
  <tr>
    <td>CaribouLite Hardware SDR mounted on a RPI-Zero with custom firmware</td>
  </tr>
</table>


In our application, each ADC sample contains 13 bit (I) and 13 bit (Q), that are streamed with a maximal sample rate of 4 MSPS from the AT86RF215 IC. This channel requires 4 bytes (samples padded to 32-bit) per sample (and I/Q pair) => 16 MBytes/sec which are 128 MBits/sec. In addition to the 13 bit for each of I/Q, the Tx/Rx streams of data contain flow control and configuration bits. The modem (AT86RF215) IC by Microchip contains two RX I/Q outputs from its ADCs (one for each physical channel - sub-1GHz and 2.4GHz), and a single TX I/Q intput directed to the DACs.


<table>
  <tr>
    <td><img src="hardware/rev2/pictures/cad_image_bw.png" alt="Top View"></td>
  </tr>
  <tr>
    <td>Top & Bottom view, Production Rev2</td>
  </tr>
</table>

**Deeper project details will be published shortly in our Wiki pages.**

# Specifications

<B>RF Channels:</B>
- Sub-1GHz: 389.5-510 MHz / 779-1020 MHz
- Wide tuning channel: 30 MHz - 6 GHz (excluding 2398.5-2400 MHz and 2483.5-2485 MHz)

<table>
  <tr>
    <td><img src="hardware/rev1/frequencies.png" alt="spectra"></td>
  </tr>
  <tr>
    <td style="text-align:center">Applicable spectra, S1G - sub-1GHz, WB - Wide tuning channel</td>
  </tr>
</table>
<B>Note</B>: 
The gaps are defined by the design constraints of the system and may not exist in real-life hardware. Actual modem synthesizer outputs test show wider margins at room temperature than those written in the datatsheet, but, as noted by Microchip, performance may suffer.


<B>FPGA specifications:</B>
- 160 LABs / CLBs
- 1280 Logic Elements / Cells
- 65536 Total RAM bits
- 67 I/Os, Temp: -40-100 degC

<B>Applicable RPI models</B>: RPI_1(B+/A+), RPI_2B, RPI_Zero(Zero/W/WH), RPI_3(B/A+/B+), RPI_4B

Parameter                  |  Sub-1GHz                    | Wide Tuning Channel
---------------------------|------------------------------|------------------------------------------------------------------
Frequency tuner range      | 389.5-510 MHz / 779-1020 MHz | 30 MHz - 6 GHz (excluding 2398.5-2400 MHz and 2483.5-2485 MHz)
Sample rate (ADC / DAC)    | 4 MSPS                       | 4 MSPS
Analog bandwidth (Rx / Tx) | <4 MHz                       | <4 MHz
Max Transmit power         | 14.5 dBm                     | >14 dBm @ 30-2400 MHz, >13 dBm @ 2400-6000 MHz
Receive noise figure       | <4.5 dB                      | <4.5 dB @ 30-3500 MHz, <8 dB @ 3500-6000 MHz

<B>Note</B>: 
(1) Feature comparison table with other SDR devices will be published shortly
(2) Some of the above specifications are simulated rather than tested
(3) Analog bandwidth controlled by the modem

# Board Layout
![2d_nums](hardware/rev1/2d_nums.png)

<B>Description:</B>
1. Raspberry-Pi 40-pin connector
2. A modem - AT86RF215
3. TCXO - 0.5 ppm @ 26 MHz
4. FPGA - ICE40LP series from Lattice Semi.
5. A frequency mixer with integrated synthesizer - RFFC5072
6. External reference clock connector (may be used to acheive coherence between many CaribouLite units.
7. A PMOD connector for FPGA expantion
8. RPI configuration EEPROM (following RPI-HAT specifications)
9. RF front-end - switched, amplifiers, and filters.
10. Reset switch
11. User custom switch + RPI HAT EEPROM reconfiguration (write-enable) switch
12. Wide band SMA connector
13. Sub 1-GHz SMA connector
