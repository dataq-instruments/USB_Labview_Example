# USB_Labview_Example

 It demonstrate how to use Labview's driver and protocol (**without .NET class nor ActiveX**) to set up and acquire data then display in a chart. It applies to DI-1100, DI-1110, DI-1120, DI-2108, DI-2008, DI-4108, DI-4208, DI-4718B, and DI-4730 USB. It supports both 32 and 64-bit of LabView

**Prerequisites**:

1) Firmware 1.35 or higher is recommended https://github.com/dataq-instruments/Firmware_Upgrade. Earlier version of firmware may not work properly at higher sample rate

2) Understand the protocol, please refer to  https://www.dataq.com/resources/pdfs/misc/Dataq-Instruments-Protocol.pdf
 
3) Turn 21xx/11xx/41xx/47xx into CDC mode: plug the device to USB port, if the LED already blinks Yellow, stop, you are already in CDC mode. If not, once the LED turns blinking Green, push and hold the button immediately (within 5 second time frame), the LED should turn white, hold until LED turns Red, then release the button, now the LED will blink yellow to indicate CDC mode. If you need to exit CDC mode, repeate the same action and a green blinking LED will indicate LibUSB mode.

  
**Run it**:

 1) Use Windows Device Manager to find out the COM port for your device and enter it to COM Port text box <br/><br/>
![alt text](https://www.dataq.com/resources/repository/matlab_devicemanager.png)

 2) Load the sample vi above, you can exam the block diagram:<br/>
 ![alt text](https://www.dataq.com/resources/repository/lvrawcdc1.png)

 3) Bring Front Panel into focus and click Run to start it<br/>
![alt text](https://www.dataq.com/resources/repository/lvrawcdc2.gif "ScreenCapture by LICECap")  

 4) To debug, please read the protocol to learn more, and exam the error codes


**Note**:

- LabView's VISA driver keeps data from previous session, so please press Stop button to close the port when exiting the program

 
**Extra**:

  - A good tool to understand/debug the protocol communication is the network protocol analyzer WireShark https://www.wireshark.org/

