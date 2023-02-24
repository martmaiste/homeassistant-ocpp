# HomeAssistant OCPP + Shelly 3em load balacing

## TLDR;
- configuration.yaml includes the sensor templates that calculate the total power and current on the most loaded phase
- automations.yaml includes the automation for adjusting the charger current depending on the house load

## Setup notes
- [ABB Terra AC wallbox](https://new.abb.com/ev-charging/terra-ac-wallbox) is an affordable and well known EVSE with OCPP support.
  This EVSE is preconfigured to use ABB cloud service for remote management and Apps. For connecting the charger with your own OCPP server you need to contact your ABB sales representitive and ask for:
  * TerraConfig Portal account and
  * TerraConfig APP account.
  
  They are two separate accounts, one is probably meant for service providers and the other for installers. 
  
  * TerraConfig Portal account allows to set up the OCPP connection profile in the TerraConfig Portal.
    
    Example values for the profile:
    * Type: ws:// (this is an unsecure WebSocket version, not tested with the more secure wss://)
    * URL: 192.168.1.3:9000 (use your HomeAssistant server IP address)
    * Protocol Type: OCPP
    * Protocol Version: ocpp16j
  * TerraConfig APP account. Use TerraConfig APP on the mobile device with this account to connect to the charger over Bluetooth using the chargers PIN code. You can download the preconfigured OCPP connection profile to the charger using the APP.
- [Home Assistant OS](https://www.home-assistant.io/installation/generic-x86-64) runs on a small Intel NUC PC with 4G of RAM and 128GB SSD storage.
- [HACS](https://hacs.xyz/docs/configuration/basic/) offers community supported Integrations for HomeAssistant, we need it to add OCPP support.
- [OCPP Integration](https://github.com/lbbrhzn/ocpp) can be installed using HACS

