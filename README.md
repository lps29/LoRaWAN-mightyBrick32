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
    Serial.begin(115200);
    pinMode(A3, INPUT);
  }

  // the loop function runs over and over again forever
  void loop()
  {
    float vin = analogRead (A3) * 2 * 0.003226; // 0.003226 = 3.3 / 1023
    Serial.println(vin);
    delay(2000); // wait for a second
  }
```

![alt text](https://github.com/[username]/[reponame]/blob/[branch]/image.jpg?raw=true)
