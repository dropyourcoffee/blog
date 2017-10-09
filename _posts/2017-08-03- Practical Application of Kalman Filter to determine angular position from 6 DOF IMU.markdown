---
layout: post
title:  "Kalman Filter to determine orientation (angular position) from 6 DOF IMU sensor"
date:   2017-08-03 10:43:53 +0900
categories: IMU
---
<script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

Estimating orientation by measuring gravitational acceleration with accelerometer is very reactive however, it is in general very noisy since it always has noise due to translational movements.
On the other hand, we could double-integrate angular acceleration measured by gyroscope to determine the angular velocity, however the problem with the gyro is that it drifts over time,

In short,
* Orientation estimate from *accelerometer* over a time period can be trusted, but instantaneous data is not accurate.
* Orientation estimate from *gyroscope* over a time period diverges due to accumulated errors by drift, but instantaneous data is generally more accuarate than the former.

### Kalman Filter
> In any place where you have **uncertain information about some dynamic system**, and you can make an **educated guess** about what the system is going to do next.<br>
[Kalman filter explanation](http://www.bzarg.com/p/how-a-kalman-filter-works-in-pictures/)

Basically, we can use Kalman filter to fuse two inertial sensors and find the optimised gain(Kalman Gain) for each inputs.<br>
Kalman Filter algorithm consists of two repetitive stages:

1. Time Update(Prediction) - Predict gravitational orientation based on accelerometer value and gain<br>
2. Measurement Update(Correction) - Update the measurement with gravitational orientation based on gyroscope and update gain.<br>

We continuously update accelerometer(input with noise) with gyro data(true values).


* Time update(Prediction)
In Prediction, we estimate values based on input + previous state<br>
![Time Update(Prediction)]({{ site.url }}/img/2017-08-03-img1.jpeg)<br>
*Time Update(Prediction)*

* Measurement update(Correction)
In Measurement, we compare previous estimate with actual measurement and modulate Kalman Gain.<br>
![Measurement Update(Correction)]({{ site.url }}/img/2017-08-03-img2.jpeg)<br>
*Measurement Update(Correction)*
<br><br>
where, <br>
$$ X_k $$         : Accelerometer value X at time, k<br>
$$    \hat{X} $$  : Prediction<br>
$$ X^-_k $$       : Previous
$$ u_k $$         : Gyroscope value U at time, k <br>
$$ P $$           : 2x2 Error Covariance Matrix<br>
$$ Q $$           : Process noise Covariance ()<br>
$$ R $$           : Measurement Covariance (Noise)<br>
$$ z_k $$         : Actual Measurement<br>
$$ I $$           : 2x2 Identity Matrix<br>

![ State Transition Model]({{ site.url }}/img/2017-08-03-img3.png)
<br>
### Example C Code
{% highlight cpp %}
// Kalman.c

double Q_angle, Q_gyro, R_measure ; // Value in interest
double angle, bias ;
double P[2][2]; // Error Covariance
double K[2] ; // Kalman Gain

double predict(double acc, double gyro, double dt) {
  angle += dt * (gyro - bias) ;

  //Project the error covariance ahead
  P[0][0] += dt * (dt * P[1][1] - P[0][1] - P[1][0] + Q_angle) ;
  P[0][1] -= dt * P[1][1] ;
  P[1][0] -= dt * P[1][1] ;
  P[1][1] += Q_gyro * dt ;

  //Kalman Gain
  double S = P[0][0] + R_measure ;
  K[0] = P[0][0] / S ;
  K[1] = P[1][0] / S ;

  // Update with measurement
  double y = acc - angle ;
  angle += K[0] * y ;
  bias += K[1] * y ;

  //Update P
  double P_prev[2] = {P[0][0], P[0][1]} ;
  P[0][0] -= K[0] * P_prev[0] ;
  P[0][1] -= K[0] * P_prev[1] ;
  P[1][0] -= K[1] * P_prev[0] ;
  P[1][1] -= K[1] * P_prev[1] ;

  return angle ;
} ;

void init(double angle, double gyro, double measure) {
  Q_angle = angle ;
  Q_gyro = gyro ;
  R_measure = measure ;

  angle = 0 ;
  bias = 0 ;

  P[0][0] = 0 ;
  P[0][1] = 0 ;
  P[1][0] = 0 ;
  P[1][1] = 0 ;
};

double getVal(int num) {
  switch (num) {
    case 0 :
      return Q_angle ;
      break ;
    case 1 :
      return Q_gyro ;
      break ;
    case 2 :
      return R_measure ;
      break ;
  }
};
{% endhighlight %}