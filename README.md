# Berry-Harvesting-Rover
A rover bot that utilizes computer vision and a robotic arm to detect and harvest berries based on various parameters like size and colour. 

# Motivation Behind The Project
[Urban farming](https://www.thespruceeats.com/what-is-urban-farming-5188341) is a new concept that aims to utilize rooftops of apartments and similar small spaces in a city/heavily populated region to grow small plants while also expending minimum effort. For this purpose, generally smaller and more resilient plants are chosen. For this purpose, various forms of berry-type fruits such a blackberries, tomatoes, eggplants, etc. are ideal due to their small size. 

In urban farming, it is possible to automate many things, including watering of plants as well as pest control. However, automated harvesting has always been a challenge, since in berry-type plants different individual fruits ripen at different times. Hence, for this purpose, a rover capable of using computer vision to differentiate between ripened and unripened fruits is of great use.

# Design of robot
As the central control unit of the rover, we will use the Arduino Mega 2560 microcontroller based on the ATmega2560. For employing computer vision, we will use a vision sensor(camera) along with a Raspberry Pi 3 Model B. The bot must be capable of moving forward, backward and also take left or right turns. Moreover, it should be capable of precisely picking and dropping fruits in the correct areas. Hence a robotic arm with a specialised gripping mechanism is necessary. The major goal is to make achieve high accuracy at low cost. A strong and sturdy build is also desirable since it will be lifting rather heavy loads. It will be fully automated with the help of coloured guiding lines on the floor. Hence, no manual operation/controller is necessary. 

- ## Components necessary

1. Arduino Mega 2560
2. Raspberry Pi 3 Model B
3. Vision Sensor
4. IR sensors
5. Ultrasonic Sensor
6. Motor Controller
7. Adapter
8. DC motors


