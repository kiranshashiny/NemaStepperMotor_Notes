# NemaStepperMotor_Notes
Notes


The Nema stepper motor that is being used for CNC is :

![image](https://user-images.githubusercontent.com/14288989/188083115-6537f30e-6310-424b-950b-b32c64001d98.png)

CNC shield being used :

![image](https://user-images.githubusercontent.com/14288989/188083216-a9dd6614-892c-40bf-a0bb-554cce073b06.png)


The CNC shield is mounted on the Arduino Uno .

How to debug :

- No external 5v is required for the CNC shield.
- Using Multimeter check the 5v on the CNC shield and the 5v of the back side of the Arduino.
- 

How to set the current limit on the motor driver ( or else it will get hot )

![image](https://user-images.githubusercontent.com/14288989/188088698-4f55f1b7-f5e7-44a2-9167-d831aa1504f9.png)

Hold the Multimeter GND and the pot on the driver to check the current.

A typical example would be ( 0.9 X 8 X 0.068 = 0.48A )

Imot = Maximum motor current

Rsen = current sensing resistance.

( to be continued )

https://www.youtube.com/watch?v=OpaUwWouyE0&t=30s



![image](https://user-images.githubusercontent.com/14288989/188097567-2a6541df-89ad-4eab-af8c-96838bdac420.png)


[17pm-k3.pdf](https://github.com/kiranshashiny/NemaStepperMotor_Notes/files/9476282/17pm-k3.pdf)

--

[17PM-K016V-NMB.pdf](https://github.com/kiranshashiny/NemaStepperMotor_Notes/files/9477678/17PM-K016V-NMB.pdf)

![image](https://user-images.githubusercontent.com/14288989/188138933-3c5fe443-2ca6-4faa-9da9-9b53e374a10f.png)




https://www.mpja.com/Stepper-Motor-NEMA-17-24V-18Deg-Minebea-USED/productinfo/30235%20MS/



## Why stepper gets too hot !

![image](https://user-images.githubusercontent.com/14288989/188450186-dd2d4cb5-3fd1-4724-996e-8ab604bcf887.png)

## Link to a German Arduino Nema 17 

https://starthardware.org/arduino-a4988-nema17/

![image](https://user-images.githubusercontent.com/14288989/188457192-a47b2c38-1d4f-4a03-9cae-8d584f62ec36.png)

##. When it started working without the CNC shield.
This was connected to a bread board.


The code is as follows:

```
// Define pin connections & motor's steps per revolution
const int dirPin  = 3;
const int stepPin = 6;
const int stepsPerRevolution = 200;

void setup()
{
  // Declare pins as Outputs
  pinMode(stepPin, OUTPUT);
  pinMode(dirPin, OUTPUT);
}
void loop()
{
  // Set motor direction clockwise
  digitalWrite(dirPin, HIGH);

  // Spin motor slowly
  for(int x = 0; x < stepsPerRevolution; x++)
  {
    digitalWrite(stepPin, HIGH);
    delayMicroseconds(2000);
    digitalWrite(stepPin, LOW);
    delayMicroseconds(2000);
  }
  delay(1000); // Wait a second
  
  // Set motor direction counterclockwise
  digitalWrite(dirPin, LOW);

  // Spin motor quickly
  for(int x = 0; x < stepsPerRevolution; x++)
  {
    digitalWrite(stepPin, HIGH);
    delayMicroseconds(1000);
    digitalWrite(stepPin, LOW);
    delayMicroseconds(1000);
  }
  delay(1000); // Wait a second
}

```

## connections are as follows 

```
Step = 6
Dir = 3
2b and 2a are connected to one pair
1a and 1b are connected to second pair
Reset and Sleep are interconnected
Vmot is connected to 12v

GND is connected to Arduino's GND.

Vdd is connected to Arduino's 5v
GND is connected to Arduino's GND as well.
```


## Vref 

Vref was found to be 0.39v ( the casing is not heating up ! )


## To make the movement fast.
Slow makes it noisy.

```
// Spin motor quickly.. This is noiseless !
  for(int x = 0; x < stepsPerRevolution; x++)
  {
    digitalWrite(stepPin, HIGH);
    delayMicroseconds(1000);
    digitalWrite(stepPin, LOW);
    delayMicroseconds(1000);
  }
  delay(1000); // Wait a second
```

## To make continuous movement - one direction

// Spin motor slowly
  for(int x = 0; x < stepsPerRevolution; x++)
  {
    digitalWrite(stepPin, HIGH);
    delayMicroseconds(1000);
    digitalWrite(stepPin, LOW);
    delayMicroseconds(1000);
  }




![image](https://user-images.githubusercontent.com/14288989/189081552-d6c66c30-261d-4871-8f94-2847919a68fe.png)


