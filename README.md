# USB_Labview_Example

 It demonstrate how to use Labview's VISA driver and our device protocol, **without .NET class nor ActiveX**, to set up and acquire data then display the waveform in a chart. It applies to DI-1100, DI-1110, DI-1120, DI-2108, DI-2008, DI-4108, DI-4208, DI-4718B, and DI-4730 USB. **It supports both 32 and 64-bit LabView**

**Prerequisites**:

1) Firmware 1.35 or higher is recommended https://github.com/dataq-instruments/Firmware_Upgrade. Earlier version of firmware may not work properly at higher sample rate

2) Understand the protocol, please refer to  https://www.dataq.com/resources/pdfs/misc/Dataq-Instruments-Protocol.pdf
 
3) Turn 21xx/11xx/41xx/47xx into CDC mode (Program Mode): plug the device to USB port, if the LED already blinks Yellow, stop, you are already in CDC mode. If not, once the LED turns blinking Green, push and hold the button immediately (within 5 second time frame), the LED should turn white, hold until LED turns Red, then release the button, now the LED will blink yellow to indicate CDC mode. If you need to exit CDC mode back to LibUSB mode (Windaq mode), repeate the same action and a green blinking LED will indicate LibUSB mode.

  
**Run it**:

 1) Use Windows Device Manager to find out the COM port for your device and enter it to COM Port text box <br/><br/>
![alt text](https://www.dataq.com/resources/repository/matlab_devicemanager.png)

 2) Two sample vis are available
    - rawcdc_protocol.vi is for single channel
    - rawcdc_protocol_2ch.vi is for two channels, it demonstrate how to reshape the array to plot two channels
 
 3) Load a sample vi above, you can exam the block diagram (the following is from rawcdc_protocol.vi):<br/>
 ![alt text](https://www.dataq.com/resources/repository/lvrawcdc_ch1.png)

 4) Bring Front Panel into focus and click Run to start it<br/>
![alt text](https://www.dataq.com/resources/repository/lvrawcdc2.gif "ScreenCapture by LICECap")  

 5) To debug, please read the protocol to learn more, and exam the error codes


**Note**:

- LabView's VISA driver keeps data from previous session if the port is not closed properly, so please press Stop button to close the port before exiting the program

- When configuring the serial, disable termination char feature so that ALL binary data can go through

- After each command is sent, a read to serial port will clear the echo. To simplify the demo, we didn't bother to verify the echo to ensure each command is constructed and processed properly.

- The last undocumented command "nop" will do nothing and will not generate echo from the device, it just adds extra time to flush the input buffer before the start command

- The default serial data format in LabView is big endian, and the one from device is little endian 

- Before converting byte data stream to int16 data stream, always retrieve even number bytes from the input buffer

- When accquiring multiple channels, besides adding extra member to the scanlist, one also needs to always retrieve data in terms of scans and reshape the array before charting (the following block applies to 2 channel configuration) <br/>
![alt text](https://www.dataq.com/resources/repository/lvrawcdc_ch1.png "block for two channel configuration") 

 
**Extra**:

  - A good tool to understand/debug the protocol communication is the network protocol analyzer WireShark https://www.wireshark.org/

