# Line-follower project
A line follower is a type of autonomous robot or vehicle (in our case a robot that sort of looks like a vehicle) designed to follow a visible path or line on the ground. This path is typically marked with a contrasting color, such as black on a white surface (like in our case) or vice versa. The robot uses sensors, usually infrared sensors, to detect the line and make adjustments to stay on course. The basic working principle involves the use of sensors to detect the contrast between the line and its surroundings. The sensors generate electrical signals based on the intensity of light reflected from the surface. By analyzing these signals, the robot can determine whether it is on the line, off to one side, or completely off the track. To navigate along the line, the robot employs control algorithms that enable it to make adjustments to its speed and direction in real-time. For example, if the robot drifts to the right of the line, it may increase the speed of the left motor or decrease the speed of the right motor to steer itself back onto the correct path. In our case, the robot uses PID control to stay on track.
What did we have to do?

As teams of three, we had a day to spend on college grounds to put together a line follower that would successfully complete a given circuit within a timeframe. We hade to manually cut and glue together the "body" of our robot and attach to it the hardware parts. Ideally, for maximum grade, our little Lightning McQueen was supposed to complete the circuit in under 20 seconds. During grading, we were allowed to showcase the line follower 3 times before our grade was calculated using the best time from those 3 tries. Our luck made it so we missed the maximum grade by one second, but nonetheless it was a great performance since 3 hours before we presented the project nothing worked and we were about to blow up our battery two times.
What is PID?

PID (or Proportional-Integral-Derivative) is a feedback control system widely used in engineering and automation. PID controllers are commonly used in various applications to regulate and control processes, such as temperature, speed, position etc.

How it works:

    Proportional: The proportional term is directly proportional to the current error, which is the difference between the desired setpoint and the actual value. It produces an output that is proportional to the present error. This term contributes to the overall correction based on the magnitude of the error.

    Integral: The integral term considers the accumulated sum of past errors over time. It is responsible for eliminating any residual steady-state error that might persist with only proportional control. The integral term helps to reduce the long-term error by adjusting the output based on the accumulated historical error.

    Derivative: The derivative term is proportional to the rate of change of the error. It anticipates future behavior of the system by considering how quickly the error is changing. The derivative term helps to dampen the system's response, preventing overshooting and oscillations.

A PID controller's output is the sum of these three terms, each adjusted by respective constants (proportional gain denoted by kp, integral gain denoted by ki, and derivative gain denoted by kd). The combination of these terms allows the controller to provide a more accurate and responsive control action, improving the system's stability and performance.
How did we use PID for our line follower?

In truth, our team assigned values to kp, ki and kd by trial and error, until we finally hit the right set of values that would stabiilize our line follower. In reality, this is how a PID controller should work for a line follower:

    Error Calculation: Calculate the error, which is the difference between the desired position (center of the line) and the actual position of the robot based on sensor readings.
    P control: Adjust the robot's steering based on the proportional term. If the robot is to the right of the line, increase the left motor speed or decrease the right motor speed (and vice versa). The amount of adjustment is proportional to the error.
    I control: Address any persistent steady-state error by using the integral term. Sum up the errors over time and apply a correction to the motor speeds.
    D control: Add damping to the system by considering the rate of change of the error.
    Combine PID Terms: Calculate the PID output by summing the proportional, integral, and derivative terms with their respective coefficients : PID Output = (p * kp) + (i * ki) + (k * kd).
    Apply PID and tune parameters: Apply the PID output to adjust the speeds of the robot's motors which will results in corrections that bring the robot back to the line and fine-tune the gains experimentally to achieve the desired line-following performance.

What parts did we need?

    Arduino Uno
    Zip-ties (very importand and lifesaving)
    Powersource (in our case, a LiPo battery, or two if you worry about blowing up one of them)
    2 rubber wheels
    QTR-8A reflectance sensor (detects how much infrared light is reflected from a nearby surface)
    Wires (especially male-female for the sensor)
    Nuts and bolts
    Ball caster
    Chassis or the body of the LF (DIY made)
    Breadboard
    L293D driver
    2 DC motors

How did we do it?

We started by making the chassis of the line follower: using a foam board provided by our teacher, a 3D model to take inspiration from and a cutter, we had to handmade the body of the LF the best we could. Putting our crafting skills at work, we managed to make a sturdy chassis for the robot in little over 2 hours. After a short pizza break, it was time to assemble the car. It took us a bit to figure out how to exactly connect everything, but we managed to do a fine job.

![299414186-e831e28d-18b1-4eec-86ee-6d00e78f1f6e](https://github.com/anamaria1-png/Line-follower/assets/89720718/4ee42b46-f2d8-4e38-8034-da16319081e2)
![299414695-e3917069-5faa-4ea4-ad73-e3c97a662931](https://github.com/anamaria1-png/Line-follower/assets/89720718/8f52d2af-dcaa-49e3-9a46-b4f84dac88fe)
Then, with the code provided in the last laboratory, we started testing how it works. We soon realized it doesn't and it didn't take us long to figure out that the problem was the calibration, but it took us enough to figure out that we didn't attach the sensor as we should've; it couldn't read the ground since the foam board blocked it, so we had to grab the cutter and carve through our chassis again. Then, we could finally test it, but we ran into other problems. Firstly, we didn't carefully follow the instruction and disconnected the battery wires incorrectly, so the ends touched and it short circuited, which caused it to heat up severely. Once we solved that, we encountered another issue: due to a wire connectivity issue, the battery heated up again and this time, it caught fire for a second before we disconnected it, melting the plastic of our wires. After replacing the battery and building up the courage to connect it to our LF again, we finally managed to start testing the code for reals. It took us an insane amount of time to find the right triple of values for kp, ki and kd to make our little car work, but our issues weren't solved then either. We had to hardcode a way for our LF to ignore small errors because it was too slow, completing the circuit in about 40 seconds, which was a lot. Calibrating the sensor automatically was another pain we had to go through, but, after trying lots of alternatives - including trying to store a manual calibration in EEPROM - we managed to fix it somehow (although I think none of us is really sure how).

The final result was very satisfying, you can watch how our line follower completes the circuit here: Line follower demo.
In the end, even though we spent 12 hours on college grounds (until 12AM), which I wouldn't wish upon my worst enemy, it was genuinely a fun experience and our work felt nicely rewarded when we saw our Lightning McQueen successfully completing the circuit in a decent amount of seconds :)

Another pic of our car, this time with the battery we didn't blow up:
![299418907-cbf2b33e-4daa-4e27-b280-cb11c8f45c11](https://github.com/anamaria1-png/Line-follower/assets/89720718/760180cb-eefc-4369-827b-4a0efc85b93f)

https://youtu.be/rWC1NJsf9Xo

Project done in partnership with @slayyyyyyy  and @malinaalexa (team Slay).





