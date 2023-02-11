# Design

This document shows how the requirements for the controller were derived.

As always, do some research to see if this has been done before and, if not, can someone else's work make this project work better, easier, faster?

1. Look for similar projects.
2. What controls are needed to control a dog robot.
3. Find out how ROS2 is used to control dog robots.

Having gained some background knowledge about the problem space, the system architecture is then defined and then we can fully define the requirements for the controller.

## Similar projects

### Open Dog

James Bruton's open dog projects are a great starting point for this work.  Over the past couple of years, I have watched most of his YouTube videos so already know about his Arduino based open dog controller and the later [Raspberry Pi version](https://www.youtube.com/watch?v=ATQblGOjMWQ).

#### The open dog remote

GitHub repo has the [Arduino code](https://github.com/XRobots/openDog/blob/master/Part1/code/Remote001/Remote001.ino) and the [CAD model STEP file.](https://github.com/XRobots/openDog/blob/master/Part1/CAD/Remote.stp)

#### Raspberry Pi remote

The remote has the following features:

* 2 x 3 DoF joysticks.
* 3 x buttons.
* 1 x emergency stop button.
* 1 x 7" touchscreen.

The GutHub repo for the code and CAD is <https://github.com/XRobots/ROSremote>.  There is next to no code in this repo and no info on what ROS packages are used but these can be guessed at from the video contents.

## Controls needed to operate a robot dog

TODO

## ROS2 dog robot control

To control a dog robot, the ROS2 messages needed are:

* Twist.  Definitely needed for forward/back and left/right movements.
* TODO Work out how to do things like sit/roll over

### Research

Found presentation from ANYmal presentation at ROSCon 2016.

* <https://roscon.ros.org/2016/presentations/ROSCon%202016%20-%20ANYmal.pdf>
* <https://vimeo.com/187696096>

Other useful stuff:

* <https://github.com/andreasBihlmaier/gazebo2rviz>
* <https://github.com/leggedrobotics> A mine of information.
* <https://answers.ros.org/question/345408/navigation-with-a-quadruped-robot/>
    * <https://github.com/ethz-adrl/towr/tree/ros2> Useful package for defining legged robots.

There is a joypad in RQt!

## System Architecture

The system architecture defined in this section is very specific to controlling Bittle robot to make sure I focus on getting something made.

### Controlling PC

Has Micro-ROS agent to attach to controller.

### Bittle

There are two main ways to use Bittle.

#### Option 1

Can use supplied board only. How to control it?

Pros:

* No extra boards

Cons:

* Cannot control gait.

#### Option 2

Add RPi of some sort.  RPI3A+ seems like the best. £28.30

Pros:

* Can control gait.
* No need for PC.  Just switch on, wait until booted and use controller directly.

Cons:

* Extra board.

Notes:

* <https://docs.petoi.com/api/ros>

#### MU Vision Sensor

Bought this so need to work out how to use it! <https://docs.petoi.com/extensible-modules/mu-camera>

### Controller

#### ESP32

Uses ESP32 as only MCU. ESP32 talks Micro-ROS.

#### RPi

Use 3A+ board plus 5" touch screen.
Ubuntu 64 bit.  Tier 1 support from ROS2 for arm64 arch so just download packages.
Memory is only 512MB so server only.

Bought the following from "The PiHut".

* 5" DSI Capacitive Touch Display for Raspberry Pi (800×480),  £43.20
* Raspberry Pi 3 Model A+ £26.00

Decided that using the RPi was the best way to go.

## Controller requirements

### Must haves

* Portable. Implies...
    * Battery powered.
    * Wi-Fi connected.
* ROS2 compatible.
* MUST be quick to implement, test and use.
* Push buttons.
* Power switch.
* Kill switch?

### Nice to haves

* Should be created in a way that is easy to extend or enhance.
* Should not be too heavy to hold for long periods but can always use strap to take the weight.

## Software

The controller must run ROS2 so a Raspberry Pi is the natural choice.  The RPi does not have enough ADC pins to connect to the joysticks so I have chosen to use an Arduino Nano for this purpose.

### Arduino Nano

Use micro-ROS on the Arduino Nano? No.  Arduino Nano is not powerful enough.

Use JSON comms instead.  Has it's own flavour of JSON so will use that.

### RPi Joystick and buttons interface

Listens to JSON comms from Arduino and outputs ROS2 messages.

Done this a couple of times at work so will use the same approach but implement in Python instead of C++.  Could also use Rust but probably too early for that.

TODO What do the buttons do?

Power switch is just hardware.

#### ROS2 Messages

`/cmd_vel` TwistStamped - This is the only message output by the Teleop Joy package.  The joystick buttons are used as modifiers.

TODO Work out how the 6 axis joysticks map to the `TwistStamped` message.
