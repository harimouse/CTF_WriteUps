# Hidden in Plain Graphic 

The title "Hidden in Plain Graphic" is a clever twist on the phrase "hidden in plain sight," suggesting that the flag is likely concealed within an image. Since the challenge provides a pcap file, I considered and googled multiple ways an image could be hidden in network traffic throughout this challenge.

## **Initial Approach: Checking for Suspicious Packets via Abnormal Ports**

I started by filtering for abnormal ports to identify any unusual activity. I used the following Wireshark filter to exclude common ports:

!(tcp.port == 80 || tcp.port == 443 || udp.port == 53)

These ports correspond to:
- 80: HTTP
- 443: HTTPS
- 53: DNS

![hipg1](https://github.com/user-attachments/assets/3f590ca7-1cf4-4d69-a96d-2c2224e099ec)

This filter reduced the packet count from 5,003 to 1,570 packets. However, I wasn’t particularly confident in this approach. The total number of packets—5,003—struck me as weird. Why not a round number like 5,000? This detail was annoying me, but I pressed on.

I hit Fn+End to zip to the last packet and poke around. In the "Info" column, I spot a ton of stuff hitting port 27015—and it's labelled "Source Engine Query." That’s just common for people playing Source Engine games like CS:GO or Half-Life. I bet the challenge creator’s a Counter-Strike grinder, haha. 

![hipg2](https://github.com/user-attachments/assets/41116cd9-20ec-43e6-a6c1-4ead498b6658)

![hipg3](https://github.com/user-attachments/assets/9e6306c6-6803-48a5-8e18-c709b1481798)

I determined that this approach was a dead end.

## **Pivot: Investigating Packet Lengths**

I scrapped the idea of chasing abnormal ports and returned to the peculiar packet count of 5,003. Thinking the flag might be in a large file transfer, I sorted the packets by length to identify outliers. 
Using Fn+Home and Fn+End, I confirmed that packet 562 had an unusually large length compared to others.

![hipg4](https://github.com/user-attachments/assets/b0519b43-d47c-4190-9adf-e7e2bdf88a8b)

Following the TCP stream for packet 562 isolated three packets, which felt significant given the odd total of 5,003 packets. I was convinced this wasn’t a coincidence—no one designs a pcap challenge with such a specific number by accident. I tried exporting objects (e.g., HTTP, DICOM) to see if a PNG file was embedded, but none of the options yielded results.

Digging deeper, I revisited packet 562 and examined the reassembled contents in ASCII. After some research, I learned you can display the TCP stream in "raw" format and save it as a file. I saved the raw data as a file named hi.

In the terminal, I ran:
file hi
IT WAS A PNG FILE!!!!

![hipg5](https://github.com/user-attachments/assets/283ae4cd-d6fc-4ade-934b-9889ee23de99)

I renamed the file to hi.png and opened it. The image itself was unremarkable, but I wasn’t done yet.

![hipg6](https://github.com/user-attachments/assets/974a2ad0-87ba-4b54-b893-e6ab5ed2f90f)

![hipg7](https://github.com/user-attachments/assets/1198f4b2-beca-49b9-847f-c43876e4e608)

Image Analysis
To ensure I hadn’t missed anything, I throw every tool I’ve got at it:

1. **Binwalk**: I checked for embedded files or archives within hi.png. Nothing was found.

![hipg8](https://github.com/user-attachments/assets/29285f14-386b-4e4e-85b5-c7026ee18103)

2. **Exiftool**: I examined the metadata for hidden clues, such as comments or author details. No luck there either.

![hipg9](https://github.com/user-attachments/assets/1bc296c4-1a5f-4b94-8c2b-50833bcf8f89)

3. **Zsteg**: Finally, I used zsteg to check for data hidden in the image’s least significant bits (LSB). Bingo! The flag was embedded there.

![hipg10](https://github.com/user-attachments/assets/8fccf539-aabc-4e2f-8075-a51485d493d7)

HUZZAHHH!!! The flag is: flag{RED4CT3D}
