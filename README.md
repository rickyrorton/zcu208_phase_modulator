# Digital Implementation of Linear PLL for PM Demodulation
FPGA based digital implementation of linear PLL for PM demodulation.

## How does it work?
While a linear PLL is a completely analog circuit with an analog four quadrant multiplier, active/passive loop filter and a 
voltage-controlled oscillator (VCO), this projectaims to implement a faithful digital counterpart using FPGA resources like 
multipliers, FIR/IIR filters and Direct Digital Synthesizers (DDS Compilers).

A Phase-locked loop consists of three main blocks-Phase detector,loop filter and a VCO.

<img width="701" height="361" alt="image" src="https://github.com/user-attachments/assets/ae109a5c-55c6-467c-9d03-c43cfdadc2cc" />

The phase detector compares the incoming signal with the locally generated reference signal and generates a phase error. 
This phase error is then fed into the loop filter to suppress any high frequency components. The filtered signal is then 
fed into the VCO, closing the feedback loop and allowing the system to track the input signal’s phase continuously.

## How was it implemented?
This design was implemented on Xilinx's Ultrascale+ RFSoC ZCU208 evaluation platform using Xilinx Vivado 2020.2 and Vitis 2020.2. 
The design utilises Xilinx's IP Cores for the phase detector (multiplier) and DDS compiler to generate the local reference signal. 
The design also uses a IIR filter written in verilog as the loop filter. The loop filter used in the design is a discrete time 
implementation of a first order RC low pass filter obtained through bilinear transform.

<img width="723" height="163" alt="image" src="https://github.com/user-attachments/assets/43fba916-c029-4ee7-8c3b-643bc0d0657c" />

The transfer function of the IIR filter obtained after bilinear transformation of the RC filter is as follows,

<img width="421" height="155" alt="image" src="https://github.com/user-attachments/assets/0b49abca-f7a8-4382-9d11-c93b845d0a8b" />

The architecture of the digitally implemented VCO is shown below.

<img width="839" height="205" alt="image" src="https://github.com/user-attachments/assets/a93f9889-e8ae-42fb-bb3c-b1e5381a353b" />

The PM modulator was implemented using a DDS compiler with the phase offset configuration set to streaming

## Block diagram
<img width="903" height="296" alt="image" src="https://github.com/user-attachments/assets/bbc23299-a46e-4ddc-9215-de5b3a49de70" />

Note: To account for the multiplier’s inherent low pass characteristic in an actual LPLL, a FIR filter is used.
