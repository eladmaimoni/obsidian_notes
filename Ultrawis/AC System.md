
Conclusions From Experiment 1

1. We need to use a smoother kalman filter with adequate process noise
2. IDEA - when collecting data, we need to cut off the data on a certain velocity (for example - when it first reaches 0.2 DPS) and fit the curve to this velocity. The filter responds quite slowely to changes at low speed) AND the Kalman filter my not reach slow speed so quickly.
3. We need to incorporate a cutoff velocity (probably 0.1 DPS)
4. We might want to incorporate control vectors into the equation - such as joystick
5. Calibration process should find:
   1. max velocity per gear
   2. deceleration when there are no joystick inputs (AKA friction declaration)
   3. acceleration at each gear
6. we need to test what happens when we 'help' the crane with 'counter slew'
7. do we need to model emergency break?

ABB tasks

1. stabilize frequency and interval, remove debugging data (encoder turns etc)
2. purchase SVN package - Salome takeover
3. incorporate joystick input data to the inputs
4. check if we can incorporate emergency break into the data
5. weight gauge integration?
6. 