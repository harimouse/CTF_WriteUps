RED
-	Image file downloaded
-	Use binwalk
-	It is a PNG file, no zip file
-	Use exiftool, finds a poem
-	Crimson heart, vibrant and bold,.
Hearts flutter at your sight..
Evenings glow softly red,.
Cherries burst with sweet life..
Kisses linger with your warmth..
Love deep as merlot..
Scarlet leaves falling softly,.
Bold in every stroke.
-	First letter of the sentences spell out CHECKLSB
-	Since it has to do with least significant bit of the image, I will use zsteg
-	zsteg gives me:
cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==
-	It is obviously base64 
-	So I decoded it using dcode and found the flag
-	flag{red4ct3d}
