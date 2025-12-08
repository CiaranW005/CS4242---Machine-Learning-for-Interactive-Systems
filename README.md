# Punch-a-thon - Machine Learning for Interactive Systems (CS4242)

Punch-a-Thon is an arcade-style game that combines hardware, movement tracking, and machine learning to create a fun scoring challenge. Players earn points by doing three 
things: shouting, punching, and making a facial expression. Each was determined using a different ML technique running across an Arduino Nano 33 BLE Sense and FaceOSC.

The idea was to build something playful yet technically interesting, being inspired by arcade punch machines and games like “Punch-Out”, where your physical performance 
drives the score. To achieve this, we used Regression to estimate punch force, Classification to evaluate the quality of a shout, and Dynamic Time Warping (DTW) to match 
facial expressions. Players earn maximum points by punching fast, shouting loudly, and making a strong, angry expression.

## Design and Implementation:
- The shout mechanic was treated as a classification problem, allowing the system to reliably distinguish a “real” shout from
  background noise or ordinary speech. A small neural classifier was trained on recorded sample shouts, and its confidence
  output was mapped directly into the shout portion of the final score.
  <sub>Implemented by Igor</sub>

- A regression model was used to convert continuous accelerometer readings into a punch-strength value. Punches vary widely
  in angle, speed, and rotation, so regression performed better on continuous motion data than categorical approaches. The
  model rewarded straight, high-acceleration punches while penalising swinging or angled motions.    
  <sub>Implemented by Emily</sub>

- Facial expressions were analysed using DTW applied to FaceOSC’s facial-point data. Since different players express emotions
  at different speeds, DTW allowed us to match short expression sequences to template gestures even when they were not time-
  aligned. This process generated an expression score that acted as a multiplier in the final scoring system.
  <sub>Implemented by Ciarán</sub>

- All three ML outputs were integrated in MaxMSP, which handled state resets, timing, and the user-facing feedback loop. The
  final score was calculated by combining punch strength, shout confidence, and facial-expression matching, encouraging
  players to perform all three actions consistently for maximum points.

This combination kept the game responsive, fair, and enjoyable while also demonstrating how three different machine learning 
approaches can work together in real-time.

## Tools Used:
- [Arduino Library](https://docs.arduino.cc/)
- [Arduino LSM9DS1 Library](https://github.com/arduino-libraries/Arduino_LSM9DS1)
- [Wekinator](http://www.wekinator.org/)
- [Edge Impulse](https://edgeimpulse.com/)
- [Cycling74 Max 8 (MaxMSP)](https://cycling74.com/products/max)
- [FaceOSC](https://github.com/kylemcdonald/ofxFaceTracker/releases)

## Full Report

A more detailed explanation of the system, along with diagrams and reflections, can be found in the full report:

[ML for Interactive Systems - Report](report/MLForInteractiveSystems-Report.pdf)
