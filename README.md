# HOLA Innovation Kit Workshop 1: Wrist Watch
## 1. Run Factory Test  
Turn on M5StickC using button on left. You should see a cube that rotates when you rotate the device. If you see battery error 22, charge the device by attaching the device to your USB port for a few minutes and then try again.
## 2. Install Arduino IDE  
Download latest Arduino IDE from https://www.arduino.cc/
## 3. Add M5StickC Board Support  
Follow Boards Manager stick section from https://docs.m5stack.com/#/en/arduino/arduino_development?id=boards-manager and "For M5StickC" section for last step.
## 4. Add M5StickC Library  
Follow M5Stack Library section from https://docs.m5stack.com/#/en/arduino/arduino_development?id=m5stack-library and "For M5StickC" section for last step.
## 5. Get a blank screen
Add the following code to the Arduino code window and click the arrow icon for upload. If you get a connection error try changing the COM port in Tools>Port
```C
#include <M5StickC.h>

void setup() {
  // put your setup code here, to run once:
  M5.begin();
  M5.Lcd.setRotation(3);
  M5.Lcd.fillScreen(BLACK);

}

void loop() {
  // put your main code here, to run repeatedly:

}
```
## 6. Add some text
```C
#include <M5StickC.h>

void setup() {
  // put your setup code here, to run once:
  M5.begin();
  M5.Lcd.setRotation(3);
  M5.Lcd.fillScreen(BLACK);
  
  M5.Lcd.printf("Hello, World");
}

void loop() {
  // put your main code here, to run repeatedly:

}
```
## 6. Change text to a time
```C
#include <M5StickC.h>

void setup() {
  // put your setup code here, to run once:
  M5.begin();
  M5.Lcd.setRotation(3);
  M5.Lcd.fillScreen(BLACK);
  
  M5.Lcd.printf("12:55:00");
}

void loop() {
  // put your main code here, to run repeatedly:

}
```
