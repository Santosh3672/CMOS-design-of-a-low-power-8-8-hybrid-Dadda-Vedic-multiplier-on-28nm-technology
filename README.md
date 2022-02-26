# CMOS design of a low power 8×8 hybrid Dadda Vedic multiplier on 28nm technology
This repository presents the CMOS design of a low power 8×8 hybrid Dadda-Vedic multiplier on 28nm technology using Synopsys Custom compiler

## Table of content 
 * [Abstract](#Abstract)
 * [Design Detail](#Design-Detail)
 * [Low power full Adder](#Low-power-full-Adder)
 * [Low power half adder](#Low-power-half-adder)
 * [Design of 4x4 Dadda multiplier](#Design-of-4x4-Dadda-Multiplier)


## Abstract
 Multiplication is a commonly used arithmetic operation; hence a multiplier is used in most digital systems like ALU of Microprocessor,  DSP applications such as image processing, and arithmetic related operation. A multiplier is a significant design that primarily uses full adders and half adders that consume a large portion of the area and power of the design. In this report, we have designed an 8×8 Dadda-Vedic tree multiplier with the advantage of the Dadda multiplier [[1](#Reference)] by utilizing less full adder and half adder than conventional Wallace tree design [[2](#Reference)] and also uses the advantage of the scalability of a Vedic multiplier. We have also presented an energy-efficient full adder [[3](#Reference)] and a half adder that we are using in our design. We have used Synopsys custom compiler tool for the design using 28nm technology libraries.

## Design Detail
## Low power full Adder
Conventional full adder designed using gates (Fig.1) converted into CMOS level design are not optimized designs. As per the diagram below, a full adder requires 2 XOR gates(12 CMOS each), 2 AND gates(6 CMOS each) and 1 OR gate(6 CMOS each), so a complete full adder design has 36 CMOS.

<p align="center">
<img src="https://github.com/Santosh3672/CMOS-design-of-a-low-power-8-8-hybrid-Dadda-Vedic-multiplier-on-28nm-technology/blob/main/FA_GATES.jpg" alt="MarineGEO circle logo" style="height: 400px; width:600px;"/><br />
  Fig.1: Gate level Full adder design <br />
</p>

Various designs are available in literature that design full adders using fewer gates to save power and area. One such design is a 10T full adder that uses 10 CMOS. Fig.2 shows the design.

<p align="center">
<img src="https://github.com/Santosh3672/CMOS-design-of-a-low-power-8-8-hybrid-Dadda-Vedic-multiplier-on-28nm-technology/blob/main/10T_FA_schematics.png" alt="MarineGEO circle logo" style="height: 600px; width:800px;"/><br />
  Fig.2: 10T Full adder schematics <br />
</p>

This type of design requires no VSS or VDD supply; hence it consumes less power but has a problem of output voltage swing (output voltage level less than VDD for logic 1 and more than VSS for logic 0), as shown in Fig.2   For this reason, we cant use this design for a cascaded system like a multiplier.
<p align="center">
<img src="https://github.com/Santosh3672/CMOS-design-of-a-low-power-8-8-hybrid-Dadda-Vedic-multiplier-on-28nm-technology/blob/main/10T_FA_wave%20form.jpg" alt="MarineGEO circle logo" style="height: 600px; width:800px;"/><br />
  Fig.3: 10T Full adder waveform <br />
</p>


So in our design, we are using an energy-efficient [[2](#Reference)] full adder design that doesn’t have the problem of output voltage. This design uses 28 MOSFETs, of which we are connecting 8 MOSFETs to VDD or VSS, so it consumes low power. From the truth table of full adder boolean value of sum is EXOR(A,B) when Cin is ‘0’ and EXNOR(A,B) when Cin is ‘1’ and the boolean value of Cout is A*B when Cin is ‘0’ and A+B when Cin is ‘1’. So in the first stage, we have an inverter with VDD and VSS. In the next stage, we have Exor, Exnor, AND, and OR gates designed with fewer gates and fewer gates connected to VDD and VDD, followed by the final stage is, where we place a mux with Cin as the select line.
<p align="center">
<img src="https://github.com/Santosh3672/CMOS-design-of-a-low-power-8-8-hybrid-Dadda-Vedic-multiplier-on-28nm-technology/blob/main/LP_FA_design.png" alt="MarineGEO circle logo" style="height: 700px; width: 700px;"/><br />
  Fig.4: 28T low power full adder design <br />
</p>


Fig.5 shows the schematic of the design in Synopsys Custom Compiler. While designing, we have assumed μn = 2*μp and to have an un-skewed design, we have taken selected W/L ratio such that βn =  βp. 
<p align="center">
<img src="https://github.com/Santosh3672/CMOS-design-of-a-low-power-8-8-hybrid-Dadda-Vedic-multiplier-on-28nm-technology/blob/main/LP_FA_schematics.jpg" alt="MarineGEO circle logo" style="height: 700px; width: 700px;"/><br />
  Fig.5: Schematics of 28T energy efficient full adder<br />
</p>

To test the circuit, we have built a test bench (Fig.6) where we provide all possible digital inputs to the circuit through a pulse signal. Fig.7 shows the input-output waveform. We can observe that the problem of output voltage swing is not present. 
<p align="center">
<img src="https://github.com/Santosh3672/CMOS-design-of-a-low-power-8-8-hybrid-Dadda-Vedic-multiplier-on-28nm-technology/blob/main/LP_FA_tb.png" alt="MarineGEO circle logo" style="height: 700px; width: 700px;"/><br />
  Fig.6: Testbench used to simulate 28T energy efficient full adder<br />
</p>
<p align="center">
<img src="https://github.com/Santosh3672/CMOS-design-of-a-low-power-8-8-hybrid-Dadda-Vedic-multiplier-on-28nm-technology/blob/main/LP_FA_wave%20form.png" alt="MarineGEO circle logo" style="height: 700px; width: 700px;"/><br />
  Fig.7: Waveform of 28T energy efficient full adder<br />
</p>

## Low power half adder
We have designed a half adder in the same approach as the energy-efficient full adder. Since we don’t have Cin input, MOSFETs related to Cin including the mux are not used hereRest of the design remain the same. Fig.8 shows the schematics of half adder, and Fig.9 shows the waveform.
<p align="center">
<img src="https://github.com/Santosh3672/CMOS-design-of-a-low-power-8-8-hybrid-Dadda-Vedic-multiplier-on-28nm-technology/blob/main/LP_HA_schematics.jpg" alt="MarineGEO circle logo" style="height: 700px; width: 700px;"/><br />
  Fig.8: Schematics of energy efficient half adder<br />
</p>

<p align="center">
<img src="https://github.com/Santosh3672/CMOS-design-of-a-low-power-8-8-hybrid-Dadda-Vedic-multiplier-on-28nm-technology/blob/main/LP_HA_waveform.png" alt="MarineGEO circle logo" style="height: 700px; width: 700px;"/><br />
  Fig.9: Waveform of energy efficient half adder<br />
</p>

## Design of 4x4 Dadda Multiplier
We can create a multiplier now that we have an optimized full adder and half adder. In our design, we are using a Dadda multiplier. The reason for choosing this multiplier was that it focuses on reducing the number of full adder and half adders used in the design compared to a Wallace tree multiplier that tries to reduce each stage. Though the number of reduction stages in both the multiplier is the same, the Dadda multiplier had slightly lower delay due to fewer gates used. 

We have illustrated the working of a 4×4 Dadda multiplier in Fig.10. In this method, we generate partial products using AND gates. Then unlike the Wallace tree multiplier in the Dadda multiplier, the partial products are arranged as an inverted triangle to use fewer full and half adders.
<p align="center">
<img src="https://github.com/Santosh3672/CMOS-design-of-a-low-power-8-8-hybrid-Dadda-Vedic-multiplier-on-28nm-technology/blob/main/4x4_dadda_multiplier.jpg" alt="MarineGEO circle logo" style="height: 500px; width: 900px;"/><br />
  Fig.10: Design architecture of 4x4 Dadda multiplier<br />
</p>

Fig.11 shows the schematics of the 4x4 multiplier in Synopsys custom compiler. 
<p align="center">
<img src="https://github.com/Santosh3672/CMOS-design-of-a-low-power-8-8-hybrid-Dadda-Vedic-multiplier-on-28nm-technology/blob/main/4x4_schematics.png" alt="MarineGEO circle logo" style="height: 500px; width: 900px;"/><br />
  Fig.11: Schematics of 4x4 Dadda multiplier<br />
</p>
The waveform of input and output waveform are shown in fig. We can observe that the problem of output voltage swing is not seen here.
<p float="left">
  <img src="https://github.com/Santosh3672/CMOS-design-of-a-low-power-8-8-hybrid-Dadda-Vedic-multiplier-on-28nm-technology/blob/main/4x4_wave_full.jpg" width="500" />
  <img src="https://github.com/Santosh3672/CMOS-design-of-a-low-power-8-8-hybrid-Dadda-Vedic-multiplier-on-28nm-technology/blob/main/4x4_wave_half.png" width="500" /> 
 <h2 align="center"><br /> Fig.12: Waveform of 4x4 Dadda multiplier<br />
  </h2>
</p>

## Reference
 - [1]. Dadda, Luigi (May 1965). "Some schemes for parallel multipliers". Alta Frequenza. 34 (5): 349–356.
 - [2]. C.S. Wallace, A suggestion for a fast multiplier, IEEE Trans. Computers, Vol. 13, pp. 14-17, Feb. 1964.
 - [3]. Mariano Aguirre-Hernandez and Monico Linares-Aranda, “CMOS full adder for energy efficient arithmetic applications” IEEE Transactions on VERY LARGE SCALE INTEGRATION (VLSI) Systems, vol. 19, no. 4, april 2011.
