## Mobile Arcade

The greatest thing nobody ever wanted...

<img src="/Images/LightsAdded.jpg" width="250">


### Table of Contents
- [Concept](#concept)
- [System Design](#systemdesign)
- [Physical Enclosure](#physicalenclosure)
- [Arcade Emulator](#arcadeemulator)
- [mBED Breakout & Drive System](#mbedbreakout&drivesystem)

### Concept

> "To develop a mobile arcade cabinet that can be controlled over Bluetooth to enable ultimate portability and usability, while maintaining retro charm."

The Mobile Arcade was designed to incorporate a retro gaming experience with quarkey mobile chassis. The original idea was centered around a table top arcade experience with additional entertainment features, including vibrent and responsive lighting. In order to better suit and entertain the target audiance (children aged 9 through 14), mobility was incorporated as well. With this in mind, the following design requirements were set:
1. Fully functional, single player, arcade system (ability to play NES and Atari games)
2. Visually pleasing enclosure with a retro feel
3. Interactive lighting
4. Basic Bluetooth-controlled mobility 

### System Design

The design of the mobile arcade was divided into distinct subsystems which were later interfaces. These subsystems included the physical enclosure, the arcade emulator, and the mobility driver. Each of these systems are outlined here.

The following block diagram illustrates all components of the arcade system:
<img src="/Images/BlockDiagram.png" width="350">
* Raspberry Pi: Main processor & arcade game emulator, user interface
* GPIO Interfaces: Joystick, buttons controller
* mBED: Microcontroller in charge of lights, remote control and drive system
* Bluetooth Bridge: Communication between remote control phone and the mBED
* Dual-Channel Motor Driver: Motor driver for running the tank-drive motors
* LED Strips: Decorative lights, ran by the mBED
* Power: Li-Po battery and regulator for all components

### Physical Enclosure

The enclosure was designed using Dassault Systems’ Solid Works. Each portion of the seven component design was fitted together in software before fabrication was attempted. The structure was set as 3/32in clear acrylic sheets.

<img src="/Images/ArcadeCAD.png" width="350">

The overall shape of the enclosure resembles that of a standard arcade cabinet, however there are a few notable exceptions. The design is much simpler than standard cabinets, reducing the number of distinct components that need to be fabricated for the system to fit together. Additionally, the cabinet incorporates mounting holes specifically designed to accommodate drive motors. Two motors can be fixed near the front of the cabinet, while a rounded skid drags at the rear. This produces a "tank drive" configuration which allows the enclosure to maneuver around its environment.

<img src="/Images/ArcadeCabinetPaint.jpg" width="250">
The enclosure after laser cutting and two cotes of dark blue spray paint.

### Arcade Emulator

Raspberry pi stuff here

### mBED Breakout & Drive System

In order to connect the mBED, Bluetooth Bridge, and Dual-Channel motor driver together, a single-layer breakout board was created and fabricated. Side-plugs were soldered to allow the motors and LEDs, as well as an auxiliary power source.

Breakout board design.

<img src="/Images/mBEDBreakoutBoard.png" width="350">

Completed breatout board.

<img src="/Images/mBEDBreakoutBoardDone.jpg" width="350">

The following library was used to control the Dual-Channel motor driver:
[Motor Driver Library](https://os.mbed.com/users/abraha2d/code/Motor/)

[All code for the mBED can be found here.](https://os.mbed.com/users/abraha2d/code/MobileArcade/file/)

### LEDs

[Dotstar LEDs](https://www.adafruit.com/product/2239?length=1) were used to decorate the Arcade, and were chosen due to the relaxed timing requironments, allowing relativaly easy interface with the mBED. A simple library was used and is linked below:

[Custom Dotstar mBED library.](https://os.mbed.com/users/abraha2d/code/APA102/)

Code was written to accept input from the Raspberry Pi to syncronize lighting effects to certain events in the Emulator. For example, on emulation startup, a startup animation is shown on the LEDs. Other effects were added for when games are started and stopped. The Raspberry Pi sends serial commands via USB to the mBED.

### Power System

The arcade is powered from a large lithium-ion battery pack. A 5V, 3A regulator is used to provide power for the Raspberry Pi, mBED system, and the motors. The LCD contains an internal regulator, and is able to plug directly into the battery without further regulation.

The image below contains the battery and regulator plugged into the mBED breakout board.
<img src="/Images/WireHarness.jpg" width="350">

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/1961C/MobileArcade/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
