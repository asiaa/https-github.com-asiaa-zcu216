# zcu216
# Xilinx ZCU216 board development
# 100G Ethernet:
  100MHz reference clock is provided by pl_clk0 from the ZYNQ Ultrascale+ block. Fixed 33.333MHz clock provided by Si5341 on the board is the input clock to the ZYNQ Ultrascale+ block. Open the Block design in Vivido; Double click on the "ZYNQ ..." block ; Clock on the "Clock Configuration"; "output Clocks" -> "Low Power Domain Clocks" -> "PL Fabric Clocks"; there is PL0 which is specified at 100MHz. So the 100MHz reference clock to 100G Ethernet core is quite stable, can be affected by the modelling.
# Setup the Mellanox switch:

Mellanox SN2100 switch: 
* Use the RJ45+rs232 converter cable, connect to the console port. For SN2100, locate at rigtht top.

user: admin

password:admin

* Adjust the MTU size. Default is 1500, that is too small for our application.
* Incoming and outgoing ports all have to be adjusted.
* Connector at Mellanox side has to be Mellanox specified. Other brand's doesn't work. 
[standalone: master] > enable

[standalone: master] # configure terminal

[standalone: master] (config) # interface ethernet 1/1 shutdown

[standalone: master] (config interface ethernet 1/1) # mtu 9216

[standalone: master] (config interface ethernet 1/1) # exit

[standalone: master] (config) # no interface ethernet 1/1 shutdown

* save the change.  

[standalone: master] (config) # configuration write 

# Setup the Mellanox NIC:
* NIC = Mellanox MCX416A-CCAT ConnectX®-4 EN network interface card,100GbE dual-port QSFP28,PCIe 3.0 x 16
* Use the RJ45+rs232 converter cable, connect to the console port. For SN2100, locate at rigtht top.
* Mellanox switch user manual :  https://docs.nvidia.com/networking/display/Onyxv393220
* Prior to the test, the MTU of 100G NIC has to be expanded to more than the size from ZCU216. I set it to 9660. The max. is 9999. The command is :
Root > ifconfig 'name_of_100G_port' mtu 9660

For example of our case:

Root > ifconfig enp23s0f1 mtu 9660


Issue the 'ifconfig' again to make sure the mtu has been changed. If the mtu size is smaller than the packets sent, all packets will be lost, and nothing you can get on the PC.

# Cable/Connector:
* Copper and optical fiber cables were tested. At Mellanox switch or NIC side, Mellanox specified connector is a must, other brands do not work. At ZCu216 side, looks like all brands are fine. "Mellanox", "Generic" and a local brand "Jumbo-Sum" has been tested, they are all fine.
* Mellanox copper cable, 3M long,MCP-7F00, 25Gx4 to 100G break out cable, passed tests.

![Screenshot _100G_2022-04-01](https://user-images.githubusercontent.com/1265867/161182153-183260b4-ffd6-4664-853a-4bf05c5d055d.png)

# Misc
[HiSpeedDigital _8A34001.pdf](https://git[HiSpeedDigital_100G.pdf](https://github.com/asiaa/zcu216/files/8494253/HiSpeedDigital_100G.pdf)

hub.com/asiaa/zcu216/files/8494252/HiSpeedDigital._8A34001.pdf)

[HiSpeedDigital_GetTheCasperfpgaUnderVirtualEnvironment.pdf](https://github.com/asiaa/zcu216/files/8494254/HiSpeedDigital_GetTheCasperfpgaUnderVirtualEnvironment.pdf)

[HiSpeedDigital_GetTheLibrary.pdf](https://github.com/asiaa/zcu216/files/8494255/HiSpeedDigital_GetTheLibrary.pdf)

[HiSpeedDigital_Modifications.pdf](https://github.com/asiaa/zcu216/files/8494257/HiSpeedDigital_Modifications.pdf)

[HiSpeedDigital_SDBooting.pdf](https://github.com/asiaa/zcu216/files/8494258/HiSpeedDigital_SDBooting.pdf)

[HiSpeedDigital_Ubuntu.pdf](https://github.com/asiaa/zcu216/files/8494259/HiSpeedDigital_Ubuntu.pdf)

[HiSpeedDigital_VirtualPythonLocalExample.pdf](https://github[HiSpeedDigital_ZCU216Misc.pdf](https://github.com/asiaa/zcu216/files/8494261/HiSpeedDigital_ZCU216Misc.pdf)
.com/asiaa/zcu[HiSpeedDigitalClocks.pdf]

(https://github.com/asiaa/zcu216/files/8494263/HiSpeedDigitalClocks.pdf)
216/files/8494260/HiSpeedDigital_VirtualPythonLocalExample.pdf)

[HominWiki_MainHomePage.pdf](https://github.com/asiaa/zcu216/files/8494264/HominWiki_MainHomePage.pdf)

