---
title: Fault Injector
date: "2019-08-31"
description: Development of a robust SITL UAV testing environment.
image: https://github.com/deliastephens/FaultInjector/blob/master/res/FaultInjector.PNG?raw=true
---
## Project Overview

Testing UAVs in the field can be costly: not only must you charge batteries, go through checklists, prepare the drone, transport people and materials to the testing site, and return everything to its place, there is the chance that the changes you have made will fail. Software-in-the-loop ([SITL](http://ardupilot.org/dev/docs/sitl-simulator-software-in-the-loop.html)) simulation eliminates the need for physical tests but maintains the integrity of the testing environment by linking a flight dynamics model such as [JSBSim](http://jsbsim.sourceforge.net/) to the autopilot, enabling rapid development and testing of UAV software.

<!-- ![Final Product](https://github.com/deliastephens/FaultInjector/blob/master/res/FaultInjector.PNG?raw=true) -->

<img align="right" src="https://github.com/deliastephens/FaultInjector/blob/master/res/FaultInjector.PNG?raw=true" width="50%">



However, current SITL solutions do not allow for the rapid testing of multiple missions in succession. Additionally, simulations are typically run in the ideal environment, assuming perfect connections to the UAV and all its equipment.
Developing further on the deprecated work by [Jayson Boubin](http://jaysonboubin.com/), I modified the [UAV FaultInjector](https://github.com/boubinjg/FaultInjector) to load, modify, and reset MissionPlanner Waypoint files, run multiple missions, and perform robust UAV testing in concert with open-source flight dynamics simulators.

[Here](https://github.com/deliastephens/FaultInjector) is my code for the FaultInjector, [here](https://gist.github.com/deliastephens/6eb3fb3111f5d854bb240c7649847c1f) is a more detailed description of how to get SITL running, and [here](https://gist.github.com/deliastephens/fb2cfeb348b4ac89e1acd20d751836a9) are the personal notes I kept while developing this project. Enjoy!

## Setting up SITL

My first task was connecting the SITL physics simulator to a flight simulator for effective mission visualization. Because much of the documentation was outdated, I have written my own guide, available [here](https://gist.github.com/deliastephens/6eb3fb3111f5d854bb240c7649847c1f).

I eventually ended up with a FlightGear visualization connected to my instance of JSBSim. It received missions through MAVProxy and MissionPlanner. With this implementation, you can create missions, run them in real-life locations, and see if the autopilot fails given certain conditions.

{{< gallery match="images/*"loadJQuery=true sortOrder="desc" rowHeight="150" margins="5" thumbnailResizeOptions="600x600 q90 Lanczos" showExif=true previewType="blur" embedPreview=true >}}


## Fault Injection

Once I had SITL running on my computer, I decided to take the existing FaultInjector script and modify it to be able to:
- Load missions from a .txt file
- Run a SITL simulation
- Reset drone position after a completed mission
- Run multiple missions in succession
- Interface with existing Ground Control systems

[![Final Product](https://github.com/deliastephens/FaultInjector/blob/master/res/FaultInjector.PNG?raw=true)](https://github.com/deliastephens/FaultInjector)

A build log is available [here](https://gist.github.com/deliastephens/fb2cfeb348b4ac89e1acd20d751836a9), but I was ultimately able to update the FaultInjector to reflect changes in Python and ArduPilot development, add the functionality to load missions, start and stop SITL instances, and run multiple missions in succession. With this tool, rapid development and testing of autopilots is made simple and practical.

For a more detailed user guide, please go to [the FaultInjector Github page](https://github.com/deliastephens/FaultInjector).
