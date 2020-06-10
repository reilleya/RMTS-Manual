# Rocket Motor Test System
RMTS is a complete set of test stand electronics in a single device for amateur motor builders. It was designed to be a simple and safe way to ignite solid rocket motors and collect data from their firing to enable hobbyists to make informed decisions as they iterate on their propellant formulas and motor designs. It is similar in complexity to a standard rocketry altimeter and doesn't require any special skills to use. It is a standalone unit meaning you don't need to leave a computer near the motor. As it is specialized for rocketry, it displays thrust and pressure curves immediately after the firing without needing to pass the data through a spreadsheet. The built in wireless ignition channel reduces the number of devices you need to set up to one and allows you to measure the motor's startup transient as logging begins when the igniter fires.
## Components
The system consists of a transmitter, receiver, and an application that is run on the user's computer. The transmitter is the larger of the two circuit boards included in the system and has terminal blocks around the edge for connecting transducers and the igniter. The receiver is the smaller board and has two connectors, one USB port for connecting to the user's computer and an RP-SMA jack for the antenna. The software can be downloaded from [here](https://github.com/reilleya/RMTS-Software/releases).
## Using RMTS
Before using RMTS for the first time you will need to calibrate it. More information about what that entails it found [here](https://github.com/reilleya/RMTS-Manual#calibration).
To assemble and use the system for a series of static fires, follow [this](https://github.com/reilleya/RMTS-Manual#firing-procedure) guide.
## Connection Diagram
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
## Setup
Coming Soon
## Calibration
RMTS is different from other rocketry electronics you may be familiar with as its sensors are external to the board and can be swapped by the user. This is beneficial as it allows you to use transducers well suited for each motor you fire and may be able to use ones you already have. The downside is that the characteristics of sensors you choose to use cannot be built into the software and have to be deternined by you. The RMTS application includes a workflow to make this process simple, and this guide explains how to use it and what is happening internally.
### What is a transducer?
A transducer is a device that converts a signal from one kind of energy (mechanical, thermal, electrical, etc) to another. The transducers that we are interested in for testing motors are sensors, which convert a property of the physical world into a signal that we can read. The specific sensors that RMTS is designed to read from are [load cells](https://en.wikipedia.org/wiki/Load_cell) and [pressure transducers](https://en.wikipedia.org/wiki/Pressure_sensor), which convert force and pressure, respectively, into electrical signals. For more details on how they do this, consult the articles linked above.
### What is transducer calibration?
The transducers that RMTS is designed to work with output a voltage that corresponds to the force or pressure that is applied to the transducer. There is no single standard that describes what voltage a transducer should output for a given input. Even transducers from a single manufacturer of the same model have slightly different outputs for the same physical input. Fortunately, most transducers produce a simple linear response to their input, as shown in the figure. By applying a few different inputs to the transducer and measuring the outputs, we can find the relation and use it to convert any future voltage readings RMTS makes to the real quantities they correspond to.
### RMTS Calibration Workflow
The RMTS application provides a workflow that collects the data required to perform a transducer calibration.
### Calibration Tips
* Though a two points define a line and are technically all that is needed to perform a calibration, the RMTS software doesn't allow you to save a calibration that has less than three points. This is because each point has some associated measurement error, but the more points you enter, the less impact this noise has.
* It is a good idea to use inputs along a range that goes to as close to the limits of the transducer as possible. For example, a 2000 N load cell could be calibrated with points at 0, 500, 1000, 1500, and 1750 N. The goal is that the system shouldn't have to extrapolate significantly (or at all, ideally) to convert any measurement it makes during real use. Though the transducer should be linear over its range, this is only to an extent and only understanding how it responds in the 0 - 200 N range can lead to error if it is going to be used to measure 1500 N. Even if the transducer is perfectly linear, measurement error on small inputs adds up quickly when extrapolating. If that same 2000 N load cell was only calibrated to 200 N with a single measurement that was 20 N off due to a faulty reference scale or bad technique, it would result in an error of 150 N at 1500 N. If it was instead calibrated with the same error to 1000 N, it would only be 30 N off at 1500 N. More data points in that limited range can help counteract the error, but it is a good idea to use a large range as well.
* Look for sources of error in your calibration method and attempt to correct them. For example, a common procedure for calibrating load cells is to stack objects of known weight on the load cell to produce a variety of inputs. There is nothing wrong with this method in theory, but in practice it can be difficult to balance the items on the load cell, which can lead to them leaning on something other than the load cell. This means that not all of their force is transfered into the load cell, which will lead to your calibration overestimating the force applied during tests. To avoid this, use a beam-type load cell (which is easier to attach masses to), or place your load cell on the reference scale, tare it, and then apply the weights as before. Though they will likely have to lean against something for support, this no longer matters as the same force is being transmitted through the load cell and the scale so it can be measured accurately.
## Firing Procedure
Coming Soon
## Trigger Mode
(Diagram)
This input enables the use of an external ignition system. Set up the program as if you were going to fire using the board. Instead of connecting the igniter to the ignition port, simply connect the igniter in parallel with the trigger port on the board. The board will automatically begin recording as soon as it detects a large voltage spike. This trigger port is opto-isolated and rectified, so there is no risk of accidental ignition and polarity doesn't matter. It also should not trigger from a continuity check, but it is worth testing to be sure. As soon as the motor is done firing, go through the usual procedure to end the test (i.e. press the stop button).
## Troubleshooting
Coming Soon
## Glossary
* Transducer: A device that converts some value from the physical world into a signal. In this context, this usually refers to load cells and pressure sensors.
* ADC: Analog to digital converter. The component on the board that reads from the transducers and outputs a corresponding number.
* Raw Value: A value directly output by the ADC. Corresponds to a voltage read from a transducer.
* Converted Value: A value in real-world units obtained by passing a raw value through a calibration function. 
* Receiver: The smaller device that connects to a user's computer.
* Transmitter: The larger device that the igniter and transducers are connected to.
