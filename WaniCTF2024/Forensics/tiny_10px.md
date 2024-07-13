## tiny_10px

![ảnh](https://github.com/LDV-SpaceK/WaniCTF2024/assets/151914246/641d8644-afba-42c8-b21a-73ef0ba98ccb)

## Resize image

* file: chal_tiny_10px.jpg

## Overview

* this picture is a complete picture but was fix the size to smaller

## Solution

* first, open the picture

![chal_tiny_10px](https://github.com/LDV-SpaceK/WaniCTF2024/assets/151914246/5d5b2341-a184-40cc-b7e2-3f1718d49793)

* it is just a small piece of full picture
* this is the jpg file size hex structure

![ảnh](https://github.com/LDV-SpaceK/WaniCTF2024/assets/151914246/e4e36f43-3347-475a-9b63-604e0740bb13)

![ảnh](https://github.com/LDV-SpaceK/WaniCTF2024/assets/151914246/cb217cfe-0801-4048-b2ae-8e1adb70dc6e)

* original: `FF C0 00 11 08 00 0A 00 0A`
* modified: `FF C0 00 11 08 00 9A 00 9A`

![ảnh](https://github.com/LDV-SpaceK/WaniCTF2024/assets/151914246/59c94bc8-0511-41ee-91ce-a75fd3e4e55a)

`FLAG{b1g_en0ugh}`




