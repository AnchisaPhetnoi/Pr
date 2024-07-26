# Arduino ESP8266 BLYNK IOT - ทดลอง Sensor DHT22 วัดอุณหภูมิ และ ความชื้นในอากาศ
### Sensor DHT22 วัดอุณหภูมิ และ ความชื้นในอากาศ เพราะ มีความระเอียดมากกว่า

### ผลลัพน์ ดังนี้
#### 1.แบบแรก
![451803876_1652633288891200_6952959525567965509_n](https://github.com/user-attachments/assets/bc51d661-40b1-4477-8998-909b52cd76b1)

### โค้ดโปรแกรมใส่ใน  Arduino
```cmd
// DHT Temperature & Humidity Sensor
// Unifid Sensor Library Example
// Written by Tony DiCola for Adafruit Industries
// Released under an MIT license.

// REQUIRES the following Arduino libraries:
// - DHT Sensor Library: https://github.com/adafruit/DHT-sensor-library
// - Adafruit Unified Sensor Lib: https://github.com/adafruit/Adafruit_Sensor

#include <Adafruit_Sensor.h>
#include <DHT.h>
#include <DHT_U.h>

#define DHTPIN D1  // Digital pin connected to the DHT sensor
// Feather HUZZAH ESP8266 note: use pins 3, 4, 5, 12, 13 or 14 --
// Pin 15 can work but DHT must be disconnected during program upload.


// Uncomment the type of sensor in use:
//#defin DHTTYPE DHT11 // DHT 11
#define DHTTYPE DHT22 // DHT 22 (AM2302)
//#define DHTTYPE DHT 21  // DHT 21 (AM2301)

// See guide for details on sensor wiring and usage:
//   https://learn.adafruit.com/dht/overview

```


### 2.แบบที่สอง
(![452219120_1163551618237156_1571524004272609197_n](https://github.com/user-attachments/assets/1af11e85-75c6-4918-b0b5-999a63ed4360)

### โค้ดโปรแกรมใส่ใน  Arduino






### การต่อ
![451742799_782779597265594_1270962989219594466_n](https://github.com/user-attachments/assets/9ae75156-0591-40be-89f2-4cd0db43850d)

### เซนเซอร์ที่ใช้วัด
![451208733_1201615957955922_2435783463726308154_n](https://github.com/user-attachments/assets/ae4fe5fd-3538-423f-87f8-4278f5a570fa)

![451442482_454058517464713_4823766014069100707_n](https://github.com/user-attachments/assets/b4f11f6d-0f1a-426a-962c-7394ae3babbf)

![451426076_492943826757353_570999236254261601_n](https://github.com/user-attachments/assets/bc78d6cb-64eb-4dff-9746-19424678a8f6)

![451430261_1448181175847072_963677684820988539_n](https://github.com/user-attachments/assets/33fee7b9-2f03-4368-9c8f-371627a6613e)

![451184617_821446120093530_7320758254414631433_n](https://github.com/user-attachments/assets/807599aa-8a26-40d7-945a-bd0086e9ce47)


### ไลบราลี้ ที่ใช้

![450909045_430751126631344_1940757051376448781_n](https://github.com/user-attachments/assets/fbb2c20e-b62d-463f-9211-6f04040923ba)


![450358665_414886868249042_6469617079530953669_n](https://github.com/user-attachments/assets/a17966ed-6e26-4b2f-a571-a988089da63b)

### มีสองตัว 
#### แต่ตัวสีแดงสามารถต่อเชื่อมได้เลยเพราะ มีการต่อ พูอัพรีสิทเตอร์มาให้แล้ว ในสีแดงๆ ด้านข้าง

![451418838_420623423645711_8938275803987425028_n](https://github.com/user-attachments/assets/3c1160a0-7b63-4f20-8c61-7fed15204e1e)

### ตัวสีขาว Sensor DHT22 มีความละเอียดกว่า DH11

![451440258_474883625258947_788138245912276795_n](https://github.com/user-attachments/assets/21283fb0-2ea7-41aa-b4d1-350b05547ebd)


### แบบนี้ไม่ต้องต่อพูอัพลีสิซเตอร์
![ภาพ](https://github.com/user-attachments/assets/88df54d5-941a-42e8-a1c6-47445f8b881d)


#### ไมโครคอนโทรนเลอร์คือ อะดูโน่ หรือ บอร์ดที่ใช้เชื่อมต่อการเขียนโปรแกรมและ Run โปรแกรม

### เอกสารที่ดูเพิ่มเติม ตามเว็บไซร์ในภาพ สำหรับการส่งสัยเรื่องการใช้งานยังไง
![ภาพ](https://github.com/user-attachments/assets/a07573b0-00cb-41b1-8a93-51949d1175ea)

### โปรโตคอที่ใช้งาน คือการเขียนโปรแกรมเพื่อดึง Data ให้มันนำมาใช้งาน อ่านค่าเซนเซอร์ ไปแสดงผลการวัดอุณหภูมิกับค่าเซนเซอร์
![ภาพ](https://github.com/user-attachments/assets/c97463b7-4a82-46c5-baf2-8dd99773e35f)

### ลงไลบรารี้
![ภาพ](https://github.com/user-attachments/assets/dc5fecc7-0e71-4813-993d-46c883d54de0)

### การใช้งาน
#### 1.ลองตัวแรก
![ภาพ](https://github.com/user-attachments/assets/8935d977-81d0-4fe0-9ebd-80355aeea48e)

![ภาพ](https://github.com/user-attachments/assets/d6627177-585f-41b4-981a-86b8551bee9f)



#### 2.ลองตัวสอง















