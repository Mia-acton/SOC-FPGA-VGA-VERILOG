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
I decided to create a simple Pac-Man-style visual for my FPGA VGA Driver project. Going into this, I assumed it would be relatively straightforward to configure the VGA logic and draw a few basic shapes on screen - but I quickly discovered that even simple graphics can become challenging when built at the hardware-description level.

To build confidence, I first created a few small practice visuals, including the French and Jamaican flags, as shown below. These early tests helped me establish a foundation in drawing pixel regions, using row/column counters, and controlling RGB signals. Once I felt comfortable with this workflow, I moved on to developing my actual Pac-Man scene. 

My final design consists of four main components:
  - A yellow Pac-Man character
  - Three ghosts (red, white, and cyan)
  - A blue maze-like grid structure
  - Beige pac-dots scattered throughout the maze

I intentionally built each part in stages I began with Pac-Man on a blank screen to confirm that my coordinate system and circle-drawing logic were correct. Next, I added two ghosts to verify spatial alignment and ensure that the characters appeared consistently across frames. Once I introduced the maze structure, the complexity increased significantly - particularly with object alignment and priority ordering, since Pac-Man must always appear on top of the background elements. 

Despite the unexpected challenges, working through these problems game me a much deeper understanding of VGA timing, pixel-based rendering, and hardware-driven graphics. The iterative process of refining each component ultimately shaped the final version of my project. 

### **Code Adaptation**
I decided to use the Stripes template code as the foundation for my project, modifying it so that instead of solid colour bands, it would draw pixel-based shapes for my Pac-Man scene. To do this, I reorganised the template into clearly defined sections and assigned priority levels to each graphic element. This allowed lower-priority objects (like the maze walls) to be drawn first, while higher-priority objects (such as Pac-Man and the ghosts) were drawn afterward so they would appear on top. 

The first modification I made was replacing the original stripe-generation logic with my own conditional checks for specific pixel regions. I began with the lowest-priority component - the maze grid - and created it by defining rectangular regions line by line using row and column comparisons. Once the walls rendered correctly, I added additional sections for the pac-dots, ghosts, and finally Pac-Man. This step-by-step restructuring demonstrated how the original template could be adapted from simple coloured stripes into a layered, fully customised VGA image. 

### **Simulation**
To test my VGA design, I simulated the project using Vivado's built-in simulator, which allowed me to examine how the timing signals and RBG outputs behaved over time. In the waveform, key signals such as clk, hsync, vsync, and the row/col counters can be seen updating as the pixel clock advances. Watching these counters increment and reset confimred that the VGA timing generator was working correctly - particularly the transition through the active video region and the blanking intervals. I also monitored the red, green, and blue outputs to verify that colour values were being assigned only when the row and column matched the coordinate ranges of Pac-Man, the ghosts, or the maze walls. 

One important observation from simulation is that Vivado does not display the actual picture - instead, it shows signal changes. For example, in my screenshot, I can see the RGB values momentarily swicthing to non-zero values whenever the counters pass through areas where my code draws a specific object. This helped me confirm that my priority logic was correct and that higher-priority objects (like Pac-Man) were drawn after background elements. By reviewing these transitions, I was able to catch small alignment and timing issues before synthesising the design onto hardware.  

### **Synthesis**
Describe the synthesis & implementation outputs for your design, are there any differences to that of the original design? Guideline 1-2 short paragraphs.

### **Demonstration**
While my final design may not have been perfect, I did learn a lot from this project. 

### **References**
At least 3
