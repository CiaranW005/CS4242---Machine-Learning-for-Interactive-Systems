# Punch-a-thon - Machine Learning for Interactive Systems (CS4242)

Punch-a-Thon is an arcade-style game that combines hardware, movement tracking, and machine learning to create a fun scoring challenge. Players earn points by doing three 
things: shouting, punching, and making a facial expression. Each was determined using a different ML technique running across an Arduino Nano 33 BLE Sense and FaceOSC.

The idea was to build something playful yet technically interesting, being inspired by arcade punch machines and games like “Punch-Out”, where your physical performance 
drives the score. To achieve this, we used Regression to estimate punch force, Classification to evaluate the quality of a shout, and Dynamic Time Warping (DTW) to match 
facial expressions. Players earn maximum points by punching fast, shouting loudly, and making a strong, angry expression.

## Design and Implementation:
- The shout mechanic was treated as a classification problem, allowing the system to distinguish a "real" shout from other
  loud sounds. The model's confidence score was then 
  directly integrated into the final gameplay score.
  <sub>Implemented by Igor</sub>

- A regression model was utilised to convert continuous accelerometer readings into a punch-strength score. Since punches can
  vary significantly in angle and speed,
  regression was selected because it effectively handles continuous sensor data, providing more reliable results than
  category-based methods.
  <sub>Implemented by Emily</sub>

- Facial expressions were analysed using DTW on FaceOSC data. DTW was chosen because players express emotions at different
  speeds, and this technique is effective for
  matching sequences that do not align perfectly in time.
  <sub>Implemented by Ciarán</sub>

- All three ML outputs were combined inside MaxMSP, which handled timing, state resets between rounds, and visual feedback.
  The final score multiplied punch strength, shout confidence, and facial-expression matching to reward players who performed
  all three actions consistently.

This combination kept the game responsive, fair, and fun to use while also demonstrating three different ML approaches 
working together in real time.

## Tools Used:

[Arduino Library](https://docs.arduino.cc/)

[Arduino LSM9DS1 Library](https://github.com/arduino-libraries/Arduino_LSM9DS1)

[Wekinator](http://www.wekinator.org/)

[Edge Impulse](https://edgeimpulse.com/)

[Cycling74 Max 8 (MaxMSP)](https://cycling74.com/products/max)

[FaceOSC](https://github.com/kylemcdonald/ofxFaceTracker/releases)
