# Adaptive Lighting in Home Assistant - TUTORIAL

<a href="https://youtu.be/c1cnccmgl3k" target="_blank"><img src="https://github.com/smarthomejunkie/Home-Assistant-Tutorials/blob/master/Adaptive-Lighting-In-Home-Assistant/Adaptive-Lighting-In-Home-Assistant-Tutorial-Thumb.png?raw=true"></a>

<a href="https://www.patreon.com/bePatron?u=50155158" target="_blank"><img src="https://github.com/smarthomejunkie/Home-Assistant-Tutorials/blob/master/become-a-patron.png?raw=true" alt="Become a Patron!"></a>

The instructions for this tutorial can be found [in this YouTube video](https://youtu.be/c1cnccmgl3k).

You can copy and paste the code used in this video, but please make sure that you replace the entities in this code by your own entities.
This code is here for your convenience and works 100% if everything is installed correctly. If something is not working in your install, please review your installation and check the sensors in your Developer Tools to see what might be missing in your setup.

**The Automation:**

```
alias: 'Light: Toggle Hallway lights on motion'
description: >-
  Toggle lights and set color temperature and brightness to bright during the
  day and to cosy during the night.
trigger:
  - type: motion
    platform: device
    device_id: ffba233ac2e7f65649e80d71dd97a849
    entity_id: binary_sensor.hall_downstairs_motion_sensor_occupancy
    domain: binary_sensor
    id: motion-detected
  - type: no_motion
    platform: device
    device_id: ffba233ac2e7f65649e80d71dd97a849
    entity_id: binary_sensor.hall_downstairs_motion_sensor_occupancy
    domain: binary_sensor
    id: motion-stopped
    for:
      hours: 0
      minutes: 5
      seconds: 0
condition: []
action:
  - choose:
      - conditions:
          - condition: trigger
            id: motion-detected
          - condition: state
            entity_id: sun.sun
            state: above_horizon
        sequence:
          - service: light.turn_on
            data:
              kelvin: 4000
              brightness_pct: 100
            target:
              entity_id: light.hall_downstairs
      - conditions:
          - condition: trigger
            id: motion-detected
          - condition: state
            entity_id: sun.sun
            state: below_horizon
        sequence:
          - service: light.turn_on
            data:
              kelvin: 2400
              brightness_pct: 50
            target:
              entity_id: light.hall_downstairs
      - conditions:
          - condition: trigger
            id: motion-stopped
        sequence:
          - service: light.turn_off
            data: {}
            target:
              entity_id: light.hall_downstairs
    default: []
mode: single

```



If this helped and saved you time, you can support me by becoming my Patron or buy my a coffee (or two ;). I'd really appreciate that.

<a href="https://www.patreon.com/bePatron?u=50155158" target="_blank"><img src="https://github.com/smarthomejunkie/Home-Assistant-Tutorials/blob/master/become-a-patron.png?raw=true" alt="Become a Patron!"></a>

<a href="https://www.buymeacoffee.com/smarthomejunkie" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/default-blue.png" alt="Buy Me A Coffee" height="51" width="217" ></a>

## DISCLAIMER
* **NEVER REPLACE YOUR FILES BY THE FILES IN THIS REPOSITORY WITHOUT CREATING A BACKUP FIRST!**
* **THESE FILES CONTAIN ONLY PART OF THE CODE OF YOUR ORIGINAL FILES.**
* **ALWAYS COPY THE CODE IN THESE FILES AND PASTE THEM WITHIN YOUR ORIGINAL FILES.**
