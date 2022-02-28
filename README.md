# CMOS design of a low power 8×8 hybrid Dadda Vedic multiplier on 28nm technology
This repository presents the CMOS design of a low power 8×8 hybrid Dadda-Vedic multiplier on 28nm technology using Synopsys Custom compiler

## Table of content 
 * [Abstract](#Abstract)
 * [Design Detail](#Design-Detail)
 * [Low power full Adder](#Low-power-full-Adder)
 * [Low power half adder](#Low-power-half-adder)
 * [Design of 4x4 Dadda multiplier](#Design-of-4x4-Dadda-Multiplier)
 * [Design of 8x8 Dadda-Vedic multiplier](#Design-of-8x8-Dadda-Vedic-multiplier)
 * [DC analysis](#DC-analysis)
 * [Reference](#Rererence)
 * [Acknowledgements](#Acknowledgements)


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


In our design, we are using an energy-efficient [[2](#Reference)] full adder design that doesn’t have the problem of output voltage. This design uses 28 MOSFETs, of which we are connecting 8 MOSFETs to VDD or VSS. In [[2](#Reference)] the design was compared with different available full adder designs and results have shown a saving of upto 80% power, which is relatedto powerless and groundless configuration of some gates.
From the truth table of full adder boolean value of sum is EXOR(A,B) when Cin is ‘0’ and EXNOR(A,B) when Cin is ‘1’ and the boolean value of Cout is A*B when Cin is ‘0’ and A+B when Cin is ‘1’. So in the first stage, we have an inverter with VDD and VSS. In the next stage, we have Exor, Exnor, AND, and OR gates designed with fewer gates and fewer gates connected to VDD and VDD, followed by the final stage is, where we place a mux with Cin as the select line.
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
We can create a multiplier now that we have an optimized full adder and half adder. In our design, we are using a Dadda multiplier. Dadda multiplier is same as Wallace tree multiplier but Dadda multiplier is quite faster than Wallace tree multiplier as it requires fewer gates than the Wallace multiplier thus it leads to fewer power consumption.  
A Wallace multiplier tries to do as much reduction as possible but a Dadda multiplier tries to do as few reductions as possible. Though the number of reduction stages in both the multiplier is the same, the Dadda multiplier had slightly lower delay due to fewer gates used. 

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
<p align="center">
  <img src="https://github.com/Santosh3672/CMOS-design-of-a-low-power-8-8-hybrid-Dadda-Vedic-multiplier-on-28nm-technology/blob/main/4x4_wave_full.jpg" width="500" />
  <img src="https://github.com/Santosh3672/CMOS-design-of-a-low-power-8-8-hybrid-Dadda-Vedic-multiplier-on-28nm-technology/blob/main/4x4_wave_half.png" width="500" /> 
<br /> Fig.12: Waveform of 4x4 Dadda multiplier<br />
</p>

## Design of 8x8 Dadda-Vedic multiplier
To design an 8×8 multiplier, we have used the existing 4x4 Dadda multiplier and arranged them like a Vedic multiplier where small multipliers are used in cascade to create a big multiplier. However, we have arranged the products of the 4×4 multiplier as an inverted triangle like the Dadda multiplier. We have illustrated the whole architecture of design in Fig.13.

<p align="center">
<img src="https://github.com/Santosh3672/CMOS-design-of-a-low-power-8-8-hybrid-Dadda-Vedic-multiplier-on-28nm-technology/blob/main/8x8%20mult-dadda_vedic_hybrid.png" alt="MarineGEO circle logo" style="height: 770px; width: 869px;"/><br />
  Fig.13: Schematics of 4x4 Dadda multiplier<br />
</p>
Since there are 16 inputs of the design, it is difficult to change all the design inputs, so for that reason, in our test bench, we have set some inputs as constant by tying them with VDD or VSS and applying pulse signal to other inputs as shown in Fig.14. 

<p align="center">
<img src="https://github.com/Santosh3672/CMOS-design-of-a-low-power-8-8-hybrid-Dadda-Vedic-multiplier-on-28nm-technology/blob/main/8x8_mult_tb.jpg" alt="MarineGEO circle logo" style="height: 500px; width: 900px;"/><br />
  Fig.14: Testbench of 8x8 multiplier<br />
</p>

Fig.15 shows the input and output waveform. 
<p align="center">
<img src="https://github.com/Santosh3672/CMOS-design-of-a-low-power-8-8-hybrid-Dadda-Vedic-multiplier-on-28nm-technology/blob/main/8x8_mult_waveform.png" alt="MarineGEO circle logo" style="height: 500px; width: 900px;"/><br />
  Fig.15: Waveform of 8x8 multiplier<br />
</p>

## DC analysis
To verify the functionality of the design, we have connected the input pins DC supply as shown in Fig.16. So the value of inputs are A =(10110010)binary =(178)decimal, B = (01100010)binary = (98)decimal.
<p align="center">
<img src="https://github.com/Santosh3672/CMOS-design-of-a-low-power-8-8-hybrid-Dadda-Vedic-multiplier-on-28nm-technology/blob/main/8x8_dc_tb.png" alt="MarineGEO circle logo" style="height: 500px; width: 900px;"/><br />
  Fig.16: Test bench for DC analysis of 8x8 multiplier<br />
</p>
The expected output is Y = (17444)decimal = (0100 0100 0010 0100)binary.
The output of the simulator(Fig.17) is also the same as the expected output.
<p align="center">
<img src="https://github.com/Santosh3672/CMOS-design-of-a-low-power-8-8-hybrid-Dadda-Vedic-multiplier-on-28nm-technology/blob/main/8x8_dc_result.png" alt="MarineGEO circle logo" style="height: 500px; width: 900px;"/><br />
  Fig.17: Result of the DC analysis of 8x8 multiplier<br />
</p>

## Reference
  [1]. Dadda, Luigi (May 1965). "Some schemes for parallel multipliers". Alta Frequenza. 34 (5): 349–356. \
  [2]. C.S. Wallace, A suggestion for a fast multiplier, IEEE Trans. Computers, Vol. 13, pp. 14-17, Feb. 1964.\
  [3]. Mariano Aguirre-Hernandez and Monico Linares-Aranda, “CMOS full adder for energy efficient arithmetic applications” IEEE Transactions on VERY LARGE SCALE INTEGRATION (VLSI) Systems, vol. 19, no. 4, april 2011. 

## Acknowledgements

 - [Kunal Ghosh, Co-founder, VSD Corp. Pvt. Ltd.](https://www.iith.ac.in/events/2022/02/15/Cloud-Based-Analog-IC-Design-Hackathon/)
 - [Cloud Based Analog IC Design Hackathon](https://www.iith.ac.in/events/2022/02/15/Cloud-Based-Analog-IC-Design-Hackathon/')
 - [Synopsys India](https://www.synopsys.com/)
 - [Sameer Durgoji, NIT Karnataka](https://www.iith.ac.in/events/2022/02/15/Cloud-Based-Analog-IC-Design-Hackathon/)
 - [Chinmay panda, IIT Hyderabad](https://www.iith.ac.in/events/2022/02/15/Cloud-Based-Analog-IC-Design-Hackathon/)

