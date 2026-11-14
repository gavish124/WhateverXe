# Alder Lake Surface Optimized WhateverXe fork notes

This fork contains the official WhateverXe 0.8.2 code + three commits:

1. Two eDP hand-off commits by Thatisjigen (from pr/edp-handoff-0.7.0, cherry-picked).
2. Ignore TRANS_DDI_FUNC_CTL2 bit 3 in the eDP boot checks: the Surface Pro 9 firmware leaves 0x60404 = 0x8, which made the boot preflight reject the panel.

## Tested on

| Device model | Hardware | Software |
| --- | --- | --- |
| Surface Pro 9 | i7-1265U, iGPU 46a8 revision 000c, 2880x1920 eDP | macOS 26.7.1, OpenCore 1.0.8, WhateverXe Graphics 0.4.4 pkg |


## Expected result

Preflight passes, Metal 2, 1536 MB VRAM.

## Not tested yet

Other machines, other macOS versions, whether the two eDP commits are still needed on 0.8.2 (plain 0.8.2 plus only the CTL2 change was not tried).

> [!CAUTION]  
> At the moment, 120 Hz is not working as intended. By default, macOS sets the display's refresh rate to 60 Hz, and switching to 120 Hz while booted will work fine. But, the display will fail to properly initialize in the 120 Hz mode. If you want to use 120 Hz, you will need to set your refresh rate to 60 Hz everytime you boot, and then change the refresh rate to 120 Hz once fully booted. If you have forgotten to change the refresh rate back to 60 Hz, you will need to boot without acceleration using the `-wex-no-accel` boot-arg (120 Hz display initialization seems to work fine in the framebuffer patched non-accelerated state).

## Enable and customize the behavior of the backlight smoother to improve your experience

This backlight smoother implementation is modelled after the implementation found in [acidanthera's WhateverGreen kext](https://github.com/acidanthera/WhateverGreen). You can use the instructions from the WhateverGreen [FAQ.IntelHD.en.md](https://github.com/acidanthera/WhateverGreen/blob/master/Manual/FAQ.IntelHD.en.md#customize-the-behavior-of-the-backlight-smoother-to-improve-your-experience), but keep in mind that the boot-arg for enabling the backlight smoother is `-wex-bls`.
