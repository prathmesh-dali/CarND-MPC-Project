# CarND-Controls-MPC
Self-Driving Car Engineer Nanodegree Program

---

## Introduction
---

This repo contains my solution to MPC assignemnet of term 2 SDC.

## The Model

---

1. States:-
    * px - x-coordinate of current location of vehicle in global map.
    * py - y-coordinate of current location of vehicle in global map.
    * psi - current orientation of vehicle.
    * v - current velocity of the vehicle.
    * cte - cross track error, which is measured w.r.t desired position of the vehicle.
    * epsi - error in orientation of vehicle w.r.t desired orientation.
2. Actuations:-
    * delta - steering angle of the vehicle by which vehicle will turn. This angle is restricted between 25 to -25 degrees.
    * a - throttle or brake  of the vehicle which accelerates or descelerates vehicle. Value of throttle is restricted between -1 to 1.

3. Kinematic Model:-
    - px` = px + v * cos(psi) *dt
    - py` = py + v * sin(psi) *dt 
    - psi` = psi + v / Lf * -delta *dt
    - v` =  v + a * dt
    - cte` = cte + v * sin(epsi) * dt
    - espi` = espi + v / Lf * -delta *dt 

## N & dt

---
**Values used in this project for N and dt are 10 and 0.1 respectively.** Actually I have taken these values from udacity QnA video and somehow after trying for multiple vaules from N -> 5-20 and dt -> 0.06-0.2 these values worked well for me. And it makes sense since taking N very low will result in predicting for shorter future and taking it too high will result in predicting for longer future values which intern will result in complex and long running computations. 

## MPC Preprocessing

---
Before passing the values to polyfit I am converting those to vehicle co-ordinate system which inturn results in easier computations as vehicle x and y are 0, 0 as vehicle location will be origin and orientation angle also will be 0. I used 3rd order polynomial for fitting as it can model road lanes properly. Taking higher order polynomial will result in comple computations and taking lower order polynomial will not give proper approximation while calculating minima.

## Model Predictive Control with Latency
---
For tackling latency I am using Kinematic model equations specified above to compute states after the period of latency. Then these predicted states are passed to model for optimizing.

## Final video
---
<p  align="center"><a href="https://youtu.be/TfZZmo54vvg" target="_blank"><img src="https://img.youtube.com/vi/TfZZmo54vvg/0.jpg" alt="IMAGE ALT TEXT HERE" width="480" height="300" border="1" /></a></p>