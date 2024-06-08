---
title: 'Cloud Driven Smart Energy Meter'
author: '**Natalya Pishna and Saifedin Maani** (website template by Ryan Tsang)'
date: '*EEC172 SQ24*'

toc-title: 'Table of Contents'
abstract-title: '<h2>Description</h2>'
abstract: 'Our innovative Smart Power Meter is designed to transform how home energy consumption is managed and monitored. This Smart Power Meter conducts real-time power measurements for household appliances, and controls power utilization with reliable relays. The primary advantage of this design is to provide users with actionable insights into their energy use, through informed monitoring of local rates and consumption daily, using our Cloud service. This is the standout feature of this smart meter powered by AWS Cloud SNS communication, which can also send immediate notifications during power outages and alerts about peak hour rates to avoid high energy costs 
<br/><br/>
Our source code can be found
<a href="https://github.com/natpish/final_proj_src_code">
  here (placeholder)</a>.

<div style="display:flex;flex-wrap:wrap;justify-content:space-evenly;padding-top:20px">
  <div style="display: inline-block; vertical-align: bottom;">
    <img src="./media/Image_001.jpg" style="width:auto;height:2in"/>
    <!-- <span class="caption"> </span> -->
  </div>
  <div style="display: inline-block; vertical-align: bottom;">
    <img src="./media/Image_002.jpg" style="width:auto;height:2in" />
    <!-- <span class="caption"> </span> -->
  </div>
</div>

<h2>Video Demo</h2>
<div style="text-align:center;margin:auto;max-width:560px">
  <div style="padding-bottom:56.25%;position:relative;height:0;">
    <iframe style="left:0;top:0;width:100%;height:100%;position:absolute;" width="560" height="315" src="https://www.youtube.com/embed/wSRtnAEZhmc?si=3vQXNj4h0WkW-F-q" title="YouTube video player" frameborder="0" allow="accelerometer; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
  </div>
</div>
'
---

# HOW IS OUR PROJECT DIFFERENT?
## Existing Products:

Poniie, kuman, MECHEER and existing products that monitor real-time energy consumption and display cost. 
Our product goes beyond just monitoring, it also provides cloud-driven insights to revolutionize how 
you manage your energy consumption. The other products that are similar are expensive, 
but our product has the advantage of being cheap and small-scale which is more suitable for homeowners.

<div style="display:flex;flex-wrap:wrap;justify-content:space-evenly;">
  <div style='display: inline-block; vertical-align: top;'>
    <img src="./media/Image_003.jpg" style="width:auto;height:200"/>
    <span class="caption">
      <a href="https://aerogarden.com/gardens/harvest-family/Harvest-2.0.html">AeroGarden Harvest 2.0</a>
      <ul style="text-align:left;">
      <li>Inexpensive ($90)</li>
      <li>Not Automated</li>
      <li>Small Scale</li>
      <li>No remote monitoring</li>
    </ul>
    </span>
  </div>
  <div style='display: inline-block; vertical-align: top;'>
    <img src="./media/Image_004.jpg" style="width:auto;height:200" />
    <span class="caption">
      <a href="https://www.hydroexperts.com.au/Autogrow-MultiGrow-Controller-All-In-One-Controller-8-Growing-Zones">Autogrow Multigrow</a>
      <ul style="text-align:left;">
      <li>Expensive ($4500)</li>
      <li>Fully Automated</li>
      <li>Huge Scale</li>
      <li>Cloud monitoring</li>
    </ul>
    </span>
  </div>
</div>

# Design

## System Architecture

<div style="display:flex;flex-wrap:wrap;justify-content:space-evenly;">
  <div style="display:inline-block;vertical-align:top;flex:1 0 400px;">
The system architecture consists of two architectures: IoT and Embedded System architectures.

### Embedded System Architecture
There are 4 main hardware components in this architecture: The CC3200 micro-controller, the INA219 current sensor, Oled display and a single-channel relay module.
The CC3200 enables power supplied to a DC load using a 5V High/Low trigger single-channel relay module that can be used to connect/disconnect power via a GPIO Output High level trigger. When power is supplied, the INA219 sensor measures voltage and current through a 0.1 Ohm shunt voltage resistor. These power measurements can be used to measure the power consumed by the load. The data is obtained via I2C communication, and can then be used to compute energy consumption calculations such as hourly energy cost, and hourly average power (kW/h).

### IoT System Architecture
Our IoT infrastructure enables the user with the advantage of robust energy consumption management, and monitoring. User settings and configurations such as manual power control, and hourly rate adjustments per peak hours can be configured onto the micro-controller via GET requests. Furthermore, the hourly average power consumption and load status are communicated to the user directly through POST requests forwarded to the user through AWS IoT SNS. 
This architecture enables continuous power monitoring insights for the user every hour, in the aim of better energy management enabled by insights and power control.

  </div>
  <div style="display:inline-block;vertical-align:top;flex:0 0 400px;">
    <div class="fig">
      <img src="./media/Image_005.jpg" style="width:90%;height:auto;" />
      <span class="caption">System Flowchart</span>
    </div>
  </div>
</div>

## Functional Specification

<div style="display:flex;flex-wrap:wrap;justify-content:space-evenly;">
  <div style="display:inline-block;vertical-align:top;flex:1 0 300px;">
    
### Local System Overview
The Smart Power Meter was designed using the CC3200 Micro-controller integrated with an Oled screen display, a power sensor and wireless IoT communication. Our design uses the INA219 to collect power measurements interfaced with the CC3200 using I2C.
The measurements are used to compute real-time energy consumption calculations using local rates, and shown for the user on an Oled display. The onsite UI is also integrated with an manual override capability for power control using an IR receiver feature.

### Cloud Driven Insights
The Smart Power Meter drives energy monitoring and management through our Cloud AWS IoT servers, enabling dynamic user setting changes and local rate variations using GET requests along with reporting of hourly power data and outage notification via POST requests. 

### Power Control
Based on user settings configured through AWS IoT, the Smart Energy Meter can control a relay connected by GPIO, in order to connect and disconnect power to a load. This feature allows remote management of power consumption based on user preferences driven by Cloud data insights.

  </div>
  <div style="display:inline-block;vertical-align:top;flex:0 0 500px">
    <div class="fig">
      <img src="./media/Image_006.jpg" style="width:90%;height:auto;" />
      <span class="caption">State Diagram</span>
    </div>
  </div>
</div>

# Implementation

### CC3200 Core Hardware
The core hardware of the prototype is illustrated in the schematic shown in \textit{\textbf{Figure 4}}. The schematic shows all the hardware modules involved, along with all the pin connections, additional components and organization of the embedded system architecture.

\begin{figure}[h]
    \centering
    \includegraphics[width=1.1\linewidth,height=6in]{schematic.png}
    \caption{Smart Power Meter Prototype Schematic}
    \label{fig:button-3}
\end{figure}

### CC3200 Core Software
The core software of the prototype is illustrated in the block diagram shown in \textit{\textbf{Figure 5}}. The diagram summarizes the logic components of the software involved in the prototype.

\begin{figure}[h]
    \centering
    \includegraphics[width=1.1\linewidth,height=3in]{s_block.png}
    \caption{Smart Power Meter Prototype Software}
    \label{fig:button-4}
\end{figure}


### INA219 Overview and Hardware Configuration
The INA219 power sensor measures voltage and current using ADC applied to a 0.1 Ohm shunt voltage measurement. It can communicate with a micro controller via I2C. The Adafruit INA219 breakout board module was used, which was equipped with INA219 pull-up resistors for I2C to easily integrate the INA219 with the prototype. A 3.3 VCC and GND is connected from the C3200 to power the INA219 chip. The VIN + and VIN - are the pins that connected to the 0.1 Ohm shunt resistor, in which the VIN + was connected to the power supply and VIN - was connected to the load entry node. The INA219 additionally has two configuration pins A0 and A1 used to customize the I2C device address between 16 different possible addresses. In the case of the Adafruit INA210 breakout board, both pins were connected to GND and so the device address was by default 0x40.

### INA219 I2C Firmware Implementation
The I2C API Library for the INA219 integration with the CC3200 was written by Saifedin using the INA219 data-sheet (containing information about device and register addresses). In the implementation, the main two register addresses used were 0x01 for the shunt voltage and 0x02 for the bus voltage. These are 16 bit registers, and the I2C readfrom function was adapted to use 2 bytes rather than just one byte in other I2C CC3200 applications. Using the shunt voltage, the current was calculated by dividing the shunt voltage reading by 0.1 ohm. Power can then be calculated by multiplying the calculated current with the voltage reading.

### Single-Channel DC Relay Hardware and Software
A 5V powered Single-Channel DC Relay was used to control the load power. DC + and DC - were the relay power pins connected to the CC3200 5V pin and GND. The IN pin is used to control the state of the relay using an Output HIGH/LOW trigger depending on the configuration. In our prototype, GPIO pin 60 was configured as an output pin and connected to the IN pin. This relay has three application pins: NO, NC, and COM. COM is always connected directly to the DC power positive terminal. The NO (Normally-Open) and NC (Normally-Closed) pins are used exclusively. If NC is open, and NO is connected directly to the load. Then, if the IN receives a HIGH GPIO signal the relay connects the power to the load, otherwise the load power is always disconnected (OPEN). This was the configuration used in our prototype.

### Oled Display
A 1.5"" 128x128 OLED Adafruit breakout board was used to display
graphics and interfaces with the CC3200 via 3-pin SPI communication.
The pins used from this breakout boardwere the SCK (SPI Clock pin), SI (SPI MOSI pin), OLEDCS( SPI CSpin), R (RESET pin), DC (Data/Command pin), Vin (3.3 V supply)and a GND pin. The OLEDCS was configured to be connected to a
GPIO for a software chip select, the DC pin was biased to HIGH
for Data and LOW for Command. Lastly, there was an active-low
reset pin. For the prototype, the title "Cloud-Driven Smart Energy Meter" would first be displayed. Then, a list of dynamically changing values would be displayed to reflect the measurements and calculations for average power, energy cost and relay status. The placeholder text would first be printed, and remain static throughout such as "Power: ". However, we developed a function to input float values and desired display indexes to print characters next to the placeholder text dynamically as values changed. This way "Power: -5.437 mW" would be printed and varied according to calculations and measurements.

### IR Receiver Software and Hardware
An IR receiver was used and interfaced with GPIO pin 18 with the OUT pin, where IR digital signals were decoded following the NEC specification encoding. The IR receiver requires a low-pass filter recommended with 100 ohm resistor in series with a capacitor to GND, this is to provide power stability for the IR receiver. \cite{Vishay:824932} The decoding of the signal was implemented using SysTick timers to time and record lengths of pulses per the NEC specification, from which data is sampled and the button pressed from the IR remote could be identified \cite{Vishay:80071}.
The IR receiver application was solely used for a user controlled manual override of the relay. 

### AWS IoT Integration
Using an IoT server that was configured with the enumeration of
an AWS IoT device. For the prototype, an SNS topic subscribed to
an email address was used, with an IoT rule was created with an
SQL statement that uses the SELECT modifier to send a specified
area of the shadow POST update JSON message. In the prototype,
it was attempted to send status on hourly energy costs and relay
operation.

### Prototype Application Notes
The INA219 is also capable of measuring current and power designed to concurrently support micro-controller CPU compute. In practice, we avoided reading from these registers to avoid I2C communication overhead.
It is recommended to use separate VCC and GND pins for all modules and not to provide common VCC or GND 
It is recommended to connect an extra capacitor between VIN + and VIN - for the INA219 which helped stabilise the sensor readings and provided better accuracy for I2C readings.

  </div>
  <div style='display: inline-block; vertical-align: top;flex:1 0 600px'>
    <div class="fig">
      <img src="./media/Image_013.jpg" style="width:auto;height:2in;padding-top:30px" />
      <span class="caption">Pump Circuit Diagrams</span>
    </div>
  </div>
</div>

# Challenges

## I2C Communication
The principle challenge was establishing I2C communication with the first batch the INA219 sensors ordered (not Adafruit). Saifedin spent many days troubleshooting why the I2C communication is failing, and using a protocol analyzer it was identified that there was an abrupt clock that is consistently shorted to GND. It was assumed those parts were defective, and an Adafruit sensor ordered arrived before the prototype presentation.The only difference was that this board an LED indicator to indicate power stability across the board. It was discovered that those INA219 breakout boards have a wire header for VIN + and VIN - that is impractical for breadboard prototyping because the entire breakout board is designed for PCB mounting, and not for breadboard prototypes. This connection header kept being loose, and attempting to force the connection allowed I2C communication to work. We realized because of how extremely frequent the wire header was loose, the all the connections to the sensor were grounded - by design to avoid damaging the INA219 chip.
This imposed a challenge to prepare a robust prototype, as integrating the Oled and relay throughout was very difficult because of the difficulty to have consistent power stability with loose wire header.
The only way this challenge was overcome for the demonstration was by holding the wire header firmly to the breakout board but that does not always help.

## Hardware Setup
There are many components used for this prototype and power stability across the entire was impossible with the limited VCC pins and GND pins. The INA219 continuously led to cases where the Oled and CC3200 were sinking current because of the power instability. Therefore, when connecting the same VCC of the CC3200 shared by two or modules all the modules stopped operating. In a similar fashion, using common GND pins for different modules, even with the load, led to the same issue. 
To overcome this issue, we used another CC3200 to supply VCC and GND to the IR reciever and relay. We also made sure to add separate VCC and GND pins to each module, and lastly we added a 100 uF capacitor between VCC and GND to filter out any voltage surges that led to more robustness, especially with the instability issue of the INA219 sensor. 

## Software
Another issue occurred with the JSON object manipulation for POST requests, that was challenging for posting two different data values continuously. Lastly, during the presentation, AWS could not connect successfully to the board due to some back-end issues.

# Future Work

Given more time, we had the idea of developing a web app to allow users
to control the device from their cell phone. Another idea we wanted to
implement in the future is adding a grow light and pH controller to
maintain a more suitable and stable environment for different plants to
grow.


# Finalized BOM

<!-- you can convert google sheet cells to html for free using a converter
  like https://tabletomarkdown.com/convert-spreadsheet-to-html/ -->

<table style="border-collapse:collapse;">
<thead>
  <tr>
    <th><p>No.</p></th>
    <th><p>PART NAME</p></th>
    <th><p>DESCRIPTION</p></th>
    <th><p>Qty</p></th>
    <th><p>SUPPLIER / MANUFACTURER</p></th>
    <th><p>UNIT COST</p></th>
    <th><p>TOTAL PART COST</p></th>
    <th><p>Purpose</p></th>
  </tr>
</thead>
<tbody>
  <tr>
    <td><p>1</p></td>
    <td><p>CC3200-LAUNCHXL</p></td>
    <td><p>MCU Evaluation Board</p></td>
    <td><p>2</p></td>
    <td><p>Provided by EEC172 Course</p></td>
    <td><p>$66.00</p></td>
    <td><p>$132.00</p></td>
    <td><p>Control Remote and Local Devices</p></td>
  </tr>
  <tr>
    <td><p>2</p></td>
    <td><p>Adafruit 1431 OLED</p></td>
    <td><p>128x128 RGB OLED Display. SPI protocol</p></td>
    <td><p>2</p></td>
    <td><p>Provided by EEC172 Course</p></td>
    <td><p>$39.95</p></td>
    <td><p>$79.90</p></td>
    <td><p>Display PPM, Temperature, Thresholds, Inputs</p></td>
  </tr>
  <tr>
    <td><p>3</p></td>
    <td><p>Adafruit 4547 3VDC Pump</p></td>
    <td><p>Submersible pump. 3V 100mA DC</p></td>
    <td><p>2</p></td>
    <td><p>Adafruit</p></td>
    <td><p>$2.95</p></td>
    <td><p>$5.90</p></td>
    <td><p>For dispensing water and nutrient solution</p></td>
  </tr>
  <tr>
    <td><p>4</p></td>
    <td><p>Adafruit 4545 6mm Tube</p></td>
    <td><p>6mm Silicone Tube: 1 meter length</p></td>
    <td><p>1</p></td>
    <td><p>Adafruit</p></td>
    <td><p>$1.50</p></td>
    <td><p>$1.50</p></td>
    <td><p>For dispensing water and nutrient solution</p></td>
  </tr>
  <tr>
    <td><p>5</p></td>
    <td><p>NTC Thermistor 10k</p></td>
    <td><p>10k ohm nominal resistance, 100cm lead</p></td>
    <td><p>1</p></td>
    <td><p>(Already had one, available on Aliexpress)</p></td>
    <td><p>$0.92</p></td>
    <td><p>$0.92</p></td>
    <td><p>For temperature compensation</p></td>
  </tr>
  <tr>
    <td><p>6</p></td>
    <td><p>Adafruit AD1015 12-bit ADC</p></td>
    <td><p>12-bit resolution, 4 channels, I2C</p></td>
    <td><p>1</p></td>
    <td><p>Adafruit</p></td>
    <td><p>$9.95</p></td>
    <td><p>$9.95</p></td>
    <td><p>To convert Thermistor and TDS sensor reading to digital</p></td>
  </tr>
  <tr>
    <td><p>7</p></td>
    <td><p>PN2222A Transistor</p></td>
    <td><p>NPN BJT (40V, 1000mA)</p></td>
    <td><p>2</p></td>
    <td><p>Digikey (onSemi)</p></td>
    <td><p>$0.40</p></td>
    <td><p>$0.80</p></td>
    <td><p>For digital motor control</p></td>
  </tr>
  <tr>
    <td><p>8</p></td>
    <td><p>1N4001 Rectifier Diode</p></td>
    <td><p>Diffused junction: 50V 1000mA</p></td>
    <td><p>2</p></td>
    <td><p>Digikey (Good-Ark Semi)</p></td>
    <td><p>$0.16</p></td>
    <td><p>$0.32</p></td>
    <td><p>Reverse Current Protection</p></td>
  </tr>
  <tr>
    <td><p>9</p></td>
    <td><p>10k ohm resistor</p></td>
    <td><p>10k ohm , 1% tolerance, 0.25W</p></td>
    <td><p>1</p></td>
    <td><p>Digikey (Stackpole Electronics)</p></td>
    <td><p>$0.10</p></td>
    <td><p>$0.10</p></td>
    <td><p>Voltage divider for Thermistor</p></td>
  </tr>
  <tr>
    <td><p>10</p></td>
    <td><p>Vishay TSOP31130 IR RCVR</p></td>
    <td><p>30kHz carrier frequency</p></td>
    <td><p>2</p></td>
    <td><p>Provided by EEC172 Course</p></td>
    <td><p>$1.41</p></td>
    <td><p>$2.82</p></td>
    <td><p>Decode user inputs</p></td>
  </tr>
  <tr>
    <td><p>11</p></td>
    <td><p>330 ohm resistor</p></td>
    <td><p>330 ohm resistor, &lt;5% tolerance, 3W</p></td>
    <td><p>2</p></td>
    <td><p>Provided by EEC172 Course</p></td>
    <td><p>$0.59</p></td>
    <td><p>$1.18</p></td>
    <td><p>Current Limit for IR Receiv er</p></td>
  </tr>
  <tr>
    <td><p>12</p></td>
    <td><p>ATT-RC1534801 Remote</p></td>
    <td><p>General-purpose TV remote. IR NTC protocol</p></td>
    <td><p>1</p></td>
    <td><p>Provided by EEC172 Course</p></td>
    <td><p>$9.99</p></td>
    <td><p>$9.99</p></td>
    <td><p>Allow user inputs</p></td>
  </tr>
  <tr>
    <td><p>13</p></td>
    <td><p>CQRSENTDS01 TDS Sensor</p></td>
    <td><p>Analog reading 0-2.3V. 0-1000ppm range</p></td>
    <td><p>1</p></td>
    <td><p>CQRobot</p></td>
    <td><p>$7.99</p></td>
    <td><p>$7.99</p></td>
    <td><p>Measure TDS of plant solution</p></td>
  </tr>
  <tr>
    <td><p>14</p></td>
    <td><p>10uF Capacitor</p></td>
    <td><p>Electrolytic Cap 100V</p></td>
    <td><p>2</p></td>
    <td><p>Provided by EEC172 Course</p></td>
    <td><p>$0.18</p></td>
    <td><p>$0.36</p></td>
    <td><p>DC Filtering for IR Receiv er</p></td>
  </tr>
  <tr>
    <td><p>15</p></td>
    <td><p><u>AA Battery (4ct</u>)</p></td>
    <td><p>1.5 Volt, Non-rechargable</p></td>
    <td><p>1</p></td>
    <td><p>Already had, but</p>
      <p>available on Amazon</p></td>
    <td><p>$3.65</p></td>
    <td><p>$3.65</p></td>
    <td><p>Provide Power to Motors</p></td>
  </tr>
  <tr>
    <td><p>16</p></td>
    <td><p>Battery Holder</p></td>
    <td><p>2xAA (3 Volts Total)</p></td>
    <td><p>2</p></td>
    <td><p>Amazon</p></td>
    <td><p>$2.50</p></td>
    <td><p>$4.99</p></td>
    <td><p>Provide Power to Motors</p></td>
  </tr>
  <tr>
    <td colspan="3">
      <p>TOTAL PARTS</p></td>
    <td><p>25</p></td>
    <td colspan="2">
      <p>TOTAL</p></td>
    <td><p>$262.37</p></td>
    <td></td>
  </tr>
  <tr>
    <td colspan="3">
      <p>TOTAL PARTS (Excluding Provided)</p></td>
    <td><p>14</p></td>
    <td colspan="2">
      <p>TOTAL (Exluding Provided)</p></td>
    <td><p>$36.12</p></td>
    <td></td>
  </tr>
</tbody>
</table>
