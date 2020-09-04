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
## 7. Change text to a time
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
## 8. Make text bigger
```C
#include <M5StickC.h>

void setup() {
  // put your setup code here, to run once:
  M5.begin();
  M5.Lcd.setRotation(3);
  M5.Lcd.fillScreen(BLACK);
  
  M5.Lcd.setTextSize(3);
  
  M5.Lcd.printf("12:55:00");
}

void loop() {
  // put your main code here, to run repeatedly:

}
```
## 9. Center text
```C
#include <M5StickC.h>

void setup() {
  // put your setup code here, to run once:
  M5.begin();
  M5.Lcd.setRotation(3);
  M5.Lcd.fillScreen(BLACK);
  
  M5.Lcd.setTextSize(3);
  
  M5.Lcd.setCursor(6, 30);
  
  M5.Lcd.printf("12:55:00");
}

void loop() {
  // put your main code here, to run repeatedly:

}
```
## 10. Get time from Real Time Clock (RTC)
```C
#include <M5StickC.h>

RTC_TimeTypeDef RTC_TimeStruct;

void setup() {
  // put your setup code here, to run once:
  M5.begin();
  M5.Lcd.setRotation(3);
  M5.Lcd.fillScreen(BLACK);

  M5.Lcd.setTextSize(3);
  
  // Set inital time
  RTC_TimeTypeDef TimeStruct;
  TimeStruct.Hours   = 12;
  TimeStruct.Minutes = 55;
  TimeStruct.Seconds = 0;
  M5.Rtc.SetTime(&TimeStruct);
}

void loop() {
  // put your main code here, to run repeatedly:
  M5.Lcd.setCursor(6, 30);
  
  M5.Rtc.GetTime(&RTC_TimeStruct);
  M5.Lcd.setCursor(6, 30);
  M5.Lcd.printf("%02d:%02d:%02d\n",RTC_TimeStruct.Hours, RTC_TimeStruct.Minutes, RTC_TimeStruct.Seconds);

  delay(500);
}
```
## 11. Use right button to update hour  
```C
#include <M5StickC.h>

RTC_TimeTypeDef RTC_TimeStruct;

void setup() {
  // put your setup code here, to run once:
  M5.begin();
  M5.Lcd.setRotation(3);
  M5.Lcd.fillScreen(BLACK);

  M5.Lcd.setTextSize(3);
  
  // Set inital time
  RTC_TimeTypeDef TimeStruct;
  TimeStruct.Hours   = 12;
  TimeStruct.Minutes = 55;
  TimeStruct.Seconds = 0;
  M5.Rtc.SetTime(&TimeStruct);

  pinMode(M5_BUTTON_RST, INPUT);
}

void loop() {
  // put your main code here, to run repeatedly:
  if(digitalRead(M5_BUTTON_RST) == LOW)
  {
    RTC_TimeStruct.Seconds = 0;
    RTC_TimeStruct.Hours = (RTC_TimeStruct.Hours + 1)%24;
    M5.Rtc.SetTime(&RTC_TimeStruct);
  }
  
  M5.Lcd.setCursor(6, 30);
  
  M5.Rtc.GetTime(&RTC_TimeStruct);
  M5.Lcd.setCursor(6, 30);
  M5.Lcd.printf("%02d:%02d:%02d\n",RTC_TimeStruct.Hours, RTC_TimeStruct.Minutes, RTC_TimeStruct.Seconds);

  delay(500);
}
```
## 12. Use home button to update minutes
```C
#include <M5StickC.h>

RTC_TimeTypeDef RTC_TimeStruct;

void setup() {
  // put your setup code here, to run once:
  M5.begin();
  M5.Lcd.setRotation(3);
  M5.Lcd.fillScreen(BLACK);

  M5.Lcd.setTextSize(3);
  
  // Set inital time
  RTC_TimeTypeDef TimeStruct;
  TimeStruct.Hours   = 12;
  TimeStruct.Minutes = 55;
  TimeStruct.Seconds = 0;
  M5.Rtc.SetTime(&TimeStruct);

  pinMode(M5_BUTTON_RST, INPUT);
  pinMode(M5_BUTTON_HOME, INPUT);

}

void loop() {
  // put your main code here, to run repeatedly:
  if(digitalRead(M5_BUTTON_RST) == LOW)
  {
    RTC_TimeStruct.Seconds = 0;
    RTC_TimeStruct.Hours = (RTC_TimeStruct.Hours + 1)%24;
    M5.Rtc.SetTime(&RTC_TimeStruct);
  }
  if(digitalRead(M5_BUTTON_HOME) == LOW)
  {
    RTC_TimeStruct.Minutes++;
    RTC_TimeStruct.Seconds = 0;
    if ( RTC_TimeStruct.Minutes >= 60 )
    {
      RTC_TimeStruct.Minutes = 0;
      RTC_TimeStruct.Hours = (RTC_TimeStruct.Hours + 1)%24;
    }
    
    M5.Rtc.SetTime(&RTC_TimeStruct);
  }
  M5.Lcd.setCursor(6, 30);
  
  M5.Rtc.GetTime(&RTC_TimeStruct);
  M5.Lcd.setCursor(6, 30);
  M5.Lcd.printf("%02d:%02d:%02d\n",RTC_TimeStruct.Hours, RTC_TimeStruct.Minutes, RTC_TimeStruct.Seconds);

  delay(500);
}
```
## 13. Use IMU to set background color
```C
#include <M5StickC.h>

RTC_TimeTypeDef RTC_TimeStruct;

void setup() {
  // put your setup code here, to run once:
  M5.begin();
  M5.Lcd.setRotation(3);
  M5.Lcd.fillScreen(BLACK);

  M5.Lcd.setTextSize(3);
  
  // Set inital time
  RTC_TimeTypeDef TimeStruct;
  TimeStruct.Hours   = 12;
  TimeStruct.Minutes = 55;
  TimeStruct.Seconds = 0;
  M5.Rtc.SetTime(&TimeStruct);

  pinMode(M5_BUTTON_RST, INPUT);
  pinMode(M5_BUTTON_HOME, INPUT);

  M5.IMU.Init();
}

void loop() {
  // put your main code here, to run repeatedly:
  float accX = 0;
  float accY = 0;
  float accZ = 0;
  double theta = 0;
  
  M5.IMU.getAccelData(&accX, &accY, &accZ);
  if ((accX < 1) && (accX > -1))
  {
    theta = asin(-accX) * 57.295;
  }
  uint8_t color = ((theta+90.0f)/180.0f)*31;
  M5.Lcd.fillScreen(color);
  
  if(digitalRead(M5_BUTTON_RST) == LOW)
  {
    RTC_TimeStruct.Seconds = 0;
    RTC_TimeStruct.Hours = (RTC_TimeStruct.Hours + 1)%24;
    M5.Rtc.SetTime(&RTC_TimeStruct);
  }
  if(digitalRead(M5_BUTTON_HOME) == LOW)
  {
    RTC_TimeStruct.Minutes++;
    RTC_TimeStruct.Seconds = 0;
    if ( RTC_TimeStruct.Minutes >= 60 )
    {
      RTC_TimeStruct.Minutes = 0;
      RTC_TimeStruct.Hours = (RTC_TimeStruct.Hours + 1)%24;
    }
    
    M5.Rtc.SetTime(&RTC_TimeStruct);
  }
  M5.Lcd.setCursor(6, 30);
  
  M5.Rtc.GetTime(&RTC_TimeStruct);
  M5.Lcd.setCursor(6, 30);
  M5.Lcd.printf("%02d:%02d:%02d\n",RTC_TimeStruct.Hours, RTC_TimeStruct.Minutes, RTC_TimeStruct.Seconds);

  delay(500);
}
```

