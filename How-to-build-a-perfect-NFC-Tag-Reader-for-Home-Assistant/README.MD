# How to build a perfect NFC Tag Reader for Home Assistant

<a href="https://youtu.be/16Es-JRaeGg" target="_blank"><img src="https://github.com/smarthomejunkie/Home-Assistant-Tutorials/blob/master/How-to-build-a-perfect-NFC-Tag-Reader-for-Home-Assistant/How-to-build-a-perfect-NFC-Tag-Reader-for-Home-Assistant-thumb.png?raw=true"></a>

<a href="https://www.patreon.com/bePatron?u=50155158" target="_blank"><img src="https://github.com/smarthomejunkie/Home-Assistant-Tutorials/blob/master/become-a-patron.png?raw=true" alt="Become a Patron!"></a>

The instructions for this tutorial can be found [in this YouTube video](https://youtu.be/16Es-JRaeGg) and [in this blog post](https://www.smarthomejunkie.net/how-to-build-a-perfect-nfc-tag-reader-for-home-assistant).

View the list of my devices and the devices that I recommend [on this page](https://github.com/smarthomejunkie/MyDevices/)

You can copy and paste the code used in this video, but please make sure that you replace the entities in this code by your own entities.
This code is here for your convenience and works 100% if everything is installed correctly. If something is not working in your install, please review your installation to see what might be missing in your setup.

**The Automations:**

```
alias: 'Tag: Arm and Disarm alarm'
description: ''
trigger:
  - platform: tag
    tag_id: 23-D1-81-A1
    id: tag-detected
  - platform: tag
    tag_id: 23-E2-79-12
    id: tag-detected
condition: []
action:
  - if:
      - condition: state
        entity_id: alarm_control_panel.home_alarm
        state: disarmed
    then:
      - service: alarm_control_panel.alarm_arm_away
        data: {}
        target:
          entity_id: alarm_control_panel.home_alarm
    else:
      - service: alarm_control_panel.alarm_disarm
        data:
          code: '1234'
        target:
          entity_id: alarm_control_panel.home_alarm
mode: restart
```

```
alias: 'Tag: Arm and Disarm alarm'
description: ''
trigger:
  - platform: tag
    tag_id: 23-D1-81-A1
    id: tag-detected
  - platform: tag
    tag_id: 23-E2-79-12
    id: tag-detected
condition: []
action:
  - if:
      - condition: state
        entity_id: alarm_control_panel.home_alarm
        state: disarmed
    then:
      - service: alarm_control_panel.alarm_arm_away
        data: {}
        target:
          entity_id: alarm_control_panel.home_alarm
    else:
      - service: alarm_control_panel.alarm_disarm
        data:
          code: '1234'
        target:
          entity_id: alarm_control_panel.home_alarm
mode: restart
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
