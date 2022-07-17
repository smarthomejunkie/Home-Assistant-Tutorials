# How to use Motion Sensors in Home Assistant

<a href="https://youtu.be/m_fbo_Co-TU" target="_blank"><img src="https://github.com/smarthomejunkie/Home-Assistant-Tutorials/blob/master/How-To-Use-Motion-Sensors-In-Home-Assistant/How-To-Use-Motion-Sensors-In-Home-Assistant-Tutorial-thumb.png?raw=true"></a>

<a href="https://www.patreon.com/bePatron?u=50155158" target="_blank"><img src="https://github.com/smarthomejunkie/Home-Assistant-Tutorials/blob/master/become-a-patron.png?raw=true" alt="Become a Patron!"></a>

The instructions for this tutorial can be found [in this YouTube video](https://youtu.be/m_fbo_Co-TU) and [in this blog post](https://www.smarthomejunkie.net/how-to-use-motion-sensors-in-home-assistant).

View the list of my devices and the devices that I recommend [on this page](https://github.com/smarthomejunkie/MyDevices/)

You can copy and paste the code used in this video, but please make sure that you replace the entities in this code by your own entities.
This code is here for your convenience and works 100% if everything is installed correctly. If something is not working in your install, please review your installation to see what might be missing in your setup.

**The Automations:**

```
alias: 'Motion Sensor Tutorial 1: 1 Room with 1 Motion Sensor and 1 Lamp'
description: ''
trigger:
  - type: motion
    platform: device
    device_id: eb4fbfb584c8c9ad7fba6b1a8ba963c3
    entity_id: binary_sensor.motion_detector_room_1_occupancy
    domain: binary_sensor
    id: motion-detected
  - type: no_motion
    platform: device
    device_id: eb4fbfb584c8c9ad7fba6b1a8ba963c3
    entity_id: binary_sensor.motion_detector_room_1_occupancy
    domain: binary_sensor
    for:
      hours: 0
      minutes: 5
      seconds: 0
condition: []
action:
  - if:
      - condition: trigger
        id: motion-detected
    then:
      - type: turn_on
        device_id: 32bcf104a4d155b6c092c427d76d85dd
        entity_id: light.room_1
        domain: light
    else:
      - type: turn_off
        device_id: 32bcf104a4d155b6c092c427d76d85dd
        entity_id: light.room_1
        domain: light
mode: single
```

```
alias: >-
  Motion Sensor Tutorial 2: 2 Rooms with 1 Motion Sensor and 1 Lamp for each
  room
description: ''
trigger:
  - type: motion
    platform: device
    device_id: eb4fbfb584c8c9ad7fba6b1a8ba963c3
    entity_id: binary_sensor.motion_detector_hall_outside_occupancy
    domain: binary_sensor
    id: motion-detected-outside
  - type: motion
    platform: device
    device_id: 7f5c77c81262df5f74fb4110f34bd371
    entity_id: binary_sensor.motion_detector_hall_inside_occupancy
    domain: binary_sensor
    id: motion-detected-inside
    for:
      hours: 0
      minutes: 0
      seconds: 0
  - type: no_motion
    platform: device
    device_id: eb4fbfb584c8c9ad7fba6b1a8ba963c3
    entity_id: binary_sensor.motion_detector_hall_outside_occupancy
    domain: binary_sensor
    id: motion-stopped-outside
    for:
      hours: 0
      minutes: 0
      seconds: 0
  - type: no_motion
    platform: device
    device_id: 7f5c77c81262df5f74fb4110f34bd371
    entity_id: binary_sensor.motion_detector_hall_inside_occupancy
    domain: binary_sensor
    id: motion-stopped-inside
    for:
      hours: 0
      minutes: 0
      seconds: 0
condition: []
action:
  - choose:
      - conditions:
          - condition: trigger
            id: motion-detected-outside
        sequence:
          - type: turn_on
            device_id: 32bcf104a4d155b6c092c427d76d85dd
            entity_id: light.hall_outside
            domain: light
          - type: turn_on
            device_id: 0ab60e7c39c3e96a2e1d09fb1bb8653d
            entity_id: light.hall_inside
            domain: light
      - conditions:
          - condition: trigger
            id: motion-stopped-outside
        sequence:
          - type: turn_off
            device_id: 32bcf104a4d155b6c092c427d76d85dd
            entity_id: light.hall_outside
            domain: light
      - conditions:
          - condition: trigger
            id: motion-detected-inside
        sequence:
          - type: turn_on
            device_id: 0ab60e7c39c3e96a2e1d09fb1bb8653d
            entity_id: light.hall_inside
            domain: light
      - conditions:
          - condition: trigger
            id: motion-stopped-inside
        sequence:
          - type: turn_off
            device_id: 0ab60e7c39c3e96a2e1d09fb1bb8653d
            entity_id: light.hall_inside
            domain: light
    default: []
mode: single
```

```
alias: >-
  Motion Sensor Tutorial 3: 3 Rooms with 1 Motion Sensor and 1 Lamp for each
  room
description: ''
trigger:
  - type: motion
    platform: device
    device_id: eb4fbfb584c8c9ad7fba6b1a8ba963c3
    entity_id: binary_sensor.motion_detector_staircase_occupancy
    domain: binary_sensor
    id: motion-detected-staircase
  - type: motion
    platform: device
    device_id: 7f5c77c81262df5f74fb4110f34bd371
    entity_id: binary_sensor.motion_detector_boiler_room_occupancy
    domain: binary_sensor
    id: motion-detected-boiler-room
  - type: motion
    platform: device
    device_id: acb452cc3debf864ffb9b934bbf00172
    entity_id: binary_sensor.motion_detector_garage_occupancy
    domain: binary_sensor
    id: motion-detected-garage
  - type: no_motion
    platform: device
    device_id: eb4fbfb584c8c9ad7fba6b1a8ba963c3
    entity_id: binary_sensor.motion_detector_staircase_occupancy
    domain: binary_sensor
    id: motion-stopped-staircase
    for:
      hours: 0
      minutes: 0
      seconds: 0
  - type: no_motion
    platform: device
    device_id: 7f5c77c81262df5f74fb4110f34bd371
    entity_id: binary_sensor.motion_detector_boiler_room_occupancy
    domain: binary_sensor
    id: motion-stopped-boiler-room
    for:
      hours: 0
      minutes: 0
      seconds: 0
  - type: no_motion
    platform: device
    device_id: acb452cc3debf864ffb9b934bbf00172
    entity_id: binary_sensor.motion_detector_garage_occupancy
    domain: binary_sensor
    id: motion-stopped-garage
    for:
      hours: 0
      minutes: 0
      seconds: 0
condition: []
action:
  - choose:
      - conditions:
          - condition: trigger
            id: motion-detected-staircase
        sequence:
          - type: turn_on
            device_id: 32bcf104a4d155b6c092c427d76d85dd
            entity_id: light.staircase
            domain: light
          - type: turn_on
            device_id: 0ab60e7c39c3e96a2e1d09fb1bb8653d
            entity_id: light.boiler_room
            domain: light
      - conditions:
          - condition: trigger
            id: motion-detected-boiler-room
        sequence:
          - type: turn_on
            device_id: 32bcf104a4d155b6c092c427d76d85dd
            entity_id: light.staircase
            domain: light
          - type: turn_on
            device_id: 0ab60e7c39c3e96a2e1d09fb1bb8653d
            entity_id: light.boiler_room
            domain: light
          - type: turn_on
            device_id: 8d67b2e29ca479f123fe93e1d239406c
            entity_id: light.garage
            domain: light
      - conditions:
          - condition: trigger
            id: motion-detected-garage
        sequence:
          - type: turn_on
            device_id: 8d67b2e29ca479f123fe93e1d239406c
            entity_id: light.garage
            domain: light
      - conditions:
          - condition: trigger
            id: motion-stopped-staircase
        sequence:
          - type: turn_off
            device_id: 32bcf104a4d155b6c092c427d76d85dd
            entity_id: light.staircase
            domain: light
      - conditions:
          - condition: trigger
            id: motion-stopped-boiler-room
        sequence:
          - type: turn_off
            device_id: 0ab60e7c39c3e96a2e1d09fb1bb8653d
            entity_id: light.boiler_room
            domain: light
      - conditions:
          - condition: trigger
            id: motion-stopped-garage
        sequence:
          - type: turn_off
            device_id: 8d67b2e29ca479f123fe93e1d239406c
            entity_id: light.garage
            domain: light
    default: []
mode: single
```

If this helped and saved you time, you can support me by becoming my Patron, buy my a coffee or join my channel. I'd really appreciate that.

<a href="https://www.patreon.com/bePatron?u=50155158" target="_blank"><img src="https://github.com/smarthomejunkie/Home-Assistant-Tutorials/blob/master/become-a-patron.png?raw=true" alt="Become a Patron!"></a>

<a href="https://www.buymeacoffee.com/smarthomejunkie" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/default-blue.png" alt="Buy Me A Coffee" height="51" width="217" ></a>

<a href="https://www.youtube.com/c/smarthomejunkie/join" target="_blank"><img src="https://github.com/smarthomejunkie/Home-Assistant-Tutorials/blob/master/Join-Logo.png?raw=true" alt="Join my Channel!"></a>


## DISCLAIMER
* **NEVER REPLACE YOUR FILES BY THE FILES IN THIS REPOSITORY WITHOUT CREATING A BACKUP FIRST!**
* **THESE FILES CONTAIN ONLY PART OF THE CODE OF YOUR ORIGINAL FILES.**
* **ALWAYS COPY THE CODE IN THESE FILES AND PASTE THEM WITHIN YOUR ORIGINAL FILES.**
