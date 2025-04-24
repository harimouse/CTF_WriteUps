# You See What You See
This is an easy one. As you CAN SEE below what was given was an image file showning the poster advertising the Internal APU CTF Competition to all APU students.

![Checkthisout](https://github.com/user-attachments/assets/a02cc3fd-4544-4e37-ab27-4b4883fcade3)


Firstly, there was nothing unusual about the image itself -- it must have to do something with the metadata or LSB

So, I proceeded with my usual commands exiftool, file and binwalk etc.

Commands file and binwalk just showed me that the image was just a normal PNG file.

However, the exiftool showed me something interesting:

![Screenshot 2025-04-24 095911](https://github.com/user-attachments/assets/79acb5f7-e9d3-4096-b2e7-9b404dc14c68)

There are three things that looked interesting:

1. The attribution URL 

![Screenshot 2025-04-24 100321](https://github.com/user-attachments/assets/6b4a41c4-3e60-4f93-adfd-a7fb5ae675b7)

2. The license and,

![image](https://github.com/user-attachments/assets/a67e7545-0736-4e7a-84c1-b4c6e0262c6e)

3. The keyword

![image](https://github.com/user-attachments/assets/f3daa058-17ef-4de4-898a-f738a691276b)

Now when I clicked the link it just brought me to a rickroll so that's out of the question
(Just got rick rolled in the big 2025)

Now the keyword is clearly text that has been encrypted using base64. However if I tried to decode that onn its own, it just clearly just showed one half of the flag:

RzAxbkchfQ== becomes G01nG!}

Thus, I combined the keyword and the license together to form a much longer ciphertext:
SUNURjI1e0szM3BfRzAxbkchfQ==
and BOOM I have tha flag:
flag{RED4CT3D}
