# Rocket Motor Test System
RMTS is a complete set of test stand electronics in a single device for amateur motor builders. It was designed to be a simple and safe way to ignite solid rocket motors and collect data from their firing to enable hobbyists to make informed decisions as they iterate on their propellant formulas and motor designs. It is similar in complexity to a standard rocketry altimeter and doesn't require any special skills to use. It is a standalone unit meaning you don't need to leave a computer near the motor. As it is specialized for rocketry, it displays thrust and pressure curves immediately after the firing without needing to pass the data through a spreadsheet. The built in wireless ignition channel reduces the number of devices you need to set up to one and allows you to measure the motor's startup transient as logging begins when the igniter fires.
## Components
The system consists of a transmitter, receiver, and an application that is run on the user's computer. The transmitter is the larger of the two circuit boards included in the system and has terminal blocks around the edge for connecting transducers and the igniter. The receiver is the smaller board and has two connectors, one USB port for connecting to the user's computer and an RP-SMA jack for the antenna. The software can be downloaded from [here](https://github.com/reilleya/RMTS-Software/releases).
## Using RMTS
Before using RMTS for the first time you will need to calibrate it. More information about what that entails it found [here](reilley.net).
To assemble and use the system for a series of static fires, follow [this](reilley.net) guide.
## Connection Diagram
Coming Soon
## Setup
Coming Soon
## Calibration
Coming Soon
## LED Explanations
(diagram)

The main RMTS board has four LEDs to indicate system status. The first is the `Power` indicator, which turns on as soon as the board is connected to a 5V supply. Next to it is the `Status` light, which has a number of blink patterns to show which state the board is currently in. Next is the `Continuity` LED, which indicates that the system has detected continuity throught the igniter circuit, including both the pyro battery and the igniter itself. Finally, the `Firing` indicator shows if the igniter port has a voltage across it. Never connect the igniter while this light is on. If it is on unexpectedly, your RMTS has been damaged.

#### Status LED Blink Patterns
| Pattern                  | Explanation                                                                                                                                 |
|--------------------------|---------------------------------------------------------------------------------------------------------------------------------------------|
| Two Fast Blinks          | System is in `setup` state. It is for a firing or calibration.                                                                              |
| Constant, Rapid Blinking | System is in `error` state. Connect to it with the radio for more details.                                                                  |
| Off                      | System is in `fire` state. Stop it in the application to view results.                                                                      |
| Slow Blinking            | System is in `results` state. The results can be viewed in the application. It can be safely powered off as the results are on the SD card. |

## Trigger Mode
This input enables the use of an external ignition system. Set up the program as if you were going to fire using the board. Instead of connecting the igniter to the ignition port, simply connect the igniter in parallel with the trigger port on the board. The board will automatically begin recording as soon as it detects a large voltage spike. This trigger port is opto-isolated, so there is no risk of accidental ignition. It also will not trigger from a continuity check. As soon as the motor is done firing, go through the usual procedure to end the test (i.e. press the stop button).
## Troubleshooting
Coming Soon
