# How to Restore Light State at Restart of  Home Assistant

<a href="https://youtu.be/m_fbo_Co-TU" target="_blank"><img src="https://github.com/smarthomejunkie/Home-Assistant-Tutorials/blob/master/How-To-Use-Motion-Sensors-In-Home-Assistant/How-To-Restore-Light-State-At-Restart-Of-Home-Assistant-thumb.jpg?raw=true"></a>

<a href="https://www.patreon.com/bePatron?u=50155158" target="_blank"><img src="https://github.com/smarthomejunkie/Home-Assistant-Tutorials/blob/master/become-a-patron.png?raw=true" alt="Become a Patron!"></a>

The instructions for this tutorial can be found [in this YouTube video](https://youtu.be/SxEHslRKqrw) and [in this blog post](https://www.smarthomejunkie.net/how-to-restore-light-state-at-restart-of-home-assistant).

View the list of my devices and the devices that I recommend [on this page](https://github.com/smarthomejunkie/MyDevices/)

You can copy and paste the code used in this video, but please make sure that you replace the entities in this code by your own entities.
This code is here for your convenience and works 100% if everything is installed correctly. If something is not working in your install, please review your installation to see what might be missing in your setup.

**The Automations:**

```
alias: 'Light: Monitor Light Status Office Front Left'
description: ''
trigger:
  - platform: device
    type: changed_states
    device_id: bc8762684309669a2d90d027dde70e2c
    entity_id: light.office_front_left
    domain: light
condition: []
action:
  - if:
      - condition: device
        type: is_on
        device_id: bc8762684309669a2d90d027dde70e2c
        entity_id: light.office_front_left
        domain: light
    then:
      - service: input_boolean.turn_on
        data: {}
        target:
          entity_id: input_boolean.office_light_front_left_status
    else:
      - service: input_boolean.turn_off
        data: {}
        target:
          entity_id: input_boolean.office_light_front_left_status
mode: single
```

```
alias: 'Light: Restore Light Status at Restart'
description: ''
trigger:
  - platform: homeassistant
    event: start
condition: []
action:
  - if:
      - condition: state
        entity_id: input_boolean.office_light_front_left_status
        state: 'on'
    then:
      - type: turn_on
        device_id: bc8762684309669a2d90d027dde70e2c
        entity_id: light.office_front_left
        domain: light
    else:
      - type: turn_off
        device_id: bc8762684309669a2d90d027dde70e2c
        entity_id: light.office_front_left
        domain: light
mode: single

```

⭐⭐⭐

If this helped and saved you time, you can support me by becoming my Patron, buy my a coffee or join my channel. I'd really appreciate that.

<a href="https://www.patreon.com/bePatron?u=50155158" target="_blank"><img src="https://github.com/smarthomejunkie/Home-Assistant-Tutorials/blob/master/become-a-patron.png?raw=true" alt="Become a Patron!"></a>

<a href="https://www.buymeacoffee.com/smarthomejunkie" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/default-blue.png" alt="Buy Me A Coffee" height="51" width="217" ></a>

<a href="https://www.youtube.com/c/smarthomejunkie/join" target="_blank"><img src="https://github.com/smarthomejunkie/Home-Assistant-Tutorials/blob/master/Join-Logo.png?raw=true" alt="Join my Channel!"></a>

⭐⭐⭐

⭐ Join my Discord server at: https://discord.gg/at8v5hW ⭐


## DISCLAIMER
* **NEVER REPLACE YOUR FILES BY THE FILES IN THIS REPOSITORY WITHOUT CREATING A BACKUP FIRST!**
* **THESE FILES CONTAIN ONLY PART OF THE CODE OF YOUR ORIGINAL FILES.**
* **ALWAYS COPY THE CODE IN THESE FILES AND PASTE THEM WITHIN YOUR ORIGINAL FILES.**
