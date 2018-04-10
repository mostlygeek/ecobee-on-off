# ecobee-on-off
A little daemon that turns the ecobee on/off when the windows/doors are open.  This program is quite specific: 

1. Works with an [Envisalink](http://www.eyezon.com/?page_id=176) to check the state of sensors around the house
1. If certain sensors (windows, doors) are open it will turn off the ecobee
1. When windows/doors are closed it will turn the ecobee back on

This program is meant to let robots doing the boring work and stop heating/cooling the outside. :)

# Dev notes #

- [thermostat settings](https://www.ecobee.com/home/developer/api/documentation/v1/objects/Settings.shtml)
  - remember the current mode before setting to "off"
  - when reverting, set the mode back to <previous mode>
- use my forked [mostlygeek/etpi](https://github.com/mostlygeek/etpi) project for listening to events from the envisalink
  - should make a `status()`  update call to dump all the status of all the zones
  - should set the ecobee to `off` when:
    - any of the watched zones are OPEN for more than <timeout> 
    - make sure to remember the `thermostatRev` value .. 
  - should revert the ecobee to the previous mode when: 
    - thermostate mode is Off 
    - all the watched zones are "RESTORED", meaning they are closed
  
  
