# LoRaWAN-mightyBrick32
Everything you would like to know about LoRaWAN-mightyBrick32 board


### Measuring VBAT voltage
- Voltage divider is placed between VBAT and A3 as shown in figure 
- When USB and battery are connected the reading from A3 is the charging voltage. 
- When only battery is connected, then A3 will read the actual battery voltage.
- Below sample code helps you to read the correct battery voltage.

```c
  // the setup function runs once when you press reset or power the board
  void setup()
  {
    SerialUSB.begin(115200);
    pinMode(A3, INPUT);
    analogReference(AR_DEFAULT); // Make sure to use the default reference voltage 3.3V
    //analogReadResolution(12); // Default resolution is 10bit, use this for 12-bit resolution  
  }

  // the loop function runs over and over again forever
  void loop()
  {
    //float vin = analogRead(A3) * 1.275 * 0.0008056 ; // For 12-bit resolution, 0.0008056 = 3.3 / 4096
    float vin = analogRead(A3) * 1.275 * 0.0032226 ; // For 10-bit resolution, 0.0032226 = 3.3 / 1024
    SerialUSB.println(vin);
    delay(2000); // wait for a second
  }
```

![alt text](https://github.com/[username]/[reponame]/blob/[branch]/image.jpg?raw=true)
