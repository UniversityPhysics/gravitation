# Moonshot I
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
delta_t = 6*60*60 # 2 hours (in seconds)
Earth = sphere(pos=vec(0,0,0), radius=6.4e6, color=color.cyan)
craft = sphere(pos=vec(-10*Earth.radius, 0,0), radius=1e6, color=color.yellow, make_trail=True)
Moon = sphere(pos=vec(4e8,0,0), radius=1.75e6, color=color.white, make_trail=True)

Earth.mass = 6e24
craft.mass = 15e3

craft.velocity =  vec(0,3e3,0)

t = 0

while t < 365*24*60*60:
    sleep(delta_t/(24*3600)) #Every 24 hours will be displayed as 1 second

    #update force and acceleration
    craft.rEarth=craft.pos-Earth.pos #r is a vector from the craft to the earth
    craft.rMoon=craft.pos-Moon.pos #r is a vector from the craft to the earth
    craft.Fnet = 0.0
    craft.acceleration = craft.Fnet/craft.mass

    #update velocity
    craft.velocity = craft.velocity + (craft.Fnet/craft.mass)*delta_t
    Moon.velocity = Moon.velocity
    
    #update position
    craft.pos = craft.pos + craft.velocity*delta_t
    Moon.pos = Moon.pos   
    
    #Detect collision
    if mag(craft.rMoon) < Moon.radius:
        break ## exit from the loop

    t = t + delta_t
```

More efficient than paste-and-see is to read the code and discuss with a partner what you think will happen, line-by-line. Compare your answers to the following questions.
* What is the physical system being modeled? 
* In the real world, how *should* this system behave? 
* On the left side of your whiteboard or paper, draw a sketch showing how you think the objects should move in the real world. 
* Will the program as it is now written accurately model the real system? 
* On the right side of the whiteboard or paper, draw a sketch of how the objects created in the program will move on the screen, based on your interpretation of the code

## Complete the model of motion of the craft subject to earth's gravity
Run the program. 
* How should the program be changed so that it is a physically reasonable model of the system? 
* Modify the program. Run it and compare its behavior to the behavior you expect from the real system.

In Python, it's simple to calculate the magnitude of the force of gravity using the quantities already defined. It's also simple to calculate the direction of the force of gravity using the function `norm(r)`, which calculates a unit vector in the direction of any vector `r` in the argument.

Checkpoint: your craft should follow a path affected by gravity.

## This code numerically integrates velocity
In the limit that the time step size goes to zero, the result of this code should converge to a well-defined limit. In practice making the step size too small actually leads to the accumulation of numerical error, in addition to making the computation take too long. The thing to do is to decrease the step size until the result no longer improves, then say "that's good enough". Decrease the step size until the orbit seems to be correct.

*You and your partner need to have a step size that is at least slightly different* I don't want to see identical work for the moonshot step.

## Add the gravitational attraction by the moon
The net force on the craft should be the vector sum of the interaction with the earth and also the interaction with the moon.

## Moonshot I

Adjust the initial velocity of the craft until it lands on the moon! Because you have a different delta_t than your partner, you will have a different initial velocity.

## Add arrows to represent force and velocity

The force vector is not a displaccement vector, and we can't just draw an arrow with length equal to the force. What we can do is to draw an arrow with an `.axis` property that is equal to the force vector multiplied by a scale factor so that force vectors are not too large and not too small to see. The scale factor is like a "conversion" where you divide by a typical force magnitude then multiply by a typical distance magnitude to make the force vectors big enough to see. You can choose a scale factor according to your personal preference, but do it before your time loop and don't update the scale (so all vectors will be on the same scale).

Add arrows showing the velocity and force before the time loop

````
#Define arrows with scale factors to illustrate momentum and force
typicalDistance = 1.0*mag(Moon.pos-Earth.pos)
typicalVelocity = mag(craft.velocity)
print("first guess for what scale factor to multiply velocity: ",typicalDistance/typicalVelocity)
scaleVelocity = 

craft.rEarth=craft.pos-Earth.pos
typicalForce=G*Earth.mass*craft.mass/mag(craft.rEarth)**2
print("first guess for what scale factor to multiply force: ",typicalDistance/typicalForce)
fArrow = arrow(pos = craft.pos, color=color.red)
vArrow = arrow(pos = craft.pos, color=color.white) 
````
At the end of your time loop (just before `t=t+delta_t`), update the position and axis properties of these arrows like this

````
    #update vector arrows
    vArrow.pos = craft.pos
    vArrow.axis = craft.velocity*scaleVelocity
    fArrow.pos = craft.pos
    fArrow.axis = craft.Fnet*scaleForce
````

## Further extensions (optional)

Calculate the velocity that should lead to a circular orbit (in python, not on your calculator, print your output). Test that you do get a circular orbit.

Experiment until you find the minimum velocity that leads to an orbit that never comes back. 

Yes, you could also let the Moon orbit the earth, and we'll do that next time.

