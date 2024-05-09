# LoRaWAN-mightyBrick32
Everything you would like to know about LoRaWAN-mightyBrick32 board


### Measuring VBAT voltage
- Voltage divider is placed between VBAT and A3 as shown in figure 
- When USB and/or battery are connected the reading from A3 should be around 4.2V 
- When only battery is connected, then A3 will read the actual battery voltage.
- Below sample code helps you to read the correct battery voltage.

```c
  // the setup function runs once when you press reset or power the board
  void setup()
  {
    SerialUSB.begin(115200);
    pinMode(A3, INPUT);
    analogReference(AR_DEFAULT); // Use the default reference voltage 3.3V
  }

  // the loop function runs over and over again forever
  void loop()
  {
    float vin = analogRead (A3) * 4.63 * 0.0008056 ; // 0.0008056 = 3.3 / 4096
    SerialUSB.println(vin);
    delay(2000); // wait for a second
  }
```

![alt text](https://github.com/[username]/[reponame]/blob/[branch]/image.jpg?raw=true)
