# PX4-Micro-Quad
A PX4 compliant Micro Quadrotor designed for autonomous MAV research.

(This repo is no longer under development)

1/04/2016 (Not an April foools joke -_-):

The new design has been made with Altium Designer and is found in the "Rev2.7z" folder.

I have redesigned the format of the 4x Brushed DC motor ESC/PDB/BEC. The board now matches the form size for the PX4 PixRacer and has been designed to work as it's brushed ESC. With CAN bus compatability, the board's STM32F103 could also serve a purpose as a co-processor for the F407 on the PixRacer.

The noisy boost converter has been dropped as it's effect on the sensors was too significant. The board now requres a 7.4v source from a 2s lipo battery. The test motors are still 3.7v, but may run at 7.4v for short peroids before becoming overheated. If suitable 7.4v micro motors (6mm-12mm) could be found, they would be an excellent replacement for the current 3.7v.

6/03/2016:

I've just finished my schematics for my first (1/2 or 1/3, depending on circumstances) PCB. It's a combined PDB, brushed ESC, and BEC. I've tried to stick as close to the standard PX4 hardware as possible.

The ESC portion includes a STM32F10XCXT6 in LQFP48 package which connects to the UAVCAN bus via a CAN Transceiver (MAX3051), takes the regular ESC control packets, converts it to a 20KHz PWM to drive the N-Channel power MOSFETs which in turn, drive the motors.

The PDB and BEC portion include a 3.7v -> 5v lipo booster converter (TPS61200) which is powered by the battery. This 5v rail will be the primary rail for all 5v required applications (IO, FMU, IMU). There is also a 3.3v LDO, dual output regulator (MIC5332) which will power IO with one rail and IC with the other.

Programming of the STM32 will be done with the use of pogo-pins, as the pads on the PCB are low profile and light (two essential qualities of micro-quad avionics).

I am still working on these designs and any feedback (or the pointing out of obvious flaws) is greatly appreciated.

P.S. The data sheet ( http://www.farnell.com/datasheets/1952113.pdf ) says that programming to System Memory is done through USART1 however it also suggests that JTAG/SWD programming is possible. Ideally, as I'm familiar with JTAG, I'd like to opt for the pogo-pins programming method.
