TEMPERATURE-MONITORING-SYSTEM

1.Abstract: 

This project focuses on monitoring room temperature and controlling a cooler using the STM32L4 microcontroller and LM35 temperature sensor. The LM35 provides an Analog voltage proportional to temperature, which is converted into a digital value using the STM32L4’s ADC. The processed temperature data is sent to a PC through UART communication, allowing real-time monitoring on a serial terminal. The system supports both automatic and manual control. In automatic mode, the cooler turns ON when the temperature exceeds 28°C and OFF when it drops below the threshold. In manual mode, the user can send commands such as ON, OFF, or AUTO through the serial window to control the cooler remotely. This project demonstrates a simple and efficient embedded solution suitable for home automation, environmental monitoring, and basic IoT applications. 


2.Required Components:

1.Microcontroller STM32L4
2.Temperature Sensor LM35
3.Relay Module (5A, One Channel Relay)
4.Cooler Or Dc Motor
5.USB Cable
6.Jumper Wires
7.Power Supply

3. Block diagram:

  <img width="1000" height="569" alt="image" src="https://github.com/user-attachments/assets/fc64af0b-8295-4a21-85cc-45cc49d2acf1" />
4. Working Principle:

Sensing:

The LM35 senses the surrounding temperature and provides an Analog voltage output (10 mV per °C).
Example:
	25°C → 250 mV output
	50°C → 500 mV output
	Signal Conversion (ADC):
The STM32L4’s ADC converts the Analog voltage from LM35 into a digital value.
ADC value = (Input Voltage / Reference Voltage) × (2ⁿ − 1)

5.Processing:

The microcontroller calculates the actual temperature using the formula:
Temperature(°C)=(ADC_Value×Vref/(2^n-1))/10mV

6.Data Transmission (UART):

The temperature value is sent from STM32L4 to the PC via UART communication at a 
predefined baud rate (e.g., 115200 bps).

7.Data Logging / Display:

On the PC, serial terminal software displays the temperature readings continuously. 
Optionally, readings can be saved to a file for further analysis.

8.Formulas for conversion:

	Voltage V in = ((Digital value * Vref)/(2^n)-1))
	Temperature = Vin *100
		Here Vref=3.3 voltage

9.Pin Connectivity:
 
1️⃣ LM35 Temperature Sensor → STM32L4R5ZI
Temperature 
Sensor (LM35) Pin	Function	STM32L4R5ZI Pin	Description
VCC	Power supply	3.3V	Can also use 5V if LM35 supports it
GND	Ground	GND	Common with STM32
OUT	Analog voltage output	GPIO_PA14	Connect to ADC input pin.
________________________________________
  
2️⃣UART Connection (to Serial Window / PC)
USB-TTL Converter Pin	STM32L4R5ZI Pin	Description
TX	PG7(LPUART1_RX)	STM32 receives data
RX	PG8(LPUART1_TX)	STM32 sends data
GND	GND	Common ground between STM32 and PC
⚙️ Baud Rate: 115200 bps (set in Arduino uno & serial terminal)

________________________________________


3️⃣Relay Module (Cooler Control) → STM32L4R5ZI
Relay Pin	Function	STM32L4R5ZI Pin	Description
IN	Relay control input	GPIO_PA14	Controlled by STM32 GPIO
VCC	Power supply	5V	From STM32 board or external supply
GND	Ground	GND	Common with STM32
COM	Common terminal	Connected to load (fan/cooler)	----
NO	Normally Open contact	To one side of fan/cooler	----
NC	Normally Closed contact	(Not used here)	----
🧠 How it works:
	When PA14 = HIGH → relay activates → fan/cooler turns ON
	When PA14 = LOW → relay deactivates → fan/cooler turns OFF
________________________________________
4️⃣ Power Supply
Source	Voltage	Connected To
STM32 Board USB	5V	Powers board & relay
3.3V from STM32	Powers LM35 sensor	----
Common GND	All components share same ground	----

10. Software Used
    
STM32CubeIDE – for program development and flashing the code.
Arduino UNO – for viewing UART data on PC or Serial terminal.
STM32CubeIDE – for configuring peripherals (ADC and UART).

 11.Algorithm / Steps
 
	Initialize ADC and UART modules.
	Read Analog value from LM35 sensor.
	Convert ADC value to temperature.
	Format temperature data as a string.
	Transmit data via UART.
	Repeat the process periodically (e.g., every 1 second).

12.Example Output

Serial Terminal Output:
Temperature: 27.5 °C
Temperature: 28.0 °C

13.Applications

	Environmental temperature monitoring
	Smart home systems
	Industrial process control
	Weather stations
	IoT-based temperature data logging

14.Advantages

	Simple and low-cost system
	Accurate and real-time monitoring
	Easy to expand with wireless or IoT modules
	Reliable UART communication

15.Conclusion:

	This project effectively monitors temperature using the STM32L4 microcontroller and the LM35 
  sensor while controlling a cooler in both automatic and manual modes. The system accurately reads
  temperature values, sends them to the PC through UART, and switches the relay based on user 
  commands or predefined temperature limits. Overall, the system is simple, reliable, 
  and well-suited for basic automation and temperature control applications.
   <img width="797" height="406" alt="Temperature _monitoring system " src="https://github.com/user-attachments/assets/11559093-90e2-4a9b-bccb-d15f1d2257e8" />

  
