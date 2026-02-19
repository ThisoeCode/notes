# Thisoe's STM32 Course Note

_[<< Back to Thisoe's Note](./README.md)_

- Course from [OJ Tube](https://www.youtube.com/playlist?list=PLz--ENLG_8TNjRg1OtyFBvUyV4PHaKwmu OJ Tube - 임베디드 실시간 강의) (lang: KR)

*******

# Menu

- 1 ~ 5\. Intro, History & Basics

- [6. Install `STM32 Cube IDE`](#ep6-install-stm32-cube-ide)

- [7. Hello! GPIO!](#ep7-hello-gpio)
> Create New STM32 Project



*******



# [EP.6](https://youtu.be/zFVamoAcE-8) Install STM32 Cube IDE

Get software at https://www.st.com/en/development-tools/stm32cubeide.html

After installing, **DO NOT CHECK ANY `Remember my choice` POPUP!** Or at least check as few as possible.



*******



# [EP.7](https://youtu.be/YZJ6RfhuGd0) `Hello! GPIO!`

## Create new stm32 project
Say we are gonna code an STM32F103C8T6

1. Open STM32CubeIDE

2. `File` > `New` > `STM32 Project`

> It starts downloading  and opens up a Target Selector

3. In `MCU/MPU Selector`, simply check `Core` > `Arm Cortex-M3`

> OR at `Series` check `STM32F1`, and in the `MCUs/MPUs List` scroll down to `STM32F103...` series and find `...C8`. <br>
> We can see its "Package" is `LQFP48`, which means how the chip and its pins look like.
> > The `48` means number of pins. There's also `LQFP100` with a hundred pins.
> `LQFP48` has 64 kB flash mem and 20 kB RAM.

Then click `Next >`

4. Set basic config:

Name the Project;<br>
Lang: C;<br>
Bin Type: Executable;<br>
Proj. Type: STM32Cube

5. "Open Aassociated Perspective?" > `Yes`

After a while it will finish creating, and show you the "Pinout & Config" of the chip.


## Link the Chip to PC, Upgrade Firmware, Code in `while(1)`, Run!
1. Link the chip to your PC with ST-Link wire.
  - If connected, the (newly bought) chip's LED light will be blinking.

2. Get ST-Link Connection software
  1. Download at https://www.st.com/en/development-tools/stsw-link004.html
  2. Unzip and set up the `STM32 ST-LINK Utility`

3. Upgrade firmware
  - Open ST-Link software
  - Try to connect by navigating into `Target` > `Connect`
  - If failed, physically reconnect the USB;<br>
    if still failing, upgrade firmware:<br>
    `ST-LINK` > `Firmware Update` > `Device Connect` (reconnect USB if failed) > `Yes`
 - "Upgrade is successful."

4. `HAL_Init`

  - In Cube IDE, we get into `/Core/Src/main.c` and find `HAL_Init();` (around line 72)<br>
    Add a breakpoint at that line.

  - Run debug (click on the "bug" icon in the top menu) and see.
    1. This starts the compiling and pops up an `Edit Configuration`, just click `Ok`.
    2. Another popup asking whether to update the firmware might appear: <br>
      Uncheck "Always check for update" then click `No`.
    3. Another `Ok` for "Save and launch" popup.

  - A stop without errors or warnings is expected.

5. Pin setting
  There's a line `SystemClock_Config();` (around line 79).
  If we add another breakpoint and run debug, after some retries we will hit timeout.<br>
  **This is because we need to add the clock pins.**

  1. Folder Explorer: open the `*****.ioc` file at root.

  2. In `Pinout & Config.` tab: `System Core` > `SYS`<br>
    `Debug` dropdown: `Serial Wire`. You will see 2 pins turned green.<br>
    `Timebase Source` dropdown: `SysTick`.

  3. `Ctrl + S` Save.

6. Run the main loop!
  - Go back to `main.c`
  - Find `USER CODE BEGIN WHILE` (around line 93 ~ 97)
  - In side the while block, add a line `HAL_Delay(1000);`
  - Add a breakpoint at this delaying line
  - Run debug.

  It should get stuck at the line successfully.



*******



# [Ep.15](https://youtu.be/LmwycZ393r4) Struct