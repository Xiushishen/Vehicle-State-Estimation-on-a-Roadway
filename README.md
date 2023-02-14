# Vehicle-State-Estimation-on-a-Roadway
An ES-EKF was implemented to estimate the vehicle state as accurately as possible. ES-EKF mainly consists of three steps: namely prediction, measurement, and correction. The prediction step employs the vehicle's dynamic model to predict the current state of the vehicle using IMU data. The IMUs generally do not have very high precision and therefore the predictions can deviate largely overtime if only IMU data is used for vehicle state estimation. Therefore, LIDAR point cloud and GNSS data is measured in the measurement step whenever available to get a better idea of the ground truth values since the error rates for these measurements are very low. In real world scenarios, these measurement sources are not available for calculation at each timestep since it may depend on the LIDAR sensor scan rate, GPS connectivity and hardware refresh rates. When measurement data is not available a rough estimate using the prediction stage might suffice; However, when measurement data is available, the correction step is used to penalize the systems' state estimation errors and improve estimation accuracy.

The implementation of ES-EKF algorithm in the update loop is as follows.

Update nominal state with motion model
Propagate uncertainty
If a measurement is available:
a. Compute Kalman Gain
b. Compute error state
c. Correct nominal state
d. Correct state covariance
The illustration below shows the above pseudocode in a workflow diagram.
![image](https://user-images.githubusercontent.com/103896788/194776029-e3138738-3b4f-47c3-9ec2-9125d016151c.png)
# Results
Part 1: ES-EKF using Inertia Measurement Unit (IMU) data for prediction step and LIDAR point cloud and GPS for correction.
Vehicle state estimates | State estimation error plot
:-------------------------:|:-------------------------:
<img src='https://github.com/Xiushishen/Vehicle-State-Estimation-on-a-Roadway/blob/main/Vehicle%20State%20Estimation%20on%20a%20Roadway/Images/Part_1.png'> | <img src='https://github.com/Xiushishen/Vehicle-State-Estimation-on-a-Roadway/blob/main/Vehicle%20State%20Estimation%20on%20a%20Roadway/Images/Part_1_error_plots.png'>

Part 2: With adjusted filter parameters to account for calibration errors introduced in LIDAR sensor.
Vehicle state estimates | State estimation error plot
:-------------------------:|:-------------------------:
<img src='https://github.com/Xiushishen/Vehicle-State-Estimation-on-a-Roadway/blob/main/Vehicle%20State%20Estimation%20on%20a%20Roadway/Images/Part_2.png'> | <img src='https://github.com/Xiushishen/Vehicle-State-Estimation-on-a-Roadway/blob/main/Vehicle%20State%20Estimation%20on%20a%20Roadway/Images/Part_2_error_plots.png'>

Part 3: Effects of sensor dropout, that is, when all external positioning information (from GPS and LIDAR) is lost for a short period of time.
Vehicle state estimates | State estimation error plot
:-------------------------:|:-------------------------:
<img src='https://github.com/Xiushishen/Vehicle-State-Estimation-on-a-Roadway/blob/main/Vehicle%20State%20Estimation%20on%20a%20Roadway/Images/Part_3.png'> | <img src='https://github.com/Xiushishen/Vehicle-State-Estimation-on-a-Roadway/blob/main/Vehicle%20State%20Estimation%20on%20a%20Roadway/Images/Part_3_error_plots.png'>
