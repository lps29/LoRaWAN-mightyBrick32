# LoRaWAN-mightyBrick32
Everything you need to know about LoRaWAN-mightyBrick32 board

### Bootloader
- The LoRaWAN-mightyBrick32 runs the standard Arduino Zero bootloader but compiled for ATSAMD21E18 MCU.
- The booloader is located in the first 8KB of internal flash memory and is protected by the NVM user byte fuse.
- The LoRaWAN-mightyBrick32 bootloader is available (here)[] for download if you wish to reflash using a SWD programmer.

### How to use the board in Arduino IDE?
- To use LoRaWAN-mightyBrick32 with Arduino IDE you will need to install the latest **Arduino SAMD Boards** package and then also the **LowPowerSolutions SAMD Boards** package by [LowPowerSolutions](https://www.tindie.com/stores/lps/).
- Add the MightyBrick core json definition URL ([https://lps29.github.io/MightyBrick/package_LowPowerSolutions_index.json](https://lps29.github.io/MightyBrick/package_LowPowerSolutions_index.json)) to your Board Manager. Follow this [link](https://support.arduino.cc/hc/en-us/articles/360016466340-Add-third-party-platforms-to-the-Boards-Manager-in-Arduino-IDE) to know how to add third-party platforms to the Boards Manager in Arduino IDE.

### Pinout 
- Use "Arduino Pin Names" in the tables below to access pins in Arduio IDE.
- SPI (SERCOM1) is connected to LoRa module.
  | SPI  | Arduino Pin Names| 
  |:-------:|:-----------------:|
  | MISO  | 6 or RF_MISO |
  | MOSI  | 4 or RF_MOSI |
  | SCLK  | 5 or RF_SCK  |
  | SS    | 7 or RF_CS   |
-  The table below only contains short description of the pins, more details on `VE`, `VB` &amp; `3v3` pins and various jumpers can be found in section [`How to power the board`](#how-to-power-the-board) and [`Solder jumpers`](#Solder-jumpers).

    <table>
    <thead>
        <tr>
            <th colspan=2> Description </th>
            <th> Arduino Pin Names </th>
            <th> PCB Pin Names </th>
            <th> LoRaWAN-mightyBrick32 </th>
            <th> PCB Pin Names </th>
            <th> Arduino Pin Names </th>
            <th colspan=2> Description </th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>-</td>
            <td>Ground</td>
            <td>-</td>
            <td>G</td>
            <td rowspan=13> <img src="/images/LoRaWAN_mightBrick32_PCB1.png" alt="drawing" width="200"/> </td>
            <td>VE</td>
            <td>-</td>
            <td>Voltage External</td>
            <td>-</td>
        </tr>
        <tr>
            <td>-</td>
            <td>Active low reset</td>
            <td>-</td>
            <td>RST</td>
            <td>VB</td>
            <td>-</td>
            <td>Voltage Battery</td>
            <td>Connected to JST +</td>
        </tr>
        <tr>
            <td>-</td>
            <td>Analog Reference</td>
            <td>-</td>
            <td>AR</td>
            <td>G</td>
            <td>-</td>
            <td>Ground</td>
            <td>-</td>
        </tr>
        <tr>
            <td></td>
            <td>Analog-0</td>
            <td>A0 or 12</td>
            <td>A0</td>
            <td>3v3</td>
            <td>-</td>
            <td>3.3V</td>
            <td>-</td>
        </tr>
        <tr>
            <td>-</td>
            <td>Analog-1</td>
            <td>A1 or 13</td>
            <td>A1</td>
            <td>SCL</td>
            <td>7 or SCL</td>
            <td>I2C SCL</td>
            <td>-</td>
        </tr>
        <tr>
            <td>EEPROM power enable via jumper MEM_GPIO</td>
            <td>Analog-2</td>
            <td>A2 or 14</td>
            <td>A2</td>
            <td>SDA</td>
            <td>6 or SDA</td>
            <td>I2C SDA</td>
            <td>-</td>
        </tr>
        <tr>
            <td>Bat voltage measurement via jumper B</td>
            <td>Analog-3</td>
            <td>A3 or 15</td>
            <td>A3</td>
            <td>5</td>
            <td>-</td>
            <td>GPIO-5</td>
            <td>RFM_DIO2 via jumper D2</td>
        </tr>
        <tr>
            <td>LED via jumper L</td>
            <td>Analog-4</td>
            <td>A4 or 16</td>
            <td>A4</td>
            <td>4</td>
            <td>-</td>
            <td>GPIO-4</td>
            <td>RFM_DIO1 via jumper D1</td>
        </tr>
        <tr>
            <td>-</td>
            <td>GPIO 0</td>
            <td>0</td>
            <td>0</td>
            <td>3 RX0</td>
            <td>3 or RX0</td>
            <td>GPIO-3/Serial0-RX</td>
            <td>-</td>
        </tr>
        <tr>
            <td>-</td>
            <td>GPIO-1</td>
            <td>1</td>
            <td>1</td>
            <td>2 TX0</td>
            <td>2 or TX0</td>
            <td>GPIO-2/Serial0-TX</td>
            <td>-</td>
        </tr>
        <tr>
            <td>-</td>
            <td>-</td>
            <td>-</td>
            <td>-</td>
            <td>SWC</td>
            <td>23</td>
            <td>SWD CLK</td>
            <td>-</td>
        </tr>
        <tr>
            <td>-</td>
            <td>-</td>
            <td>-</td>
            <td>-</td>
            <td>SWI</td>
            <td>24</td>
            <td>SWD IO</td>
            <td>-</td>
        </tr>
        <tr>
            <td>-</td>
            <td>-</td>
            <td>-</td>
            <td>-</td>
            <td>G</td>
            <td>-</td>
            <td>Ground</td>
            <td></td>
        </tr>
    </tbody>
    </table>

### Compatible Radios
- You can easily find various vendors selling LoRa modules, they all will work as long as their dimensions and pinout are as per the images below. For example - [link1](https://www.mouser.fr/ProductDetail/RF-Solutions/RFM95W-868S2?qs=OlC7AqGiEDnmrtVOomfBWA%3D%3D), [link2](https://www.nicerf.com/lora-module-lora1276-c1-868.html)
  Dimensions in mm            |  Pinout
  :-------------------------:|:-------------------------:
  ![](/images/LoRa-module-dimension.png)  |  ![](/images/LoRa-module-pinout.png)

### Solder jumpers
- There are many jumpers on LoRaWAN-mightyBrick32, here's a short description of each and default state. Please follow schematics for more details.
  - **L** (open) : Connect and disconnect on-board blue LED from `A3` pin. This allows you to use `A3` if required. See section on [`Blue LED`](#blue-led) for more details
  - **B** (open) : There are two jumpers labeled as B, close both of them to enable `VBAT` measuring circuit, open both of them to save leakage current of around ~1.65uA. See section on [`Measuring VBAT voltage`](#measuring-vbat-voltage) for more details.
  - **VB** (close) and VE (open) : As depicted in the figure below, it's a 2:1 jumper, where the middle pad is common to both VB and VE. This jumper is used to select battery voltage (`VBAT`) or external voltage (`VIN_EXT`) as the input voltage source for the 3.3V LDO. See section on [`How to power the board`](#how-to-power-the-board) for more details.
  - **D1** (open) : Close it to connect LoRa module's `DIO1` pin to pin `17` of the MCU.
  - **D2** (open) : Close it to connect LoRa module's `DIO2` pin to pin `18` of the MCU.
  - **MEM_3v3_JP** (close) and **MEM_GPIO_JP** (open) : This jumper is not labelled on the board because of space but is shown in figure below. It's a 2:1 jumper, where the middle pad is common to both **MEM_3v3_JP** and **MEM_GPIO_JP** and is connected to VCC of the 24AA02E64 EEPROM. This jumper allows EEPROM to be power from 3.3V or from GPIO. See section on [`I2C EEPROM`](#i2c-eeprom) for more details.
  - **3v3_JP** (close) : This jumper is not labelled on the board because of space but is shown in figure below. As depicted in the <a href="#jumpers">figure</a> open this jumper to use externally supplied 3.3V using the pin labeled 3v3. See section on [`How to power the board`](#how-to-power-the-board) for more details.
  - **SD_JP** (close) : This jumper is not labelled on the board because of space but is shown in figure below. As depicted in the figure below open this jumper to eliminate reverse leakage current of this shockkty diode. After this avoid connecting the USB as this will disconnect power (`VIN_EXT` or `VBAT`) from rest of the circuit. This is useful in the deployment phase where you only need battery and want to eliminate unnecessary leakage current.
  
  <a name="jumpers">![On board jumpers](/images/lorawan_mightybrick32_power_jumpers.svg)</a>

### How to power the board
- The board can be powered from 4 different input voltage sources as follows : 
  - USB
    - The 5V (`VBUS`) of the USB gets converted to 3.3V using MCP1703A LDO, that powers the rest of the system.
    - The actual voltage received by MCP1703A is 5V minus the forward voltage drop of schottky diode (D1).
    - The battery charging circuit (MCP73831) is active.
  - Battery Voltage `VBAT`
    - The battery voltage (`VBAT`) ~3.7V gets converted into 3.3V using MCP1703A LDO, that powers the rest of the system.
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
- When USB and (VBAT or VIN_EXT) are connect simultaneously the voltage from the USB gets preference automatically. The MCP1703A is powered from `VBUS` and the battery charging circuit (MCP73831) is active.
- The diagram below summarizes the various imput voltage sources.
- Please see schematics for more details.
- Below table summarizes the various power options :
  | Power Options | Decription                      |
  |---------------|---------------------------------|
  | USB           | 5V via USB                      |
  | VBAT          | 3.7V Li-ion/Li-poly via JST     |
  | VIN_EXT       | 3.7 - 6V via VE pin             |
  | 3.3V External | 3.3V regulated via 3v3 pin      |

### Blue LED
- The on-board blue LED is attached to pin `A4`, that can be used for debugging.
- If needed, a jumper is provided (labelled as L) to remove LED from pin `A4`.
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
### Peripherals
In SAMD21E18 MCU there are 4 SERCOM ports that can be configured to use for UART, I2C or SPI. By default in Arduino the UART is on SERCOM0, I2C on SERCOM3 and SPI on SERCOM1. 
- UART (SERCOM0)
  - `Serial` is same as `SerialUSB` and is available on USB.
  - `Serial0` is available on pin number 3 (RX) and 2 (TX).
  - It is possible to add another UART using SERCOM2 on pin 0,1 or 4,5 if RFM_DIO1 and RFM_DIO2 is not required. 
- I2C (SERCOM3)
  - I2C is on pin numer 6 (SDA) and 7 (SCL), so calling `Wire.begin()` will automatically initialize I2C on 6 and 7. 
- SPI (SERCOM1)
  - asfsdfsdfsdf
- If required it is possible to add another UART or I2C or SPI using SERCOM2 on pin 0,1,4,5. If RFM_DIO1 and RFM_DIO2 is in use than SPI is not possible using SERCOM2.

### I2C EEPROM
- 24AA02E64 2Kb I2C EEPROM chip with EUI-64 MAC ID. The EUI-64 can be used as globally unique Device EUI (DevEUI) to uniquely identify a LoRaWAN node.
- The EEPROM chip can be powered from 3.3V or from GPIO pin `A2` using jumpers `MEM_3v3` and `MEM_GPIO` respectively.
- If you are concerned with power consumption, I would suggest using pin `A2` to control the EEPROM power or remove both jumpers if you don't want EEPROM.
- The I2C address of 24AA02E64 is `0b 1 0 1 0 A2 A1 A0` and for this particular device the last three bits (A2 A1 A0) (excluding R/W bit) are marked don't care, that means the device will respond to any address from `0x50` to `0x57`.
- It's possible to use [Sparkfun EEPROM library](https://github.com/sparkfun/SparkFun_External_EEPROM_Arduino_Library/tree/main). Below is the list of settings that is required by the library for 24AA02E64, please see 24AA02E64 datasheet for more details.
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
