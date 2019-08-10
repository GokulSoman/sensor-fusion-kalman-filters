# Sensor Fusion Module implementing Extended Kalman Filters for LIDAR/RADAR inputs

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
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make` 
   * On windows, you may need to run: `cmake .. -G "Unix Makefiles" && make`
4. Run it: `./ExtendedKF path/to/input.txt path/to/output.txt`. You can find
   some sample inputs in 'data/'.
    - eg. `./ExtendedKF ../data/sample-laser-radar-measurement-data-1.txt output.txt`

## Code Style

The follwoing code follows [Google's C++ style guide](https://google.github.io/styleguide/cppguide.html), and has been thouroghly checked for any potential data leaks and C++ 11 syntax formats.

## Generating Additional Data

If you wish to generate another random sample fo LIDAR and RADAR data, you can generate your own data, via the following [utilities repository](https://github.com/udacity/CarND-Mercedes-SF-Utilities). This repository contains Matlab scripts that can generate random LIDAR/RADAR data for EKF Testing.
