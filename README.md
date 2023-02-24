# HomeAssistant OCPP + Shelly 3em load balacing

## TLDR;
- configuration.yaml includes the sensor templates that calculate the total power and current on the most loaded phase
- automations.yaml includes the automation for adjusting the charger current depending on the house load

## Hardware and software

- HomeAssistant runs on a small Intel NUC PC with 4G of RAM and 128GB SSD storage. The operating system is Home Assistant OS.[Installation instructions](https://www.home-assistant.io/installation/generic-x86-64)
