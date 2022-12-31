University of Pennsylvania, ESE 5190 Final Project: Step Counter

    Team Walkman🚶‍♂️
    Group Members: Pan hao, Lihong Zhao and Xingjian Chen
    Tested on: 1. Lenovo Legion 5 Pro 16" Laptop, Intel Core i7-12700H， Windows11 
               2. MacBook Air (M1, 2020), macOS Ventura 13.0
               3. Lenovo Legion R9000P 2021 15.6"
               
# Overview

In this project, we build a steps counter to detect people’s daily walking by using the IMU and LCD screen.
加点东西

# Showcase

[![Demo_Step-Counter](https://res.cloudinary.com/marcomontalbano/image/upload/v1672286692/video_to_markdown/images/youtube--YtTOuhUdWrI-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://youtu.be/YtTOuhUdWrI "Demo_Step-Counter")
           
# Instruction

## Component

### Pico4ml_Board

<div align=center>
<img src="https://github.com/ryanhpan/ESE5190-Final-Project/blob/main/media/materials/arducam-pico4ml-tinyml-dev-kit.webp" width="700">  
</div>

## Block Diagrams

<div align=center>
<img src="https://github.com/ese5190-walkman/ese-5190_final_project/blob/main/media/design/block_diagram.png" width="800">  
</div>

- The IMU module detects the movement of the user and generates the data of acceleration of linear velocity and  angular velocity.
- The Filter Algorithms remove the high frequency noise from the raw data. 
- The Data Processor identifies the signal pattern of “walking”.
- The Program counts the amount of steps in a certain amount of time.
- LCD Screen shows the amount of steps on the screen.

## Descritption of RP2040 development enviroment

## Code
By using the sdk for ICM20948 and LCD_st7735, we are now able to successfully read the acceleration and gravity data from IMU(ICM20948) and get it to display on the LCD screen (LCD_st7735) which is used by PIO.

Also, following professor's advice, we tried to find a few fixed reference points based on the camera module but we observed that the array read by camera was strange and it was hard to extract the data from it and find a few points as coordinate points within limitted amount of time. So we gave up that idea. 

The code is [here](https://github.com/ese5190-walkman/ese-5190_final_project/tree/main/code/in-progress).

### Libraries
- [ICM20948](https://github.com/ese5190-walkman/ese-5190_final_project/tree/main/code/libraries/ICM20948)
- [LCD_st7735](https://github.com/ese5190-walkman/ese-5190_final_project/tree/main/code/libraries/LCD_st7735)
- [Arducam_hm01b0](https://github.com/ese5190-walkman/ese-5190_final_project/tree/main/code/libraries/Arducam_hm01b0)

# Narrative overview of project's development

The first step of the project is to figure out how the IMU module works, what kind of data can it provide? By reading the datasheet and performing some testing, we realize that IMU can provide us the data of acceleration and gravity from three direction. The next step is that we need to design the algorithm that detect whether the sensor is moving and try to define what is one step. After a fully test of the algorithm, the final step is to use the LCD screen to show the counting result.

## Midpoint Demo

<div align=center>
<img src="https://github.com/ryanhpan/ESE5190-Final-Project/blob/main/diagram/moving%20counter%20demo.gif" width="600">  
</div>

### Moving state

<div align=center>
<img src="https://github.com/ryanhpan/ESE5190-Final-Project/blob/main/diagram/moving%20state.png" width="800">  
</div>

### Stopping state

<div align=center>
<img src="https://github.com/ryanhpan/ESE5190-Final-Project/blob/main/diagram/stopping%20state.png" width="800">  
</div>

# Troubleshooting

- [Logs](https://github.com/ryanhpan/ESE5190-Final-Project/blob/main/media/troubleshooting/notes.txt)

# Reflections

## Advantages/Disadvantages
Advantages:
1. The project does not need any peripheral equipment, it is cheap and light.
2. The project is sensitive to the state when the chip is integrated in a sports bracelet, in such case the walking detection is accurate.
3. A LCD screen is used to show the step information, it is very intuitive for user to see how many steps they walked in a day.

Disadvantage:
1.The algorithm is not sophisticated enough, it's defination on "one step" is rely on the relative position of the IMU chip. Nowadays, most step counter are integrated in the cell phone, which normally stays in the pocket when users are walking. Our algorithm can't handle that situation yet.
2. Even if users use our program on a sport bracelet, the algorithm still can't tell the difference between randomly waving the hand and actually walking, which may cause false count.
## Recommendation to future teams
Base on the disadvantage we listed above, it's obvious that only the acceleration and gravity data is not enough to define a step precisely. We will need more data to do that, such as the idea we couldn't realize due the limit of time, the positsion location. Also, there are still a lot of room for the algorithm to imporve. A machanic is required to find out what is the state now for the user. For example, if user sitting in a car, when the car moves, the acceleration and position data of the IMU will both change and that is definitely not a step. What's more, a data filter is also required to filter out those unormal shaking like shaking the equipment very fast on purpose, the step counting should not be increased. A filter is required to prevent that happen.

## Other design approaches/components we might try next time
If there is a chance in the future, we might try to refer to the latest algorithm and see how do they figure out all the problem we have above and we might try to used the wifi module to get the time and weather data to display on the LCD screen, so that it looks more like a sports bracelet.
# Feature/Accomplishment we found particularly satisfying
Successfully detect the moving state of the IMU module and turn that into walking state. When treat it like a bracelet, the step counting actually works!
# An explanation of the PIO part of the code

## The diagram of the overal logic

## Introduction to the RP2040 PIO module

## What makes RP2040 a unique asset for a microcontroller

# Team overview
- [Hao Pan](https://github.com/ryanhpan)
- [Lihong Zhao](https://github.com/lihzhao14)
- [Xingjian Chen](https://github.com/AndYmeisterrrrr)


