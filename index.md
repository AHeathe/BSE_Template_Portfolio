# Floor Cleaning Robot
I was working on an Arduino based floor cleaning robot with an Echo Sensor (HC-SR04) and an Arduino Shield.

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Amritpaul L. | Leland Highschool | Mechanical Engineering | Incoming Junior

![Headstone Image](https://bluestampengineering.com/wp-content/uploads/2016/05/improve.jpg)
 ![Echo Sensor]! (https://www.elementzonline.com/image/data/BLOG/USBlogimg.jpg)
  

# Final Milestone
My final milestone is me fixing this major issue. My car would only move forwards and not listen to any other functions. This was due to the lack of use of the ENA and ENB pins so i needed to wire them up. Then I realized I need a stronger battery source and 2 of them, one for my Arduino to power that up and one for my Arduino Sheild to power the motors and the shield. Therefore, I used 2 9V batteries. I tried swapping them out for 6V batteries and 5V batteries but they did not work so I had to continue using the 9V Batteries.

[![Milestone 3](https://res.cloudinary.com/marcomontalbano/image/upload/v1660235656/video_to_markdown/images/youtube--dGzlDxW8ur0-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://youtu.be/dGzlDxW8ur0 "Milestone 3")

# Second Milestone
My second mileston involved using the arduino shield to allow the motor to run forwards and backwards and giving the motors restrictions. Since I had only 2 motors and 2 wheels instead of 4. It was easier to setup than if it was a 4 wheeled car because then there would have been more variables in the code. I wired the motor to the shield and the shield to the arduino and tested it to make sure the motors were working. Then, I connected 5V to the 5V on the shield and the (-) side to the GRND pin.

[![Milestone 2](https://res.cloudinary.com/marcomontalbano/image/upload/v1660064085/video_to_markdown/images/youtube--vta6Ggo7jCI-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://youtu.be/vta6Ggo7jCI "Milestone 2")

# First Milestone
My first milestone was setting up the car Chasis, screwing in the motor to the frame. Then setting upp the echo sensor on the bread board and giving it input, output functions so it could do its job of using echolocation to find if there is an object in front of the sensor. Then I wired the arduino to and from the Echo sensor on the breadboard and wrote the code involving echolocation. The main issue I had with the echo sensor was the code because I did not know the distance formula but setting up the echo sensor to read distance from an object was rather straight forward. 

[![Milestone 1](https://res.cloudinary.com/marcomontalbano/image/upload/v1659979415/video_to_markdown/images/youtube--abd1UoVswN4-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://youtu.be/abd1UoVswN4 "Milestone 1")

# Bill of Materials
| First Header  |
| ------------- |
| Echo Sensor (HC-SR04)  |
| Wires  | 

| Echo Sensor (HC-SR04) |
| Wires |
| Alligator Clips |
| BreadBoard |
| Brush |
| Car Chasis (With Motor and Wheels) |

# Code

```

const int trigPin = 4;
const int echoPin = 2;

long duration; // variable for the duration of sound wave travel
int distance; // variable for the distance measurement

int motor1Ena = 11;
int motor1pin1 = 10;
int motor1pin2 = 9;


int motor2pin1 = 6;
int motor2pin2 = 5;
int motor2Ena = 3;

template <typename T>
Print& operator<<(Print& printer, T value)
{
    printer.print(value);
    return printer;
}

void setup() {
  Serial.begin(9600);
  pinMode(trigPin, OUTPUT); // Sets the trigPin as an OUTPUT
  pinMode(echoPin, INPUT); // Sets the echoPin as an INPUT
  Serial.println("Ultrasonic Sensor HC-SR04 Test"); // print some text in Serial Monitor
  Serial.println("with Arduino UNO R3");

  pinMode(motor1pin1, OUTPUT);
  pinMode(motor1pin2, OUTPUT);
  pinMode(motor2pin1, OUTPUT);
  pinMode(motor2pin2, OUTPUT);
  pinMode(motor1Ena, OUTPUT);  
  pinMode(motor2Ena, OUTPUT);
  //Initialize all to be low.
  digitalWrite(motor1pin1, LOW);
  digitalWrite(motor1pin2, LOW);
  digitalWrite(motor2pin1, LOW);
  digitalWrite(motor2pin2, LOW);
}

void loop() {
  // Clears the trigPin condition
  //Pulse with Echo. 10 microsecond pulse with trigPin.
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  // Sets the trigPin HIGH (ACTIVE) for 10 microseconds
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  // Reads the echoPin, returns the sound wave travel time in microseconds
  duration = pulseIn(echoPin, HIGH);
  // Calculating the distance
  distance = (duration * 0.0343) / 2; // Speed of sound wave divided by 2 (go and back)
  // Displays the distance on the Serial Monitor
  Serial << "Distance is: " << distance << "cm.\n";

  //if the distance is <=5 go backwards
  if  (distance <= 5){
    backwards();
    delay(2000);
  }
  else if (distance > 5 && distance < 20){
    left();
    delay(5000);
  }
  else{
    forward();
    delay(5000);
  }
}

void forward() {
  Serial.println("Going Forward");
  analogWrite(motor1Ena, 255);
  analogWrite(motor2Ena, 255);
  digitalWrite(motor1pin1, LOW);
  digitalWrite(motor1pin2, HIGH);
  digitalWrite(motor2pin1, LOW);
  digitalWrite(motor2pin2, HIGH);
}

//Make a forward, stop, backwards, left, right, and if statement with those things. add delays in the if statement. 

void StopMotors() {
  Serial.println("Stopping Motors...");
  //stop all functions
  digitalWrite(motor1pin1, LOW);
  digitalWrite(motor1pin2, LOW);
  digitalWrite(motor2pin1, LOW);
  digitalWrite(motor2pin2, LOW);
}

void backwards() {
  Serial.println("Driving Backwards....");
  analogWrite(motor1Ena, 255);
  analogWrite(motor2Ena, 255);
  
  digitalWrite(motor1pin1, HIGH);
  digitalWrite(motor1pin2, LOW);
  digitalWrite(motor2pin1, HIGH);
  digitalWrite(motor2pin2, LOW);
}

void left() {
  Serial.println("Turning Left....");
  analogWrite(motor1Ena, 255);
  analogWrite(motor2Ena, 255);
  digitalWrite(motor1pin1, HIGH);
  digitalWrite(motor1pin2, LOW);
  
  digitalWrite(motor2pin1, LOW);
  digitalWrite(motor2pin2, HIGH);
}


void right() {
  Serial.println("Turning Right....");
  analogWrite(motor1Ena, 255);
  analogWrite(motor2Ena, 255);
  digitalWrite(motor1pin1, LOW);
  digitalWrite(motor1pin2, HIGH);
  
  digitalWrite(motor2pin1, HIGH);
  digitalWrite(motor2pin2, LOW);
}

```
