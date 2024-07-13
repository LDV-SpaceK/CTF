## Image

![ảnh](https://github.com/LDV-SpaceK/Junior.Crypt.2024-CTF/assets/151914246/6645b0d0-be13-434d-99e0-08e8194cf5cd)

## Image forensics

* file:

![ảnh](https://github.com/LDV-SpaceK/Junior.Crypt.2024-CTF/assets/151914246/dcb4a4db-7210-4bd4-9655-4d9906527748)

## Tool 

* binwalk

## Overview

* key was hidden in Image, but which one?

## Solution

* first, I view all file type of these images

`file *`

![ảnh](https://github.com/LDV-SpaceK/Junior.Crypt.2024-CTF/assets/151914246/ca12afa1-41cb-422e-b4ec-f43298e786bf)

* there was a suspectious file `Thumb.db`, there was not a sqlite file

![ảnh](https://github.com/LDV-SpaceK/Junior.Crypt.2024-CTF/assets/151914246/057c56db-0cf7-47c0-9b37-4a68f1d7f058)

* FPX(FlashPix) file is a raster image file format designed for storing high-resolution digital images
* however, that image still can't be opened
* I use binwalk to figure out, is there any file contained inside

![ảnh](https://github.com/LDV-SpaceK/Junior.Crypt.2024-CTF/assets/151914246/39f131fe-e4be-4596-a640-8f9ea39f4f2d)

* there are several image file inside, extract all
* all the png file are the same to kandinsky-download... png given
* the one different is the jpg image

![ảnh](https://github.com/LDV-SpaceK/Junior.Crypt.2024-CTF/assets/151914246/a5f38c56-09b6-4412-ba40-420c0f4f0754)

`grodno{image_in_thumbnail}`

