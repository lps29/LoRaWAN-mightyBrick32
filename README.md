# LoRaWAN-mightyBrick32
Everything you would like to know about LoRaWAN-mightyBrick32 board

### How to use the board in Arduino IDE?
- To use LoRaWAN-mightyBrick32 with Arduino IDE you will need to install the latest **Arduino SAMD Boards** package and then also the **LowPowerSolutions SAMD Boards** package by [LowPowerSolutions](https://www.tindie.com/stores/lps/).
- Add the MightyBrick core json definition URL ([https://lps29.github.io/MightyBrick/package_LowPowerSolutions_index.json](https://lps29.github.io/MightyBrick/package_LowPowerSolutions_index.json)) to your Board Manager. Follow this [link](https://support.arduino.cc/hc/en-us/articles/360016466340-Add-third-party-platforms-to-the-Boards-Manager-in-Arduino-IDE) to add third-party platforms to the Boards Manager in Arduino IDE.

### Solder jumpers
- There are many jumpers on LoRaWAN-mightyBrick32, here's a short description of each and default state. Please follow schematics for more details. See section on [`Blue Led`](#blue-led) for more details.
  - **L** (open) : Use it to connect and disconnect on-board blue LED from `A3` pin. This allows you to save some power or if `A3` is required. See section on [`Measuring VBAT voltage`](#measuring-vbat-voltage) for more details.
  - **B** (open) : There are two jumpers labeled as B, close both of them to enable `VBAT` measuring circuit, open both of them to save leakage current of around ~$1.65\mu A$.
  - **VB** (close) and VE (open) : It's a 2:1 jumper, where the middle pad is common to both VB and VE. This jumper is used to select battery voltage (`VBAT`) or external voltage (`VIN_EXT`) as the input voltage source. See section on [`How to power the board`](#how-to-power-the-board) for more details.
  - **D1** (open) : Close it to connect LoRa module `DIO1` pin to pin `17` of the MCU.
  - **D2** (open) : Close it to connect LoRa module `DIO2` pin to pin `18` of the MCU.
  - **MEM_3v3** (close) and **MEM_GPIO** (open) : This jumper is not labelled on the board because of space but is shown in figure. It's a 2:1 jumper, where the middle pad is common to both **MEM_3v3** and **MEM_GPIO** and is connected to VCC of the 24AA02E64 EEPROM. This jumper allows EEPROM to be power from 3.3V or from GPIO. See section on [`I2C EEPROM`](#i2c-eeprom) for more details.
  - **3v3_INT** (close) : This jumper is not labelled on the board because of space but is shown in figure. Open this jumper to use externally supplied 3.3V using the pin labeled 3v3. See section on [`How to power the board`](#how-to-power-the-board) for more details.
  - **SD** (close) : This jumper is not labelled on the board because of space but is shown in figure. Open this jumper to eliminate reverse leakage current of this shockkty diode. After this avoid connecting the USB as this will disconnect power (`VIN_EXT` or `VBAT`) from rest of the circuit. This is useful in the deployment phase where you only need battery and want to eliminate this reverse leakage current.

### How to power the board
- The board can be powered from 4 different input voltage sources as follows : 
  - USB
    - The 5V (`VBUS`) of the USB gets converted to 3.3V using MCP1703A LDO, that powers the rest of the system.
    - The actual voltage received by MCP1703A is 5V minus the forward voltage drop of schottky diode (D1).
    - The battery charging circuit (MCP73831) is active.
  - Battery Voltage `VBAT`
    - The battery voltage (`VBAT`) ~4.2V gets converted into 3.3V using MCP1703A LDO, that powers the rest of the system.
    - Use jumper labeled as `VB` to enable `VBAT`, by default `VBAT` is enabled.
    - The pin labeled as `3v3` can be used to power expernal circuit.    
  - External Voltage `VIN_EXT`
    - Instead of a battery it is possble to use an external voltage source bypassing the MCP73831. Make sure `3.3V < VE < 5.5V`
    - Use jumper labeled  as `VE` to enable the `VIN_EXT`, by default `VIN_EXT` is disabled.
    - WARNING : Use either `VBAT` or `VIN_EXT`, never enable `VB` and `VE` at the same time.
    - The pin labeled as `3v3` can be used to power expernal circuit.
  - External 3.3V
    - In order to use external 3.3V open the jumper (`3v3_INT`) as shown in figure below, by default the jumper is closed.
    - Use pin labeled as `3v3` to supply the voltage.
    - This mode bypasses the MCP1703A LDO, so it removes `VBUS`, `VIN_EXT` and `VBAT` from circuit.
    - The whole system is supplied from this power source, so make sure the voltage does not increases beyond 3.3V but you can go down to 3.0V
- When USB and (VBAT or VIN_EXT) are connect simultaneously the voltage from the USB gets the preference automatically. The MCP1703A is supplied from `VBUS` and the battery charging circuit (MCP73831) is active.
- The diagram below summarizes the various imput voltage sources.
- Please check schematics for more details. 

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
- The EEPROM chip can be powered from 3.3V or from GPIO pin `A2` using jumpers `MEM_3v3` and `MEM_GPIO` respectively.
- If you are concerned with power consumption, I would suggest using pin `A2` to control the EEPROM power or remove both jumpers if you don't want EEPROM.
- The I2C address of 24AA02E64 is `0b 1 0 1 0 A2 A1 A0` apparently for this particular device the last three bits (A2 A1 A0) (excluding R/W bit) are marked don't care, that means the device will respond to any address from `0x50` to `0x57`.
- It's possible to use [Sparkfun EEPROM library](https://github.com/sparkfun/SparkFun_External_EEPROM_Arduino_Library/tree/main), although it does not have a straight forward function to extract EUI-64. Below is the list of settings that is required by the library for 24AA02E64. 
  - Memory Type = 2, used by `setMemoryType() \\ If you are using this function then below functions are not needed.` 
  - Memory size in bytes = 256, used by `setMemorySizeBytes(256)`
  - Address range in bytes = 1, used by `AddressBytes(1)`
  - Page size in bytes = 128, used by `setPageSizeBytes(128)`
- Below is the sample code to extract EUI-64 using [Sparkfun EEPROM library](https://github.com/sparkfun/SparkFun_External_EEPROM_Arduino_Library/tree/main), please feel to use anyother library.
  ```c
    #include <Wire.h>
    #include "SparkFun_External_EEPROM.h"

    ExternalEEPROM my_eeprom;
    #define EEPROM_ADDRESS 0b1010000
    uint8_t mac64[8];

    void setup() 
    {
      // put your setup code here, to run once:
      SerialUSB.begin(115200);
      delay(10);
      SerialUSB.println("I2C EEPROM example");

      Wire.begin();
      Wire.setClock(400000);

      my_eeprom.setMemoryType(2);
  
      if (my_eeprom.begin(EEPROM_ADDRESS, Wire) == false)
      {
        SerialUSB.println("No memory detected. Freezing.");
        while (true);
      }
      SerialUSB.println("Memory detected!");
    }

    void loop() 
    {
      my_eeprom.get(248, mac64);

      for(int i=0; i < 8; ++i)
      {
        SerialUSB.print(mac64[i], HEX);
        SerialUSB.print(" ");
      }
      delay(10000);
    }

  ```

### Battery Charger
- MCP73831 is used to charge to single cell Li-ion/Li-polymer via USB.
- The regulation voltage during constant-voltage mode is fixed at `4.2V`
- The regulation current (max charging current) is fixed at `~210mA` 

### Measuring VBAT voltage
- Voltage divider is placed between `VBAT` and `A3` as shown in figure
- When only USB is connected the reading from `A3` is the regulation voltage (Constant-Voltage mode) of MCP73831 which is 4.2V
- When USB and battery are connected the reading from `A3` is the charging voltage. 
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

  ### Some useful features to save power
  - 

![alt text](https://github.com/[username]/[reponame]/blob/[branch]/image.jpg?raw=true)
