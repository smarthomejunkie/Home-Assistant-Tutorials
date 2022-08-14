# Scenes on Steroids in Home Assistant - How To -Tutorial!

<a href="https://youtu.be/JW9PC6ptXcM" target="_blank"><img src="https://github.com/smarthomejunkie/Home-Assistant-Tutorials/blob/master/Scenes-on-steroids-in-Home-Assistant-How-To-Tutorial/Scenes-on-steroids-in-Home-Assistant-How-To-Tutorial-thumb.jpg?raw=true"></a>

<a href="https://www.patreon.com/bePatron?u=50155158" target="_blank"><img src="https://github.com/smarthomejunkie/Home-Assistant-Tutorials/blob/master/become-a-patron.png?raw=true" alt="Become a Patron!"></a>

The instructions for this tutorial can be found [in this YouTube video](https://youtu.be/JW9PC6ptXcM) and [in this blog post](https://www.smarthomejunkie.net/scenes-on-steroids-in-home-assistant-how-to-tutorial).

View the list of my devices and the devices that I recommend [on this page](https://github.com/smarthomejunkie/MyDevices/)

You can copy and paste the code used in this video, but please make sure that you replace the entities in this code by your own entities.
This code is here for your convenience and works 100% if everything is installed correctly. If something is not working in your install, please review your installation to see what might be missing in your setup.

## The Automations:

**Switch Work and Movie Scene**

```
alias: "Scene: Switch Work and Movie Scenes"
description: ""
trigger:
  - platform: time
    at: "09:00:00"
    id: Work
  - platform: time
    at: "19:00:00"
condition: []
action:
  - if:
      - condition: trigger
        id: Work
    then:
      - service: scene.turn_on
        target:
          entity_id: scene.work_scene
        metadata: {}
    else:
      - service: scene.turn_on
        target:
          entity_id: scene.movie_scene
        metadata: {}
mode: single
```

**Switch when window opens and closes**

```
alias: "Scene: Switch when window opens and closes"
description: ""
trigger:
  - type: opened
    platform: device
    device_id: c7b116979b5782b9d954814563d77247
    entity_id: binary_sensor.aqara_door_sensor_contact
    domain: binary_sensor
    id: Window Opened
  - type: not_opened
    platform: device
    device_id: c7b116979b5782b9d954814563d77247
    entity_id: binary_sensor.aqara_door_sensor_contact
    domain: binary_sensor
condition: []
action:
  - if:
      - condition: trigger
        id: Window Opened
    then:
      - service: scene.create
        data:
          scene_id: before
          snapshot_entities:
            - climate.office_front
            - light.office_back
      - service: climate.set_temperature
        data:
          temperature: 10
        target:
          entity_id: climate.office_front
      - service: light.turn_on
        data:
          color_name: blue
        target:
          entity_id: light.office_back
    else:
      - service: scene.turn_on
        data: {}
        target:
          entity_id: scene.before
mode: single

``` 

⭐⭐⭐

If this helped and saved you time, you can support me by becoming my Patron, buy my a coffee or join my channel. I'd really appreciate that.

<a href="https://www.patreon.com/bePatron?u=50155158" target="_blank"><img src="https://github.com/smarthomejunkie/Home-Assistant-Tutorials/blob/master/become-a-patron.png?raw=true" width="217" alt="Become a Patron!"></a>

<a href="https://www.buymeacoffee.com/smarthomejunkie" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/default-blue.png" alt="Buy Me A Coffee" height="51" width="217" ></a>

<a href="https://www.youtube.com/c/smarthomejunkie/join" target="_blank"><img src="https://github.com/smarthomejunkie/Home-Assistant-Tutorials/blob/master/Join-Logo.png?raw=true" width="217" alt="Join my Channel!"></a>

⭐ Join my Discord server at: https://discord.gg/at8v5hW ⭐

⭐⭐⭐


## DISCLAIMER
* **NEVER REPLACE YOUR FILES BY THE FILES IN THIS REPOSITORY WITHOUT CREATING A BACKUP FIRST!**
* **THESE FILES CONTAIN ONLY PART OF THE CODE OF YOUR ORIGINAL FILES.**
* **ALWAYS COPY THE CODE IN THESE FILES AND PASTE THEM WITHIN YOUR ORIGINAL FILES.**
