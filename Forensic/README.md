# Forensic
- ## Decoding Keystrokes from USB
Python script: [key_press](/Forensic/key_press.py)

Yes, with Wireshark you can intercept also USB packets send, for example, by a keyboard to the computer.  
So, you have the pcap file, with some "URB_INTERRUPT in" packets from the source keyboard.  
the interesting part is the field called "Leftover Capture Data" or "usb.capdata".  
An useful command to exfiltrate these values is:
```
tshark -r usb_intercept.pcapng -T fileds -e usb.capdata
```
The first byte in each line is a modifyer, which can tell if Shift, Alt, or Ctrl are held while typing the key.  
#### For example:  
0x02 --> Left Shift key  
0x0000210000000000 --> 4  
0x02002f0000000000 --> {


- ## Read ADS on Windows' NTFS
Alternate Data Streams (ADS) are a file attribute, only found on the NTFS file system, to store different streams of data, in addition to the default stream which is normally used for a file. When this feature was created, its main purpose was to provide support to the macOS Hierarchical File System (HFS).
#### Useful commands:
```
echo Hello, I'm an Alternate Data Stream > text.txt:invisible.txt
notepad text.txt:invisible.txt
Get-Item .\text.txt -Stream *
Get-Content .\text.txt -Stream:invisible.txt
```
