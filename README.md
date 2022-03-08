# zcu216
# Xilinx ZCU216 board development
# 100G Ethernet:
  100MHz reference clock is provided by pl_clk0 from the ZYNQ Ultrascale+ block. Fixed 33.333MHz clock provided by Si5341 on the board is the input clock to the ZYNQ Ultrascale+ block. Open the Block design in Vivido; Double click on th4 "ZYNQ ..." block ; Clock on the "Clock Configuration"; "output Clocks" -> "Low Power Domain Clocks" -> "PL Fabric Clocks"; there is PL0 which is specified at 100MHz. So the 100MHz reference clock to 100G Ethernet core is quite stable, can be affected by the modelling.
