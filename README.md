# CarND-Controls-PID

---

## Dependencies

* cmake >= 3.5
* make >= 4.1(mac, linux)
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
* gcc/g++ >= 5.4
  * Mac: same deal as make - [install Xcode command line tools]((https://developer.apple.com/xcode/features/)
  * [uWebSockets](https://github.com/uWebSockets/uWebSockets)
  * Run either `./install-mac.sh`
  * Simulator. You can download these from the [project intro page](https://github.com/udacity/self-driving-car-sim/releases) in the classroom.

## Basic Build Instructions

1. git clone master.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./pid`


## Implementation
The PID implementation is done on the [./src/PID.cpp](https://github.com/asaggi/CarND-PID-Control-Project/blob/master/src/PID.cpp). The [PID::UpdateError](https://github.com/asaggi/CarND-PID-Control-Project/blob/master/src/PID.cpp) method calculates proportional, integral and derivative errors and the [PID::TotalError](https://github.com/asaggi/CarND-PID-Control-Project/blob/master/src/PID.cpp) calculates the total error using the appropriate coefficients.

## Final hyperparameters chosing criteria
The parameters were chosen manually by try and error. First, make sure the car can drive straight with zero as parameters. Then add the proportional and the car start going on following the road but it starts overshooting go out of it. Then add the differential to try to overcome the overshooting. The integral part only moved the car out of the road; so, it stayed as zero. After the car drove the track without going out of it, the parameters increased to minimize the average cross-track error on a single track lap. The final parameters where [P: 1.5, I: 0.0, D: 2.5].

## Output
Screenshots @ Various stages:

![Image1](https://github.com/asaggi/CarND-PID-Control-Project/blob/master/data/SS-I.png)

---
![Image2](https://github.com/asaggi/CarND-PID-Control-Project/blob/master/data/SS-II.png)

---
![Image3](https://github.com/asaggi/CarND-PID-Control-Project/blob/master/data/SS-III.png)

---
![Image4](https://github.com/asaggi/CarND-PID-Control-Project/blob/master/data/SS-IV.png)

## Effect each of the P, I, D components

* The proportional portion of the controller tries to steer the car toward the center line (against the cross-track error). If used along, the car overshoots the central line very easily and go out of the road very quickly.

* The integral portion tries to eliminate a possible bias on the controlled system that could prevent the error to be eliminated. If used along, it makes the car to go in circles. In the case of the simulator, no bias is present.

* The differential portion helps to counteract the proportional trend to overshoot the center line by smoothing the approach to it.  