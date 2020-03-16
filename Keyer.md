# SEMI-AUTOMATIC "BUG" key - From the ground up

Keyer
 
## Required Components
 
### Resistors
 
| Value               | Quantity | Comment            |
| ------------------- | -------- | ------------------ |
| 1K                  | 3        |                    |
| 10K                 | 1        |                    |
| Linear Variable 10K | 1        | PCB mountable type |

### Capacitors
 
| Value               | Quantity | Comment                   |
| ------------------- | -------- | ------------------------- |
| 0.01uF              | 3        |                           |
| 100uF               | 1        | Electrolytic, radial lead |

### Semiconductors
 
| Part                | Quantity | Comment            |
| ------------------- | -------- | ------------------ |
| 2N2222              | 2        |                    |

### Miscellaneous

The URL links provided are not to be seen as any form of promotion, simply as guidance as to what the exact component is.
 
| Part                                 | Quantity | Comment            |
| ------------------------------------ | -------- | ------------------ |
| 6x6mm Tactile Switch                 | 1        | Similar to <https://www.bitsbox.co.uk/index.php?main_page=product_info&cPath=116_117_119&products_id=3263> |                   |
| Miniature PCB slide switch           | 1        | Similar to <https://www.bitsbox.co.uk/index.php?main_page=product_info&cPath=116_120_124_125&products_id=870> |
| Miniature Electromagnetic Transducer | 1        | Similar to <https://www.bitsbox.co.uk/index.php?main_page=product_info&cPath=302_309&products_id=2098> |
| 2-Way PCB Terminal Blocks            | 3        | Similar to <https://www.bitsbox.co.uk/index.php?main_page=product_info&cPath=225_232&products_id=2962> |
| 3-Way PCB Terminal Blocks            | 1        | Similar <https://www.bitsbox.co.uk/index.php?main_page=product_info&cPath=225_232&products_id=1712> | 
| 12-Way SingleRow Socket              | 2        | Optional, the Arduino can be soldered to the board. <https://www.bitsbox.co.uk/index.php?main_page=product_info&cPath=225_230&products_id=1643> |
| Arduino Pro Micro                    | 1        | Similar to <https://www.ebay.co.uk/itm/1-2-5-10PCS-Leonardo-Pro-Micro-ATmega32U4-16MHz-5V-ATmega328-Arduino-Pro-Mini/152216277704?ssPageName=STRK%3AMEBIDX%3AIT&var=451406319074&_trksid=p2057872.m2749.l2649> |
| PCB                                  | 1        | Optional, the keyer can easily be built on Veroboard or similar. |

## Installing the Build Software

Start by installing the Arduino IDE. This can be found at:

https://www.arduino.cc/en/Main/Software

For the purpose of this build the Windows version Arduino 1.8.8 was used. 
All default installation options were accepted.

## Compiling the source code

- This project is based on the K3NG open source keyer and the code can be found here <https://github.com/k3ng/k3ng_cw_keyer>.
At the top right of this page you will see a green button that reads "Clone or download". Click on the small downward arrow and select "Download ZIP". 
Unzip the contents into a folder of your choice.
- To support the chosen hardware a few code changes need to be made. The table below details the file changes. 
It includes the filename, the old code and new code. Sadly line numbers are of little use as the K3NG project is evolving.

### Required Code Changes

The following two changes involve removing the "//" comment lead characters to enable the command button and speed potentiometer.
 
| File                         | Old Code                           | New Code                        |
| ---------------------------- | ---------------------------------- | ------------------------------- |
| keyer_features_and_options.h | // #define FEATURE_COMMAND_BUTTONS | #define FEATURE_COMMAND_BUTTONS |
| keyer_features_and_options.h | // #define FEATURE_POTENTIOMETER   | #define FEATURE_POTENTIOMETER   |

The following two changes involve changing the trailing 0 to 1 to have the speed potentiometer continually honoured.
 
| File             | Old Code                           | New Code                          |
| ---------------- | ---------------------------------- | --------------------------------- |
| keyer_settings.h | #define potentiometer_always_on 0  | #define potentiometer_always_on 1 |

### Optional Code Changes

The following changes are optional. If you feel confident using the paddle, or simply up for a challenge, 
then these options can be changed by using the command button and the correct command as documented in the 
keyer wiki pages. If not so confident then it is probably worth doing the following:

The following change controls the startup keyer mode. It changes it from IAMBIC mode to BUG mode.

| File           | Old Code                             | New Code                        |
| -------------- | ------------------------------------ | ------------------------------- |
| k3ng_keyer.ino | configuration.keyer_mode = IAMBIC_B; | configuration.keyer_mode = BUG; |

The following three changes control the startup keyer speed and the upper and lower bounds of the speed
potentiometer.

| File             | Old Code                              | New Code                              |
| ---------------- | ------------------------------------- | ------------------------------------- |
| keyer_settings.h | #define initial_speed_wpm 26          | #define initial_speed_wpm 16          |
| keyer_settings.h | #define initial_pot_wpm_low_value 13  | #define initial_pot_wpm_low_value 8   |
| keyer_settings.h | #define initial_pot_wpm_high_value 35 | #define initial_pot_wpm_high_value 20 |

- Open the Arduino IDE and then open the k3ng_keyer.ino project file
- Navigate to Tools > Boards and select "Arduino Leonardo". Some of the Arduino Pro Micro devices seem to be identifying themselves as "LilyPad Arduino USB" devices. If
the one you have claims to be one of these then under Tools > Boards select the "LilyPad Arduino USB" device 
and not "Arduino Leonardo".
- Click the "Verify" button (Round circle with a tick mark in it - top left), if successful you will see something like 
"Sketch uses 14522 bytes (50%) of program storage space. Maximum is 28672 bytes.
Global variables use 741 bytes (28%) of dynamic memory, leaving 1819 bytes for local variables. Maximum is 2560 bytes."
though the number may not be exact.
- Make sure that the Arduino is plugged into your PC. Navigate to Tools > Port and make sure that the correct port is selected. See USB Issues below.
- Click the "Upload" button (Right pointing arrow - top left) to up load the software.
- The device should now be programmed correctly.

## PCB Revisions

- V1.? - Legend changes.
- V1.0 - March 13th, 2020 - Initial board design.
