# Alarm System files for Home Assistant

<a href="https://youtu.be/jh8l2K5oips" target="_blank"><img src="https://github.com/smarthomejunkie/Home-Assistant-Tutorials/raw/master/Alarm-System/Home-Assistant-Alarm-System-Thumb.png?raw=true"></a>

<a href="https://www.patreon.com/bePatron?u=50155158" target="_blank"><img src="https://github.com/smarthomejunkie/Home-Assistant-Tutorials/blob/master/become-a-patron.png?raw=true" alt="Become a Patron!"></a>

The instructions for this tutorial can be found [in this YouTube video](https://youtu.be/jh8l2K5oips).

View the list of my devices and the devices that I recommend [on this page](https://github.com/smarthomejunkie/MyDevices/)

## The Files:

* In the config folder you will find the code that you can add to your configuration.yaml
* In the config/www folder you will find the alarm1.mp3 file that you need for the Alarm system in Home Assistant. You can download it and store it in your own /config/www folder.

## The Automations:

```
alias: 'Alarm: Flash Lights when the Alarm is triggered'
description: ''
trigger:
  - platform: state
    entity_id: alarm_control_panel.home_alarm
    to: triggered
    id: alarm-is-triggered
  - platform: state
    entity_id: alarm_control_panel.home_alarm
    to: disarmed
    id: alarm-is-disarmed
    from: triggered
condition: []
action:
  - choose:
      - conditions:
          - condition: trigger
            id: alarm-is-triggered
        sequence:
          - repeat:
              until:
                - condition: state
                  entity_id: alarm_control_panel.home_alarm
                  state: disarmed
              sequence:
                - service: light.turn_on
                  data:
                    color_name: red
                    brightness_pct: 100
                  target:
                    entity_id: light.alarm_lights
                - delay:
                    hours: 0
                    minutes: 0
                    seconds: 0
                    milliseconds: 500
                - service: light.turn_off
                  data: {}
                  target:
                    entity_id: light.alarm_lights
                - delay:
                    hours: 0
                    minutes: 0
                    seconds: 0
                    milliseconds: 500
      - conditions:
          - condition: trigger
            id: alarm-is-disarmed
        sequence:
          - service: light.turn_on
            data:
              color_name: sienna
              brightness_pct: 70
            target:
              entity_id: light.alarm_lights
    default: []
mode: restart
```

```
alias: 'Alarm: Send notification when the alarm got triggered'
description: ''
trigger:
  - platform: state
    entity_id: alarm_control_panel.home_alarm
    to: triggered
condition: []
action:
  - service: notify.mobile_app_iphone_x_ed
    data:
      message: Possible Intruder detected!
      title: Alarm is triggered
mode: single
```

```
alias: 'Alarm: Sound Siren when the Alarm is Triggered'
description: ''
trigger:
  - platform: state
    entity_id: alarm_control_panel.home_alarm
    to: triggered
    id: alarm-is-triggered
  - platform: state
    entity_id: alarm_control_panel.home_alarm
    to: disarmed
    id: alarm-is-disarmed
    from: triggered
condition: []
action:
  - choose:
      - conditions:
          - condition: trigger
            id: alarm-is-triggered
        sequence:
          - service: media_player.volume_set
            data:
              volume_level: 1
            target:
              entity_id: media_player.alarm_speakers
          - repeat:
              until:
                - condition: state
                  entity_id: alarm_control_panel.home_alarm
                  state: disarmed
              sequence:
                - service: media_player.play_media
                  data:
                    media_content_id: http://192.168.68.132:8123/local/alarm1.mp3
                    media_content_type: music
                  target:
                    entity_id: media_player.speaker_group
                - delay:
                    hours: 0
                    minutes: 0
                    seconds: 10
                    milliseconds: 0
      - conditions:
          - condition: trigger
            id: alarm-is-disarmed
        sequence:
          - service: media_player.media_stop
            data: {}
            target:
              entity_id: media_player.speaker_group
          - service: media_player.volume_set
            data:
              volume_level: 0.4
            target:
              entity_id: media_player.speaker_group
    default: []
mode: restart
```

```
alias: 'Alarm: Trigger Alarm when Armed Away'
description: ''
trigger:
  - platform: state
    entity_id: binary_sensor.alarm_motion_sensors
    to: 'on'
condition:
  - condition: state
    entity_id: alarm_control_panel.home_alarm
    state: armed_away
action:
  - service: alarm_control_panel.alarm_trigger
    data: {}
    target:
      entity_id: alarm_control_panel.home_alarm
mode: single
```

If this helped and saved you time, you can support me by becoming my Patron. I'd really appreciate that.

<a href="https://www.patreon.com/bePatron?u=50155158" target="_blank"><img src="https://github.com/smarthomejunkie/Home-Assistant-Tutorials/blob/master/become-a-patron.png?raw=true" alt="Become a Patron!"></a>

<a href="https://www.buymeacoffee.com/smarthomejunkie" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/default-blue.png" alt="Buy Me A Coffee" height="51" width="217" ></a>

## DISCLAIMER
* **NEVER REPLACE YOUR FILES BY THE FILES IN THIS REPOSITORY WITHOUT CREATING A BACKUP FIRST!**
* **THESE FILES CONTAIN ONLY PART OF THE CODE OF YOUR ORIGINAL FILES.**
* **ALWAYS COPY THE CODE IN THESE FILES AND PASTE THEM WITHIN YOUR ORIGINAL FILES.**
