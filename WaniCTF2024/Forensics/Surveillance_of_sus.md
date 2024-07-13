## Surveillance_of_sus

![ảnh](https://github.com/LDV-SpaceK/WaniCTF2024/assets/151914246/6dd13f5a-8f69-4de3-82a2-8224d3dc320b)

## Extract file

* file: Cache_chal.bin

## Tools

[bmc-tools.py](https://github.com/ANSSI-FR/bmc-tools/blob/c66a6575209fd6501fe99fc8689468d2400366c5/bmc-tools.py)

## Solution

* First of all, I check this file hex

![ảnh](https://github.com/LDV-SpaceK/WaniCTF2024/assets/151914246/b066a412-523e-45ab-9fe8-de257c506217)

* this is RDP8bmp file, RDP8bmp is a file format used in the context of Microsoft's Remote Desktop Protocol (RDP), specifically from version 8.0 onwards. It stands for "Remote Desktop Protocol version 8 Bitmap". This format is primarily used to store bitmap images that are part of the RDP session, such as cached screen images, to optimize the performance of remote desktop connections.
* I searched and found this bmc-tools, after using it, a lot of bmp was extracted into my dir

![ảnh](https://github.com/LDV-SpaceK/WaniCTF2024/assets/151914246/bfb05eb9-3157-4b70-a635-64f8cc9c6829)

`FLAG{RDP_is_useful_yipeee}`


