# OpenThread [nRF52840](https://mou.sr/3AkvVTz) Firmware Builder.

This fork creates an autostarting thread ftd radio with cli and usb on the nRF52840-Dingle - intended to be a plug-and-play extension for your thread mesh.
 
## How to Flash the Firmware

To flash the USB version (`ot-rcp-USB.hex`), you can use either the **nRF Connect for Desktop** application or the **nrfjprog** command-line tool.
Instructions are for nRF connect method.

1. Download and install [nRF Connect for Desktop](https://www.nordicsemi.com/Products/Development-tools/nRF-Connect-for-desktop) if not already installed.
2. Launch **nRF Connect for Desktop** and open the **Programmer Tool**.
3. Put the nRF52840 dongle into **program mode**:
   - Insert the dongle into a USB port on your computer.
   - Hold down the reset button while inserting the dongle until the LED blinks slowly. Or double press reset button until LED blinks slowly.
   - This indicates the device is in program mode.
4. In the Programmer Tool, select the detected nRF52840 dongle from the device list, it should say DFU Bootloader.
5. Drag the ot-clie-ftd-USB.hex file into the add files section.
6. Click **Write** to flash the firmware onto the dongle.

## Add to Home Assistant OTBR Thread Network.
1. After flashing the nRF52840 hex code, the dongle should now be seen as a new serial port. Check you device manager (or whatever) to confirm the serial port.
2. Use putty (or similar) to connect to the serial port port at 115200,8,1,N and no flow control.
3. You should get a prompt and commands such as help or state or reset should work.  There should be redimentary boot logs displaying.
4. The network connection must be down to make changes to thread paramters: ifconfig down
5. Get the Active TLV from OTBR.  In HA go to Settings -> Thread -> then the information icon in yor preferred network.  Copy the TLV.
6. Back in putty (or whatever): dataset set active <paste your TLV>
7. Commit the dataset: dataset commit active
8. Bring up the network interface: ifconfig up
9. Ensure thread if up (it probably already is): thread start
10. Check the thread device status (within a few seconds it should have joined the thread network): state

Once set up and connected to thread, the nRF52840 can be plugged into a USB power brick (or whatever) and it will join your thread mesh.
If you need to change thread networks or just start all over, enter the command: factoryreset (and go back up to step 2).
To confirm the thread details on the device or general troubleshooting, these commands can come in handy:
state
dataset active -x 
channel
panid
extpanid
networkname
networkkey
thread start/stop
scan
scan energy
ipaddr
ipmaddr
neighbor table
router table
rloc16
eui64


## License

This repository and the OpenThread firmware are licensed under the [BSD 3-Clause License](LICENSE).

## Links

- [OpenThread Documentation](https://openthread.io/)
- [nRF52840 Product Page](https://www.nordicsemi.com/Products/nRF52840)
- [nRF Command Line Tools](https://www.nordicsemi.com/Software-and-Tools/Development-Tools/nRF-Command-Line-Tools)
- [nRF Connect for Desktop](https://www.nordicsemi.com/Products/Development-tools/nRF-Connect-for-desktop)
