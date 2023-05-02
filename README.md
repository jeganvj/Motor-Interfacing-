# MOTOR INTERFACING
## AIM:
To control the motor using driver circuits, relays and Arduino UNO controller.
## Software required:
Arduino IDE </br>
Proteous
## PROCEDURE:
### Arduino IDE
Step1:Open the Arduino IDE </br>
Step2: Go to file and select new file option </br>
Step3:Type the program </br>
Step4:Go to file and select save option to save the program </br>
Step5:Go to sketch and select verify or compile options </br>
Step6:If no error Hex file will be generated in the temporary folder </br>
### Proteus
Step7:Open the Proteus software </br>
Step8:Go to file select new design and click ok button </br>
Step9:Select component mode and click pick devices from the library </br>
Step10:Type the component name in the keyword to select the components and click ok button </br>
Step11:Design the circuit as per the diagram </br>
Step12:Double click the Arduino controller and upload the hex file generated by Arduino IDE </br>
Step13:Click start button and check the output
## THEORY:

We can control the speed of the DC motor by simply controlling the input voltage to the motor and the most common method of doing that is by using PWM signal.

![image](https://user-images.githubusercontent.com/71547910/235333428-6ea2d3a7-3e8d-4b5d-a7cc-9fa19a3e5a91.png)

### PWM DC Motor Control

PWM, or pulse width modulation is a technique which allows us to adjust the average value of the voltage that’s going to the electronic device by turning on and off the power at a fast rate. The average voltage depends on the duty cycle, or the amount of time the signal is ON versus the amount of time the signal is OFF in a single period of time.

![image](https://user-images.githubusercontent.com/71547910/235333450-351b851a-9b23-43fb-bec4-ad9a779e4fcf.png)

So depending on the size of the motor, we can simply connect an Arduino PWM output to the base of transistor or the gate of a MOSFET and control the speed of the motor by controlling the PWM output. The low power Arduino PWM signal switches on and off the gate at the MOSFET through which the high power motor is driven.

### H-Bridge DC Motor Control

On the other hand, for controlling the rotation direction, we just need to inverse the direction of the current flow through the motor, and the most common method of doing that is by using an H-Bridge. An H-Bridge circuit contains four switching elements, transistors or MOSFETs, with the motor at the center forming an H-like configuration. By activating two particular switches at the same time we can change the direction of the current flow, thus change the rotation direction of the motor.

![image](https://user-images.githubusercontent.com/71547910/235333489-ff173dfb-e8e7-46a5-ba81-40207c97b842.png)

So if we combine these two methods, the PWM and the H-Bridge, we can have a complete control over the DC motor. There are many DC motor drivers that have these features and the L298N is one of them.

### L298N Driver

The L298N is a dual H-Bridge motor driver which allows speed and direction control of two DC motors at the same time. The module can drive DC motors that have voltages between 5 and 35V, with a peak current up to 2A.Let’s take a closer look at the pinout of L298N module and explain how it works. The module has two screw terminal blocks for the motor A and B, and another screw terminal block for the Ground pin, the VCC for motor and a 5V pin which can either be an input or output.This depends on the voltage used at the motors VCC. The module have an onboard 5V regulator which is either enabled or disabled using a jumper. If the motor supply voltage is up to 12V we can enable the 5V regulator and the 5V pin can be used as output, for example for powering our Arduino board. But if the motor voltage is greater than 12V we must disconnect the jumper because those voltages will cause damage to the onboard 5V regulator. In this case the 5V pin will be used as input as we need connect it to a 5V power supply in order the IC to work properly.We can note here that this IC makes a voltage drop of about 2V. So for example, if we use a 12V power supply, the voltage at motors terminals will be about 10V, which means that we won’t be able to get the maximum speed out of our 12V DC motor.

![image](https://user-images.githubusercontent.com/71547910/235333546-0cfa7d3a-24a4-483b-bbef-b78fcaa05670.png)





## PROGRAM:
int directionPin = 12; </br>
int pwmPin = 3; </br>
int brakePin = 9;</br>
 
 bool directionState; </br>
 void setup() {</br>
 //define pins</br>
 pinMode(directionPin, OUTPUT); </br>
 pinMode(pwmPin, OUTPUT); </br>
 pinMode(brakePin, OUTPUT); </br>
 }</br>
 void loop() {</br>
 //change direction every loop()</br>
 directionState = !directionState; </br>
 //write a low state to the direction pin (13)</br>
 if(directionState == false){</br>
 digitalWrite(directionPin, LOW);</br>
 }</br>
 //write a high state to the direction pin (13)</br>
 else{ </br>
 digitalWrite(directionPin, HIGH);</br> 
 }</br>
 //release breaks</br>
 digitalWrite(brakePin, LOW);</br>
 //set work duty for the motor</br>
 analogWrite(pwmPin, 30);</br>
 delay(2000); </br>
 //activate breaks </br>
 digitalWrite(brakePin, HIGH);</br>
 //set work duty for the motor to 0 (off)</br>
 analogWrite(pwmPin, 0);</br>
 delay(2000);</br>
}</br>
## CIRCUIT DIAGRAM:
![image](https://user-images.githubusercontent.com/132323363/235739034-418d95f1-30e9-453b-8ff4-455225915a9e.png)

## OUTPUT:
![image](https://user-images.githubusercontent.com/132323363/235738959-3cd44624-4acd-462c-b298-3794e1ef7f6a.png)

## RESULT:
Thus the motor was controlled using driver circuits, relays and Arduino UNO controller.
