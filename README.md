# HomeAssistant OCPP + Shelly 3em = load balacing

## TLDR;
- configuration.yaml includes the sensor templates that calculate the total power and current on the most loaded phase
- automations.yaml includes the automation for adjusting the charger current depending on the house load

## Setup notes
- [ABB Terra AC wallbox](https://new.abb.com/ev-charging/terra-ac-wallbox) is an affordable and well known EVSE with OCPP support.
  By default the charger is preconfigured to use an ABB cloud service for remote management and Apps. Unfortunately changing the OCPP server to your own needs some extra steps.
  
  You either need help from an electrician or a company or a friend who has experience with this charger or your ABB sales represetitive for following accounts: 
  * [TerraConfig Portal](https://abb.installer.chargedot.com) for setting up a custom OCPP profile
  * [TerraConfig APP](https://play.google.com/store/apps/details?id=com.abb.nebula) for downloading the OCPP profile to your charger
  * [Terra AC: TerraConfig App Step by Step Guide](https://library.e.abb.com/public/013efbe844a94afea2d989eb4291f9ed/TerraConfigApp%20Step%20by%20Step%20Guide.pdf)
  
  They are separate accounts tied to the same client, one is probably meant for service providers and the other for installers but to finish the configuration you need both.
    
    Example values for the OCPP profile:
    * Type: ws:// (this is an unsecure WebSocket version, not tested with the more secure wss://)
    * URL: 192.168.1.3:9000 (use your HomeAssistant server IP address)
    * Protocol Type: OCPP
    * Protocol Version: ocpp16j
 
  Use TerraConfig APP on the mobile device TerraConfig APP account to connect to the charger over Bluetooth and adding the charger using the chargers PIN code. You can then download the preconfigured OCPP profile to the charger.
  
- [Home Assistant OS](https://www.home-assistant.io/installation/generic-x86-64) runs on a small Intel NUC PC with 4G of RAM and 128GB SSD storage.
- [HACS](https://hacs.xyz/docs/configuration/basic/) offers community supported Integrations for HomeAssistant, we need it to add OCPP support.
- [OCPP Integration](https://github.com/lbbrhzn/ocpp) can be installed using HACS

After OCPP integration is set up the charger can connect to HomeAssistand and start sending statistics and polling commands. The two main features are Charger Availability that show whether the charger is in use or not. The other is Charger Maximum Current that adjusts the maximum allowed current for your charger.
