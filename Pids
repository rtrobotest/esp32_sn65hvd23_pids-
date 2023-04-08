#include <Arduino.h>
#include <CAN.h>
#include <CAN_config.h>
#include <ESP32CAN.h>
#include <can_regdef.h>
 // include library
void setup() {

  CAN.setPins(4, 5);

  Serial.begin(115200); 
  // CAN controller board has 8 MHz crystal on-board
  // start the CAN controller with 500 kbps bitrate
  if (!CAN.begin(500e3)) {
    // failure
    Serial.println("CAN initilization failed!");
    while (1);
  }
}

void loop() {
  CAN.beginPacket(0x000, 8);
  CAN.write(0x00);         
  CAN.write(0x00);          
  CAN.write(0x00);
  CAN.write(0x00);
  CAN.write(0x00);
  CAN.write(0x00);
  CAN.write(0x00);
  CAN.write(0x00);         
  CAN.endPacket();

  CAN.beginPacket(0x000, 8);
  CAN.write(0x00);           
  CAN.write(0x00);
  CAN.write(0x00);
  CAN.write(0x00);
  CAN.write(0x00);
  CAN.write(0x00);
  CAN.write(0x00);
  CAN.write(0x00);
  CAN.endPacket();
  // wait for response
  while (CAN.parsePacket() == 0 ||
         CAN.read() !=  ||         // correct length
         CAN.read() != 0x00 ||      // correct mode
         CAN.read() != 0x00);       // correct PID
  // engine RPM = (A * 256 + B) / 4
  float vin = ((CAN.read() * 256.0) + CAN.read()) / 4.0; //calculation
  Serial.print("vin = ");
  Serial.println(vin);
  // ...
  delay(100);
}
