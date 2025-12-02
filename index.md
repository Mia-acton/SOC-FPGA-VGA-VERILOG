---
layout: home
title: FPGA VGA Driver Project
tags: fpga vga verilog
categories: demo
---

Welcome to my FPGA VGA Driver Project, where I bring classic Pac-Man characters to life using pure hardware logic. Explore how an FPGA generates real-time VGA graphics from scratch! 
## **Template VGA Design**
### **Project Set-Up**
Summarise the project set-up and design flow. Include a screenshot of your own set-up, for example see the image of my Project Summary window below. Guideline 1 short paragraph.

![Image](setup.png)

### **Template Code**
The template Verilog modules provided by my lecturer - ColourCycle and ColourStripes - introduce the basic structure for generating RGB signals on an FPGA using VGA timing. Both templates are designed to work alongside a VGA controller that outputs the current pixel's row and column coordinates, as well as the horizontal and vertical sync pulses. VGA works by scanning each pixel of the screen one row at a time, so your Verilog design must produce a correct RGB value for every (row, col) position during the active video period. 

The ColourStripes module uses simple combinational logic to assign different RGB values depending on the horizontal pixel position. By dividing the screen into eight vertical regions, it displays solid coloured stripes. This teaches coordinate-based pixel generation and demonstrates how the VGA controller "paints" the image left to right, top to bottom. 

The ColourCycle module instead uses a finite state machine (FSM) that cycles through eight preset colours. A counter determines how long each colour remains on screen before the state transitions. This illustrates sequential logic, state-based colour control, and the use of timing counters. 

### **Simulation**
Simulation is used to verify that the VGA modules behave correctly before programming the FPGA. By running a testbench that drives the clock, reset, and (for the stripes module) row/col coordinates, you can observe the RGB outputs and confirm the logic changes at the correct times. The Vivado Simulator allows you to inspect state transitions, counters, and colour outputs in detail. 

This step makes it easy to catch logic errors early - for example, incorrect colour ranges or FSM transitions. Once the simulated output matches the expected behaviour (e.g., correct colour sequencing or stripe boundaries), the design is ready for synthesis.

Insert waveform simulation in class. 

### **Synthesis**
Synthesis converts your Verilog code into FPGA hardware logic, mapping it into LUTs, registers, block RAM, and routing resources. The Vivado tool produces a synthesis report that shows resource usage and identifies any timing issues. After synthesis, the implementation step places and routes the logic onto the FPGA fabric and generates the bitstream used to program the board.

Examining the synthesis/implementation reports ensures the design meets timing at the VGA pixel clock frequency (typically 25.175 MHz for 640x480 at 60Hz). This confirms your design can reliably generate video signals in real time. 

Insert synthesis summary.

### **Demonstration**
The final design was loaded onto the FPGA and successfully displayed the generated graphics on a VGA monitor. Below are photographs of the working demos showing the output on screen.

![Image 1](IMG_5756.jpg)
![Image 2](IMG_5761.jpg)

## **My VGA Design Edit**
Introduce your own design idea. Consider how complex/achievabble this might be or otherwise. Reference any research you do online (use hyperlinks).

I decided to create a simple Pac-Man design for my FPGA VGA Driver Project. Going into this project, I thought it would be relatively straight-forward to configure my design accordingly - but I was sorely mistaken. I researched a number of different ideas before finally deciding on Pac-Man, I even went as far as to design and build some basic level applications on VGA including the french and jamaican flags (as seen below). I did this in order to establish a comfort level in my knowlege to this style of code, and when I decided I was happy with the output - I moved on to coding my actual project. My design consisted of a yellow Pac-Man character, three ghosts (red, white and cyan), a blue maze-like grid, and beige pac-dots. I went through various different stages in building my project, starting with a simple visual of Pac-Man on his own. I thought it was important to ensure I understood the layout of my grid before I started hard coding my final design, so I started at a foundation level. Creating the Pac-Man character itself was relatively easy at first, and I soon integrated two ghosts to figure out my alignment. Once I added in the maze-like structure things started to get a bit more complicated as I was having some alignment issues and trouble figuring out prioriy levels. 

### **Code Adaptation**
Briefly show how you changed the template code to display a different image. Demonstrate your understanding. Guideline: 1-2 short paragraphs.

I decided to use the Stripes template code to design my project. I split my VGAStripes file into different sections in order to tackle the code block by block. I started with the lowest priority image, i.e. the maze walls. I coded each wall line by line  
### **Simulation**
Show how you simulated your own design. Are there any things to note? Demonstrate your understanding. Add a screenshot. Guideline: 1-2 short paragraphs.
### **Synthesis**
Describe the synthesis & implementation outputs for your design, are there any differences to that of the original design? Guideline 1-2 short paragraphs.
### **Demonstration**
While my final design may not have been perfect, I did learn a lot from this project. 

### **References**
At least 3
