# A Tutorial on Using ESP with Lab801 Server

This tutorial provides a step-by-step instruction on how to launch the ESP GUI for SoC configurations with our lab server. 

## ESP From Columbia

> **ESP (Embedded Scalable Paltforms)** is an open-source research platform for heterogeneous system-on-chip design that combines a scalable tile-based architecture and a flexible system-level design methodology.

<div align="center">
<img src="https://i.ibb.co/pjx2mLm/esp-overview.png" alt="esp-overview" border="0">
</div>

In other words, it is a platform that integrates the full design flow of chip development. It provides 3 design flows, including RTL (Chisel, SystemVerilog, VHDL), HLS (High Level Synthesis) with C/C++ or SystemC, and Machine learning frameworks (Keras TensorFLow, Pytorch). You can choose whichever more is more suitable to your scenario.

To prototype your design, ESP also provides a SoC integration flow which automatically generates a tile-based NoC (Network-on-Chip) configured by the desiner. It comes with a GUI which guides designers to configure their own SoC with the choices of CPU, accelerator, memory and auxiliary tiles.

In the end, once your designs are ready, you can use ESP to do either a **Full-system simulation** with each supported FPGA board or real **FPGA prototyping** with supported boards. In the case of FPGA protyping, the generation of the bitstream file, the programming script and the deployment of software are fully automated.

> Full-system RTL simulation is accurate, but it is practical only for the simulation of short programs. Instead,
FPGA prototyping enables the execution of real applications on top of an operating system, while reproducing the complex interactions among all SoC components.

Fore more information, please refer to the official [ESP website](https://www.esp.cs.columbia.edu/ "ESP website") as well as the [overview paper on ESP](https://arxiv.org/pdf/2009.01178.pdf "overview paper on ESP").

In their latest paper "[Accelerator Integration for Open-Source SoC Design](https://sld.cs.columbia.edu/pubs/giri_ieeemicro21.pdf "Accelerator Integration for Open-Source SoC Design")," FPGA prototypes of various SoC designs, featuring the NVIDIA Deep Learning Accelerator and the Ariane RISC-V 64-bit processor core are demonstrated.
