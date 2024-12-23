# Home-Appliance-Control-Using-ESP32-and-MQTT
This project allows you to control appliances (e.g., lights, fans) using an ESP32 board via an MQTT protocol. The control signals are sent through a smartphone or laptop using the Ubidots MQTT broker.

Materials Required
ESP32 Development Board
4-channel relay module
Appliances (e.g., LED bulbs)
Jumper wires
Power supply

Circuit Diagram
I'll provide the circuit diagram description below. If you want an image of the schematic, let me know!

Relay Module to ESP32 Connections:

Relay IN1 → GPIO 25
Relay IN2 → GPIO 26
Relay IN3 → GPIO 27
Relay IN4 → GPIO 14
VCC → 5V
GND → GND
Appliances:

Connect the appliances to the Normally Open (NO) terminal of each relay.
Connect the Common (COM) terminal to the power source of the appliance.
Power Supply:

Use a 5V USB power adapter for the ESP32 board.
