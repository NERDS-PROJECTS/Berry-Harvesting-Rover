# Berry-Harvesting-Rover
A rover bot that utilizes computer vision and a robotic arm to detect and harvest berries based on various parameters like size and colour. 

# Motivation Behind The Project
[Urban farming](https://www.thespruceeats.com/what-is-urban-farming-5188341) is a new concept that aims to utilize rooftops of apartments and similar small spaces in a city/heavily populated region to grow small plants while also expending minimum effort. For this purpose, generally smaller and more resilient plants are chosen. For this purpose, various forms of berry-type fruits such a blackberries, tomatoes, eggplants, etc. are ideal due to their small size. 

In urban farming, it is possible to automate many things, including watering of plants as well as pest control. However, automated harvesting has always been a challenge, since in berry-type plants different individual fruits ripen at different times. Hence, for this purpose, a rover capable of using computer vision to differentiate between ripened and unripened fruits is of great use.

# Design of robot
As the central control unit of the rover, we will use the Arduino Mega 2560 microcontroller based on the ATmega2560. For employing computer vision, we will use a vision sensor(camera) along with a Raspberry Pi 3 Model B. The Raspberry Pi and Arduino can be connected via UART. The bot must be capable of moving forward, backward and also take left or right turns. Moreover, it should be capable of precisely picking and dropping fruits in the correct areas. Hence a robotic arm with a specialised gripping mechanism is necessary. The major goal is to make achieve high accuracy at low cost. A strong and sturdy build is also desirable since it will be lifting rather heavy loads. It will be fully automated with the help of coloured guiding lines on the floor. Hence, no manual operation/controller is necessary. In the present iteration, a wired connection with a computer terminal is used to start the system and display information about number and size of fruits collected. 

![components](https://user-images.githubusercontent.com/91414273/200113429-9b8ff518-fe70-4226-8c62-05c6f1df11e3.jpg)

We will use 2 DC geared motors with position encoders mounted on its shaft to traverse the arena along the black line. The feedback from the position encoders will be used to stop the robot at a given distance from the tree.

![motor connection](https://user-images.githubusercontent.com/91414273/200113440-5c4aa47c-56d5-4f85-9309-1608daabac5f.jpg)

- ## Components necessary

1. Arduino Mega 2560
2. Raspberry Pi 3 Model B
3. Vision Sensor
4. IR sensors
5. Ultrasonic Sensor
6. Motor Controller
7. Adapter
8. DC motors
9. Robotic arm

- ## Robotic arm design

A functional robotic arm can be created for prototyping purposes using a simple arrangement of two servo motors for up-and-down motion, and a DC motor for plucking the fruits. However, a special cup-shaped gripper is required so that the pressure from the DC motor does not squish the fruit.

![gripper_opened](https://user-images.githubusercontent.com/91414273/200113355-a71e12ad-61c2-49b1-9877-c6f4bd8bd9c4.png)

- ## Procedure for fruit detection

1. The bot will take a picture of tree when stopped before it.
2. The image will be processed to find contours in the image.
3. Bounding boxes will be drawn for each contour and the areas will be found.
4. The fruit block will be detected by comparing the contour area with a threshold range (the range will be found after initial testing)
5. When the block is found the bounding rectangle will be written as a new & separate image for further processing.
6. This image will be resized to match the sample images.
7. The image will be blurred using cv2.medianBlur() and more noise will be removed by using erosion techniques.
8. The image will be processed again to find contours in the image.
9. An upper & lower limit of contour area will be saved so that all other areas outside this range will be neglected.
10. Within this range, three different ranges will be predefined for finding the size of fruit i.e. max, large and small.
11. To find the colour of fruit we will create a bounding rectangle of the found fruit contour. A function will return the length and breadth of rectangle along with co-ordinates of point shown below.
12. Then we will move downward from the pixel co-ordinate shown below and will find a point where the colour value changes sharply. This colour value will be stored for identification purposes.
13. The type of fruit will be identified by three different colour ranges for each fruit (found after initial testing).
14. Finally, the size and type of fruit will be stored and displayed on the terminal. 

The fruit detection algorithm can be viewed in fruit_detection.py file.

# Bot Navigation

Navigation of bot will be done through a grid of lines with plants on a few or all of the nodes. Such a bot can be easily implemented using the line follower principle and IR sensors. [Here](https://create.arduino.cc/projecthub/saher-iqbal/line-follower-robot-36516b) is a simple tutorial on implementing a line follower algorithm.

![Line follower flowchart](https://user-images.githubusercontent.com/91414273/200115025-c966dc15-c16c-43df-b046-947b10aedc71.jpg)

The code for bot navigation algorithm can be found in the bot_navigation.ino file.

# Scope for further improvement

- In the present iteration, bot is still dependant on a wired connection with a computer to start it. A fully automated bot can be the next step where it automatically starts up at a certain suitable time of the day, stores data about number of fruits collected locally, and turns off/hibernates while not in use.
- Similarly, an automated charging system can be implemented.
- Once a fully automated system is perfected, it can be scaled up to cover entire plantations efficiently with little to no manual labour.

# References

https://www.irjet.net/archives/V7/i3/IRJET-V7I3721.pdf
