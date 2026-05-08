
# Robot Maze Program. 

For this Maze Project, the locorobo had to be programmed to solve a maze. 

For this project I added several functions that all factor into the robot solving the maze. The important parts of this program include things that help it move forward, rotate, go backwards, sense walls, and use colors.


* Variables & Imported data
This robot has a set variable (that I added) with the distance between the wall and the robot. It is measured in cm and comes up later when the robot is scanning its path.

* Moving Forward
My robot starts off with going forward. In this function I added the greenLights (which will be explained in the next section). I used the Motors and a speed of 1.5. 

* Green Light
I added green lights to go along with the function of when my robot goes forward. And for this function, I used the RGB lights that are set in the robot and have them all synced on all lights. I only added this because of how in actual light intersections, green means go and red means stop. 

* Sensing Blocked Path
The robot is able to sense a blocked wall because of the data that the robot recieves from ultrasonic. With getting the data, I added it as a value to the name *distance*. So, in this function, named wallInFront, it returns the value when the distance is less than Wall_Distance (which was a value set earlier in the beginning). So, this value is what allows the robot to sense when there is a wall in front/its path is blocked. 

* Stopping
When the robot has sensed a blocked path, the robot comes to a stop. I added this as a function so I can add a function where the robot backs up a little bit. I did the stopRobot by setting the speeds to zero.

* Red Lights
This function is basically the same as the green section. But in this case, I made the lights turn red to signify a stop and for when the robot scans the areas. 

* Moving Backwards
After the robot comes to a complete stop, I had the robot move backwards. I did this by setting the motors to backward at 0.3 and then it comes to a stop. (By calling back the stop function).

* Rotations 

Now that the robot has moved backwards, it proceeds to look 90 degrees to the LEFT. I did this by including the setup_wait and including the 90 degree rotation. It then stops after turning. 
My other rotation, if the path is blocked when checking left, it turns 180 degrees to the right. The direction doesn't matter because it is doing a 180 so it just faces the opposite side. After it turns it stops. 

* Clear Path -- While Loop
With all of these functions explained, they are put into a while loop that begins True.
It starts moving forward and scans the path along the way. if wallInFront is TRUE, then it will follow the steps of stopping the robot, activating red lights (that goes along the robot stopping), and then scans the left side at 90 degrees. It goes to sleep for 0.2. If the left path is clear, it will move forward. But, if it is blocked, it will back up a bit, turn right 180 degrees, and then move forward. After that, I added the time.sleep at (0.01) because that is where it helps with for when it moves backwards. 


