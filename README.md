![Alt text](screenshot.png "Screenshot")

webcam-pulse-detector
=====================

A python application that detects the heart-rate of an individual using their 
computer's webcam.

Inspired by reviewing recent work on Eulerian Video Magnification (http://people.csail.mit.edu/mrub/vidmag/), 
with motivation to implement something comparable in python-opencv based on a few previous efforts (such as 
https://github.com/mossblaser/HeartMonitor).

Data processing is implemented within an openMDAO assembly to facilitate rapid prototyping/redesign of the real-time 
analysis, and simple embedding into a python application.

Requirements:
---------------

- Python v2.7+ (http://python.org/)
- OpenCV v2.4+, with the cv2 python bindings (http://opencv.org/)
 
OpenCV is a powerful open-source computer vision library, with a convenient 
numpy-like interface in the cv2 bindings.

- OpenMDAO v0.5.5+ (http://openmdao.org/)

OpenMDAO is an open-source engineering framework that serves as a convenient 
object-oriented enviroment to containerize and easily make tweaks to the required 
real-time analyses.
It requires python 2.6+, numpy, scipy, and matplotlib 
(see http://openmdao.org/docs/getting-started/requirements.html)

Quickstart:
------------
- Activate the openMDAO virtual python environment in a command or terminal window
- Navigate to the downloaded source directory, and run get_pulse.py to start the application

Usage notes:
----------
- When run, a window will open showing a stream from your computer's webcam
- The application will search for a human face within the camera frames, and 
attempt to isolate an area on the forehead
- Support for pulse-detection on multiple simultaneous people in an camera's 
image stream is possible, but at the moment only the information from one face 
is extracted for cardiac analysis
- When a forehead location has been isolated, the user should press "S" on their 
keyboard to lock this location, and remain as still as possible (the camera 
stream window must have focus for the click to register). This freezes the aquisition location in place.
- The application will then track the variations in this location over time to 
measure a heartbeat. To view a stream of this data, press "D".
- The data display shows three data traces, from top to bottom: 1) raw optical 
intensity, 2) extracted heartbeat signal, 3) Power spectral density, with local 
maxima indicating the heartrate (in beats per minute). 
- With good lighting and minimal noise due to motion, a stable heartbeat should be 
isolated in about 15 seconds. When the conditions are good, other physiological waveforms, such as Mayer waves 
(http://en.wikipedia.org/wiki/Mayer_waves), should also be visible in the raw data stream (top).
- If a large spike in optical intensity is measured in the data (due to motion 
noise, sudden change in lighting, etc) the data collection process is reset and 
started over

TODO:
------
- Show the detected bpm somewhere in the camera stream
- Support for multiple individuals
- Smoother tracking of data from foreheads, perhaps by buffering and registering/inverse-transforming image subframes

