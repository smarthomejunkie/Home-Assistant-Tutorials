# Dwains Dashboard with Mushroom cards - In-DEPTH TUTORIAL

<a href="https://youtu.be/6hemFbrJuk8" target="_blank"><img src="https://github.com/smarthomejunkie/Home-Assistant-Tutorials/raw/master/Dwains-Dashboard-In-Depth/Dwains-Dashboard-In-Depth-Tutorial-thumbnail.png?raw=true"></a>

The instructions for this tutorial can be found [in this YouTube video](https://youtu.be/6hemFbrJuk8).

The code for the mushroom template card to change the icon is:

```
{% if is_state('binary_sensor.office_motion_sensor_occupancy','off') %}
  mdi:motion-sensor-off
{% else %}
  mdi:motion-sensor
{% endif %}
```

The code for the mushroom template card to change the icon-color is:

```
{% if is_state('binary_sensor.office_motion_sensor_occupancy','off') %}
  grey
{% else %}
  light-green
{% endif %}
```

The code for the mushroom template card to show the last triggered time is:

```
Triggered: {{ as_timestamp(states.binary_sensor.office_motion_sensor_occupancy.last_changed) | timestamp_custom(' %H:%M',true | int)}}
```

The code for the slider button-card is:

```
type: custom:slider-button-card
entity: climate.office_front
slider:
  direction: left-right
  background: solid
  use_state_color: false
  use_percentage_bg_opacity: false
  show_track: true
  toggle_on_click: false
  force_square: false
show_name: true
show_state: true
compact: false
icon:
  show: true
  use_state_color: false
  tap_action:
    action: more-info
  icon: ''
action_button:
  mode: toggle
  icon: mdi:power
  show: false
  show_spinner: true
  tap_action:
    action: toggle
```

If this helped and saved you time, you can support me by becoming my Patron. I'd really appreciate that.

<a href="https://www.patreon.com/bePatron?u=50155158" target="_blank"><img src="https://github.com/smarthomejunkie/Home-Assistant-Tutorials/blob/master/become-a-patron.png?raw=true" alt="Become a Patron!"></a>

<a href="https://www.buymeacoffee.com/smarthomejunkie" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/default-blue.png" alt="Buy Me A Coffee" height="51" width="217" ></a>

## DISCLAIMER
* **NEVER REPLACE YOUR FILES BY THE FILES IN THIS REPOSITORY WITHOUT CREATING A BACKUP FIRST!**
* **THESE FILES CONTAIN ONLY PART OF THE CODE OF YOUR ORIGINAL FILES.**
* **ALWAYS COPY THE CODE IN THESE FILES AND PASTE THEM WITHIN YOUR ORIGINAL FILES.**
