# gravitation
Computational assignment for University Physics course (calculus-based)

This assignment is adapted from the assignment "A Space Voyage: Part 1" from the excellent textbook Matter and Interactions, by Chabay and Sherwood. 

In this program you will model the motion of a spacecraft moving near the Earth. You will use your working program to explore the eﬀect of the spacecraft’s initial velocity on its trajectory. 

After completing this activity you should be able to:
* Identify what quantities must be calculated inside a computational loop 
* Write a program to model the motion of two gravitationally interacting objects 
* Explain why the initial velocity of an object aﬀects its trajectory as it moves near a more massive object 
* Draw a diagram showing the directions of momentum and net force at diﬀerent locations along an elliptical orbit

## Explain and predict

Study the following VPython program carefully. Make sure you understand the whole program, but don’t run the program yet. Reading and explaining program code is an important part of learning to create and modify computational models.

```
G = 6.7e-11 
mEarth = 6e24 
mcraft = 15e3 
delta_t = 12 * 60 * 60 #Converting time period to SI units of seconds. What were the units of time 12?
Earth = sphere(pos=vector(0,0,0), radius=6.4e6, color=color.cyan) 
craft = sphere(pos=vector(-10*Earth.radius, 0,0), radius=1e6, color=color.yellow, make_trail=True) 
craft.velocity = vector(0,2e3,0) 

while t < 10*365*24*60*60: 
  sleep(delta_t/(12*3600)) #Every 12 hours will be displayed as 1 second
  craft.pos = craft.pos + v_craft*deltat 
  t = t+deltat
```
Without running the program, answer the following questions: 
* What is the physical system being modeled? 
* In the real world, how should this system behave? 
* On the left side of your whiteboard or paper, draw a sketch showing how you think the objects should move in the real world. 
* Will the program as it is now written accurately model the real system? 
* On the right side of the whiteboard or paper, draw a sketch of how the objects created in the program will move on the screen, based on your interpretation of the code

## Modify and extend the model
Run the program. 
* How did your prediction compare to what you saw? Did something happen that you didn’t expect to happen? 
* How should the program be changed so that it is a physically reasonable model of the system? 
* Modify the program. Run it and compare its behavior to the behavior you expect from the real system.

Check your work before continuing

Everything above was basically copied from Chabay and Sherwood. Below I write something different.

## Further extensions

Answer the following questions.
1. Adjust the time step until decreasing it further does not change the observable results. When the code gives the same output to the desired precision, we say that it is "converged". What time step is necessary to obtain convergence?
2. Calculate the velocity that should lead to a circular orbit (in python, not on your calculator, print your output). Test that you do get a circular orbit.
3. Experiment until you find the minimum velocity that leads to an orbit that never comes back. 
