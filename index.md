# Solar Panel Sun Tracker - Phone Charger
Hi, I’m Ryan! The project that I chose is a solar panel sun tracker that uses a servo motor, photo-resistors, and of course a solar panel! This device tracks the movement of sun light allowing the solar panel to receive the maximum amount of sunlight to power a phone.

# About the Creator
Ever since I was little, I would tell my family that I wanted to become an engineer. There is even a quote of me saying that I wanted to become an engineer in my 5th grade yearbook. Although I knew I wanted to become an engineer, I never knew what type. Now in the BlueStamp Engineering Program I am exploring the variety of types of engineering, with the project I am working on.

<p align="center">
<a href="https://imgbb.com/"><img src="https://i.ibb.co/gvccW8z/IMG-5550-1.jpg" alt="IMG-5550-1" border="0"></a><br />
</p>

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Ryan | Northgate High School | Mechanical & Aerospace Engineering | Rising Senior
  
# Presentation Slideshow
This is the slideshow I used to present the Solar Panel Sun Tracker - Phone Charger.

<p align="center">
<iframe src="https://docs.google.com/presentation/d/e/2PACX-1vQ8x8O78KRGT-Bokg8Eo5ipKljwuH8d0-_Mzq7ZLjuAsKDVwWc2uPLVzLa6ELQA01R6Wf9tAiwhJDnx/embed?start=false&loop=false&delayms=3000" frameborder="0" frameborder="0" width="760" height="369" allowfullscreen="true" mozallowfullscreen="true" webkitallowfullscreen="true"></iframe>
</p>

# Final Milestone
My final milestone was to replace the original servo motor with a stronger servo motor so it would be able to tilt the solar panel. I took off the original servo motor and hot glued and taped the stronger servo motor. Next, I attached the servo motor to the solar panel with a bent paper clip. During this time, I also tested the entire device to make sure it was working correctly. Unfortunately, the servo motor would only rotate to the right when it was intended to rotate both left and right. I looked at the entire device to see if there was anything physically wrong, but saw nothing, so I looked at the code. With the help of my mentor, I was able to fix the bug in the code, allowing the servo motor to spin left and right with only a few changes in the code.

[![Final Milestone](https://res.cloudinary.com/marcomontalbano/image/upload/v1660086697/video_to_markdown/images/youtube--ifvLpzCMu4I-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://www.youtube.com/watch?v=ifvLpzCMu4I "Final Milestone"){:target="_blank" rel="noopener"}

# Second Milestone
The construction of the device's overall structure was my second milestone. I began by using cardboard to build the structure. I then made the necessary cuts in the cardboard to make the base for the entire structure, two columns, and another base for the solar panel. Next, I hot glued the two columns next to the base after adding the components from milestone 1 to it. On both columns, symmetrical perforations were then drilled, which would subsequently be used for the solar panels' range of motion. The solar panel was then hot glued to the smaller base, and the ends of two binder clips were inserted on the left and right. Inserting the ends of a binder clip and the holes at the side of each column allowed me to feed string and tie all the pieces together. These steps allowed the solar panel to have a range of motion.

[![Milestone 2](https://res.cloudinary.com/marcomontalbano/image/upload/v1659733180/video_to_markdown/images/youtube--GMWZ74NauQs-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://www.youtube.com/watch?v=GMWZ74NauQs "Milestone 2"){:target="_blank" rel="noopener"}

# First Milestone
My first milestone was getting the servo motor and the photo-resistors to correspond with each other. To begin this project I familiarized myself with the tools I was using, as it was my first time ever building something mechanical with computer science. Next, I assembled the basic structure of my device using: multiple wires, servo motor, photo-resistors, arduino board, breadboard, and 4 band resistors. After assembling, I implemented the code on to the arduino board using my computer. Unfortunatly, I ran into a problem, the servo motor was not calibrated correctly. When I input a certain amount of rotation, for example 90 degrees, the servo motor would begin to constantly spin. To fix this I made sure that all the wires were firmly connected, made sure the code was correct, and through some troubleshooting, I was able to get the servo motor to work correctly. Now when more light is detected on one photo-resistor, the servo motor will move accordingly until both photo-resistors detect equal amount of light.

[![Milestone 1](https://res.cloudinary.com/marcomontalbano/image/upload/v1659481958/video_to_markdown/images/youtube--cIgtUEMW-1w-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://www.youtube.com/watch?v=cIgtUEMW-1w "Milestone 1"){:target="_blank" rel="noopener"}

# Bill of Materials 

This table contains all the items needed to recreate the project. It contains the item, quanitity, price and where to buy the item.  

# Solar Panel Sun Tracker - Phone Charger Code

Below is the code I used to make the project operational. The code is through arduino and the photo-resistors detect the amount of light which can be seen in the serial monitor and depending on the amount of light one photo-resistor receives the servo motor will move toward that direction.

``` 
//Sun Tracker Sketch 

#include <Servo.h>

Servo servo;   // Create a servo object to control the servo
int eLDRPin = A0; // Assign pins to the LDR's
int wLDRPin = A1;
int eastLDR = 0; //Create variables to store to LDR readings
int westLDR = 0;
int difference = 0; //Create a variable to compare the two LDR's
int error = 10;  // Variable for is there is a noticable difference between the tow LDR's
int servoSet = 10; //Variable for position of servo - will be different for each device


void setup() {
  servo.attach(9);   //attaches the servo object to PWM pin 9
  Serial.begin(9600); 
}

void loop() {
  eastLDR = analogRead(eLDRPin); //Read the LDR values
  westLDR = analogRead(wLDRPin);

  if (eastLDR < 400 && westLDR < 400) {  //Check to see if there is low light on both LDR's
    while (servoSet <=100 && servoSet >=15) {     // if so, send panels back to east for the sunrise
      servoSet ++;
      servo.write(servoSet);
      delay(100);
    }
  }

  difference = westLDR - eastLDR ; //Check the difference 
  if (difference > 10) {  //Send the panel towards the LDR with a higher reading
    Serial.println(servoSet);
    if (servoSet <= 150) {
      servoSet ++;
      Serial.println(servoSet);
      servo.write(servoSet);
    }
  } else if (difference < -10) {
    if (servoSet >= 15) {
      servoSet --;
      servo.write(servoSet);
    }
  } 
  
  Serial.print(eastLDR);      //Serial monitor can be useful for debugging/setting up
  Serial.print("   -   ");    //Use it to see if your LDR's are noticeably different when
  Serial.print(westLDR);      //They have equal light shining on them, if so, correct with the error value
  Serial.print("   -   ");
  Serial.print(difference);   
  Serial.print("   -   ");
  Serial.print(servoSet);     //Fine tune the servo settings, to maximise swing available
  Serial.print("   -   ");
  Serial.println(".");
  delay(100);
}
```
