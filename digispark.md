# DigiSpark
### Installation
- Downlaod Arduino IDE from https://www.arduino.cc/en/software
- Go to File > Preferences > Additional boards manager URLs and add
```bash
https://raw.githubusercontent.com/ArminJo/DigistumpArduino/master/package_digistump_index.json
```
- Go to Tools > Board > Boards Managers and install Digistump AVR Boards
- Go to Tools > Board > Digistump AVR Boards and select Digispark
- Clock: 16.5 MHz
- Programmer: micronucleous
- Download and install Digispark windows driver from `https://content.instructables.com/F69/H6DH/JSCG6VKM/F69H6DHJSCG6VKM.zip`

### Codes
- Mouse mover
```c
// Digispark Mouse Jiggler
// Written by James Franklin for Air-Gap in 2019
// www.air-gap.com.au

#include <DigiMouse.h>
unsigned int LowerCycleTime = 10000; //Minimum Time in milli-seconds between each mouse action  Default: 10000 (10 Seconds), Max 65535ms
unsigned int UpperCycleTime = 30000; //Maximum Time in milli-seconds between each mouse action  Default: 30000 (30 Seconds), Max 65535ms
//Random Function will randomly execute a mouse move between these two values
void setup() {
  randomSeed(analogRead(0));  //Random Seed off background noise on analog pin
  pinMode(1, OUTPUT);
  DigiMouse.begin(); //start

}
void loop() {
//Moves mouse 1 pixel in a direction (up/down/left/right) in a square

  digitalWrite(1, HIGH);
  DigiMouse.moveY(100);
  DigiMouse.delay(50);
  digitalWrite(1, LOW);
  DigiMouse.delay(random(LowerCycleTime, UpperCycleTime));

  digitalWrite(1, HIGH);
  DigiMouse.moveX(100); //
  DigiMouse.delay(50);
  digitalWrite(1, LOW);
  DigiMouse.delay(random(LowerCycleTime, UpperCycleTime));

  digitalWrite(1, HIGH);
  DigiMouse.moveY(-100);
  DigiMouse.delay(50);
  digitalWrite(1, LOW);
  DigiMouse.delay(random(LowerCycleTime, UpperCycleTime));

  digitalWrite(1, HIGH);
  DigiMouse.moveX(-100);
   DigiMouse.delay(50);
  digitalWrite(1, LOW);
  DigiMouse.delay(random(LowerCycleTime, UpperCycleTime));
}
```

### Upload
- Compile the code via Sketch > Verify/Compile
- Upload the code via Sketch > Upload
- Wait for this message `Plug in Device Now..(will timeout in 60 seconds)`
- Now connect the Digispark board to USB port


### To Do
- Disabling Windows Security settings for "Real-Time Monitoring"
- Bypassing UAC
- Launching a admin command prompt, and passing commands to the prompt to download the payload
- Add exclusions in virus and security for the payload
- Attempts to further disarm Windows
- Schedule start our payload

# Resource
- https://medium.com/learning-cybersecurity/stealing-wifi-passwords-with-digispark-powershell-48fba82a13a
- https://www.vesiluoma.com/exploiting-with-badusb-meterpreter-digispark/
