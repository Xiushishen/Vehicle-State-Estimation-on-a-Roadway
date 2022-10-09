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
