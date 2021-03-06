# Sensor Fusion Module implementing Extended Kalman Filters for LIDAR/RADAR Input Processing


[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

## Kalman Filters Architecture.

A car equipped with sensors like LIDAR and RADAR on the outside, can detect objects moving around it’s range: for example, the sensors might detect a pedestrian, or even a bicycle. 

<img src="kalman-filter-map.png">

This is achieved by computing an extended kalman filter which combines both data obtained from LIDAR and RADAR simultaniously to measure the moving object’s velocity and relative position to car. For variety, let's step through the Kalman Filter algorithm ( architecture shown in above figure. ) using the bicycle example to understand how this computation really works:

- **First measurement** - the filter will receive initial measurements of the bicycle's position relative to the car. These measurements will come from a radar or lidar sensor.
- **Initialize state and covariance matrices** - the filter will initialize the bicycle's position based on the first measurement.
- then the car will receive another sensor measurement after a time period Δ*t*.
- **Predict** - the algorithm will predict where the bicycle will be after time Δ*t*. One basic way to predict the bicycle location after Δ*t* is to assume the bicycle's velocity is constant; thus the bicycle will have moved velocity Δ*t*. In the extended Kalman filter lesson, we will assume the velocity is constant.
- **Update** - the filter compares the "predicted" location with what the sensor measurement says. The predicted location and the measured location are combined to give an updated location. The Kalman filter will put more weight on either the predicted location or the measured location depending on the uncertainty of each value.
- Based on this belief, the car will then receive another sensor measurement after a time period Δ*t* to make it’s next decisive step. 
- The algorithm then does another **predict** and **update** step which will tell the car about the belief of bicycle’s position relative to vehicle.

In this project we utilize a kalman filter to estimate the state of a moving object of interest with noisy lidar and radar measurements. This module runs the above mentioned algorithm and shows it’s belief output to further track car’s distance from the relative nearby objects. 

## How to run this module.

For this project, the choice of language was C++ as these computations of beliefs need to happen quick, which calls for a more precise control over variable addresses and faster callbacks for calculated matrix multiplications. therefore you will require cmake and make for compilation and building the project.

<img src="simulator.png">

This project also involves an EKF Simulator to be present for testing results, this simulator can be found [in this repository](https://github.com/udacity/self-driving-car-sim/releases).

This repository also includes three shell scripts, `install-mac.sh`, `install-ubuntu.sh`, `install-linux.sh` . This files can be used to automate set up process and install prerequisites like cmake and [uWebSocketIO](https://github.com/uWebSockets/uWebSockets) for either Ubuntu, Linux or Mac systems. For windows you can either use Docker, VMware, or even [Windows 10 Bash on Ubuntu](https://www.howtogeek.com/249966/how-to-install-and-use-the-linux-bash-shell-on-windows-10/) followed by `install-ubuntu.sh` to install uWebSocketIO.

Once the install for uWebSocketIO is complete, the main program can be run by going in the build directory and running  `./ExtendedKF` in your Terminal and then launching the simulator on 1/2 EKF mode.

Here is the main protocol that main.cpp uses for uWebSocketIO in communicating with the simulator.

**INPUT**: values provided by the simulator to the program as inputs.

["sensor_measurement"] => the measurement that the simulator observed (either lidar or radar)

**OUTPUT**: values provided by the program after EKF computation back to the simulator.

["estimate_y"] <= kalman filter estimated position y

["rmse_x"]

["rmse_y"]

["rmse_vx"]

["rmse_vy”]

The final output of this simulation will look something like this [video](output.mov).

## Dependencies

* cmake >= 3.5
 * MAC/Linux/Windows: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: [install Xcode command line tools](https://developer.apple.com/xcode/features/)
  * Windows: Install [MinGW](http://www.mingw.org/) to obtain gcc comiler.

## Basic Build Instructions

1. Clone this repo.
2. Re-make the build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make` 
   * On windows, you may need to run: `cmake .. -G "Unix Makefiles" && make`
4. Run it: `./ExtendedKF path/to/input.txt path/to/output.txt`. You can find
   some sample inputs in 'data/'.
    - eg. `./ExtendedKF ../data/sample-laser-radar-measurement-data-1.txt output.txt`

## Code Style

The follwoing code follows [Google's C++ style guide](https://google.github.io/styleguide/cppguide.html), and has been thouroghly checked for any potential data leaks and C++ 11 syntax formats.

## Generating Additional Data

If you wish to generate another random sample fo LIDAR and RADAR data, you can generate your own data, via the following [utilities repository](https://github.com/udacity/CarND-Mercedes-SF-Utilities) created by Mercedez Innovation Garage. This repository contains Matlab scripts that can generate random LIDAR/RADAR data for EKF Testing.
