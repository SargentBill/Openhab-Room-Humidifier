# Openhab-Room-Humidifier
Activates and deactivates a room humidifier based on indoor humidity and outdoor temperature. 

## Hardware:
Digital Temperature and Humidity sensors DHT22/AMC2302 or equivalent  
Raspberry Pi running Openhab (an open source home automation program)  
Arduino Unos or equivalent (I used Arduino Nano with a Nano IO shield, which included a socket for an NRF24L01 radio module)  
Arduino Mega 2560 with W5100 ethernet shield  
Power supplies for Arduino and Raspberry Pi  
Relays rated for mains voltage (I used a solid state relay activated by 3-32 VDC)
NRF24L01 radio modules  
Wire, solder, shrink tubing, misc. electronic parts.  

## Software:
Openhab for Raspberry Pi (www.openhab.org)  
MySensors Arduino library (www.mysensors.org)  
MQTT broker running on the Raspberry Pi.  

## Overall design:
Arduino Nanos read individual DHT sensors and send the readings by radio (NRF24L01) to the Arduino Mega. The Mega connects by
ethernet cable to a network switch, to which the Raspberry Pi is also connected. The Pi accepts the payload of data from the Mega
through an MQTT protocol. Using this protocol, the Pi makes the data available to other nodes in the network that request it.
The payload data is stored and updated by the Pi whenever it is sent by a node and sent whenever it is requested. 

## Adjusting indoor humidity:
In the winter, experts recommend maintaining about 50% humidity indoors. On very cold days, however, humidity might condense
on interior windows and walls, and the difference in humidity between indoors and outdoors might cause humidity to migrate
through walls. The humidity migrating across the walls would then condense as it approaches the cold outdoor temperature, causing
water (and eventually mold) to collect within the walls. HVAC professionals recommmend homeowners to decrease indoor humidity as
the exterior temperature decreases in order to reduce the difference between indoor and outdoor humidity.

Proper ajustment of indoor humidity therefor requires both indoor and outdoor temperature readings. This home automation project
1) takes indoor and outdoor temperature readings from DHT sensors
2) takes indoor humidity readings from a DHT sensor
3) calculates the recommended interior humidity level based on outdoor temperature
4) turns on a room humidifier if the humidity level is too low
5) turns off the room humidifier when the recommended humidity level is reached.

A complete description of hardware, Openhab, MQTT and MySensors setup is beyond the scope of this ReadMe. 

## Relay with Nano and Power Supply
Shown below: Project box containing solid state relay, 9v power supply, Arduino Nano, Nano IO board, and NRF24L01 radio module. The relay
turns the humidifier on and off. Of note, an extension cord was cut in half to provide a plug and socket. The humidifier plugs into the
socket end of the former extension cord. 

![ProjectBox](/images/HmdfSwBox.JPG)

## Schematic
Shown below: Partial schematic for the Arduino Nano, SSR relay and power supply. Radio module NRF24L01 and Nano IO board not shown.

![HmdfSwSchematic](/images/HmdfSwSchematic.png)
