# Design

This document shows how the requirements for the controller were derived.

As always, do some research to if this has been done before and, if not, can someone else's work make this project work better.

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

## System Architecture

TODO

## Controller requirements

### Must haves

* Portable. Implies...
    * Battery powered.
    * Wi-Fi connected.
* ROS2 compatible.
* MUST be quick to implement, test and use.

### Nice to haves

* Should be created in a way that is easy to extend or enhance.
