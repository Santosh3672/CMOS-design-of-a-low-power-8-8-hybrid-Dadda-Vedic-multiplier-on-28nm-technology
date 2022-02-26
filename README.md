# CMOS design of a low power 8×8 hybrid Dadda Vedic multiplier on 28nm technology
This repository presents the CMOS design of a low power 8×8 hybrid Dadda-Vedic multiplier on 28nm technology using Synopsys Custom compiler

## Table of content 
 * [Abstract](#Abstract)


## Abstract
 Multiplication is a commonly used arithmetic operation; hence a multiplier is used in most digital systems like ALU of Microprocessor,  DSP applications such as image processing, and arithmetic related operation. A multiplier is a significant design that primarily uses full adders and half adders that consume a large portion of the area and power of the design. In this report, we have designed an 8×8 Dadda-Vedic tree multiplier with the advantage of the Dadda multiplier[1] by utilizing less full adder and half adder than conventional Wallace tree design[2] and also uses the advantage of the scalability of a Vedic multiplier. We have also presented an energy-efficient full adder[2] and a half adder that we are using in our design. We have used Synopsys custom compiler tool for the design using 28nm technology libraries.

## Design Detail:
## Low power full Adder:
Conventional full adder designed using gates fig1 converted into CMOS level design are not optimized designs. As per the diagram below, a full adder requires 2 XOR gates(12 CMOS each), 2 AND gates(6 CMOS each) and 1 OR gate(6 CMOS each), so a complete full adder design has 36 CMOS. 
<img src="https://github.com/Santosh3672/CMOS-design-of-a-low-power-8-8-hybrid-Dadda-Vedic-multiplier-on-28nm-technology/blob/main/FA_GATES.png" alt="MarineGEO circle logo" style="height: 600px; width:600px;"/>


Various designs are available in literature that design full adders using fewer gates to save power and area. One such design is a 10T full adder that uses 10 CMOS.Fig shows the design.

This type of design requires no VSS or VDD supply; hence it consumes less power but has a problem of output voltage swing (output voltage level less than VDD for logic 1 and more than VSS for logic 0), as shown in fig.   For this reason, we cant use this design for a cascaded system like a multiplier.

So in our design, we are using an energy-efficient [main paper 2] full adder design that doesn’t have the problem of output voltage. This design uses 28 MOSFETs, of which we are connecting 8 MOSFETs to VDD or VSS, so it consumes low power. From the truth table of full adder boolean value of sum is A⊕ B when Cin is ‘0’ and A⊕ B when Cin is ‘0’ and the boolean value of Cout is A*B when Cin is ‘0’ and A+B when Cin is ‘1’. So in the first stage, we have an inverter with VDD and VSS. In the next stage, we have Exor, Exnor, AND, and OR gates designed with fewer gates and fewer gates connected to VDD and VDD, followed by the final stage is, where we place a mux with Cin as the select line.

Fig shows the schematic of the design in Synopsys Custom Compiler. While designing, we have assumed μn = 2*μp and to have an un-skewed design, we have taken selected W/L ratio such that βn =  βp. 

To test the circuit, we have built a test bench (fig) where we provide all possible digital inputs to the circuit through a pulse signal. Fig shows the input-output waveform. We can observe that the problem of output voltage swing is not present. 

## Reference
 - [1]. Dadda, Luigi (May 1965). "Some schemes for parallel multipliers". Alta Frequenza. 34 (5): 349–356.
 - [2]. C.S. Wallace, A suggestion for a fast multiplier, IEEE Trans. Computers, Vol. 13, pp. 14-17, Feb. 1964.
 - [3]. Mariano Aguirre-Hernandez and Monico Linares-Aranda, “CMOS full adder for energy efficient arithmetic applications” IEEE Transactions on VERY LARGE SCALE INTEGRATION (VLSI) Systems, vol. 19, no. 4, april 2011.
