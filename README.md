# LoRaWAN-mightyBrick32
Everything you would like to know about LoRaWAN-mightyBrick32 board

### Blue LED
- The on-board blue LED is attached to pin `A4`, that can be used for debugging.
- If needed, a jumper is provided (labelled as L) to remove LED from the `A4` pin.
- Below is the sample code for LED blink.
  ```c
    void setup() 
    {
      // initialize digital pin LED_BUILTIN as an output.
      pinMode(LED_BUILTIN, OUTPUT); // A4 or 16 can also be used, instead of LED_BUILTIN, 
    }

    // the loop function runs over and over again forever
    void loop() 
    {
      digitalWrite(LED_BUILTIN, HIGH);  // turn the LED on (HIGH is the voltage level)
      delay(1000);                      // wait for a second
      digitalWrite(LED_BUILTIN, LOW);   // turn the LED off by making the voltage LOW
      delay(1000);                      // wait for a second
    }
  ```


### I2C EEPROM
- 24AA02E64 2Kb I2C EEPROM chip with EUI-64 MAC ID. The EUI-64 can be used as globally unique Device EUI (DevEUI) to uniquely identify a LoRaWAN node.
- The EEPROM chip can be powered from 3.3V or from GPIO pin `A2` using the jumper.
- If you are concerned with power consumption, I would suggest using pin `A2` to control the EEPROM power or remove both jumpers if you don't want EEPROM.
- The I2C address of 24AA02E64 is `0b 1 0 1 0 A2 A1 A0` apparently for this particular device the last three bits (A2 A1 A0) (excluding R/W bit) are marked don't care, that means the device will respond to any address from `0x50` to `0x57`.
- It's possible to use [Sparkfun EEPROM library](https://github.com/sparkfun/SparkFun_External_EEPROM_Arduino_Library/tree/main), although it does not have straight forward function to extract EUI-64. Below is the list of settings that is required by the library for 24AA02E64. 
  - Memory Type = 2, used by `setMemoryType() \\ If you are using this function then below functions are not needed.` 
  - Memory size in bytes = 256, used by `setMemorySizeBytes(256)`
  - Address range in bytes = 1, used by `AddressBytes(1)`
  - Page size in bytes = 128, used by `setPageSizeBytes(128)`
- Below is the sample code to extract EUI-64 using [Sparkfun EEPROM library](https://github.com/sparkfun/SparkFun_External_EEPROM_Arduino_Library/tree/main)
  ```c
  ```

### Battery Charger
- MCP73831 is used to charge to single cell Li-ion/Li-polymer via USB.
- The regulation voltage during constant-voltage mode is fixed at `4.2V`
- The regulation current (max charging current) is fixed at `~210mA` 

### Measuring VBAT voltage
- Voltage divider is placed between VBAT and A3 as shown in figure
- When only USB is connected the reading from A3 is the regulation voltage (Constant-Voltage mode) of MCP73831 which is 4.2V
- When USB and battery are connected the reading from A3 is the charging voltage. 
- When only battery is connected, then A3 will read the actual battery voltage.
- Below sample code helps you to read the correct battery voltage correctly.

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
