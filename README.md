# Flightsim-Throttle-5-axis

I am not the author of the sketch i just simply modified it to my nmeeds and figured to put it here incase someone has ther smae needs as i do.

Will need to have joystick.h and servo.h library
- joystick.h https://github.com/MHeironimus/ArduinoJoystickLibrary
- servo.h can be downloaded form arduino IDE

Parts List
- 3 10k linear potentiometer w/ PCB
- 1 10k 45mm linear potentiometer
- 1 10k rotory potentiometer
- 1 10uf 16v cap
- 1 analog servo
- ATmega 32u4 board (such as arduino learnado or mini learnado, adafruit itsy bitsy worked too but didnt get it to workk 100% becase some conflicts with the pin numbering and i didnt bother much to tink with 

Wiring
- the two fixed ends of the potentiometer goes to negative and positive of 5v and the variable pin will be connected to the analog pins, along with the servo + - and signal to analog pin
   - on a generic board they are pin A0-A3 4, 6, 8, 9, & 10 (ones marked in green on the picture below)![71iUKrFHB6L](https://user-images.githubusercontent.com/84696624/217468709-904b629a-af88-478e-9247-0284d385aec6.jpg)

Code
- if not using the same pins as i did please refewr to a pinpot of the board and change the numbers according instead of usinmg A0 using A9
change
```
int axisLimits0[] = {0, 1023}; | to int axisLimits9[] = {0, 1023}; 
```
```
bool a0Used = true; | to  bool a9Used = true; 
```
```
if(a0Used) pinMode(A0, INPUT); |to  if(a9Used) pinMode(A9, INPUT); 
```
```
if(a0Used){
    value = analogRead(A0);
    pos   = translateValue(value, axisLimits0[0], axisLimits0[1]);
    Joystick.setThrottle(pos);
    if(setting == 0) settingPrint(value, pos);

to
    
 > if(a9Used){
    value = analogRead(A9);
    pos   = translateValue(value, axisLimits9[0], axisLimits0[1]);
    Joystick.setThrottle(pos);
     if(setting == 0) settingPrint(value, pos);
 ```
 
 If no use for the servo and want to remove it remove the following from the sketch
 ```
 #include <Servo.h>
 
 Servo trim;
 
 trim.attach(8); 

  void loop() {
    val = analogRead(potpin);            // reads the value of the potentiometer (value between 0 and 1023)
    val = map(val, 1023, 0, 0, 35);     // scale it to use it with the servo (value between 0 and 180)
    trim.write(val);                  // sets the servo position according to the scaled value
    delay(5);                           // waits for the servo to get there
 ```

 
