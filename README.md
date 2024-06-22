## Self-Driving RC Car Project

This project builds a self-driving RC car using a Raspberry Pi, Arduino, and open-source software. The Raspberry Pi collects inputs from a camera module and an ultrasonic sensor, and sends data to a computer wirelessly. The computer processes input images and sensor data for object detection (stop sign and traffic light) and collision avoidance, respectively. A neural network model runs on the computer and makes predictions for steering based on input images. Predictions are then sent to the Arduino for RC car control.

### Getting Started
#### Prerequisites
- Raspberry Pi
- Arduino
- RC Car
- Pi Camera Module
- Ultrasonic Sensor
- Computer with Anaconda (Miniconda) installed
