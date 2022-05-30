# Create Your Own Garden Watering System in Home Assistant - TUTORIAL

<a href="https://youtu.be/EVpKdNLba4s" target="_blank"><img src="https://github.com/smarthomejunkie/Home-Assistant-Tutorials/blob/master/Create-Your-Own-Garden-Watering-System/Create-Your-Own-Garden-Watering-System-In-Home-Assistant-Tutorial-Thumb.png?raw=true"></a>

<a href="https://www.patreon.com/bePatron?u=50155158" target="_blank"><img src="https://github.com/smarthomejunkie/Home-Assistant-Tutorials/blob/master/become-a-patron.png?raw=true" alt="Become a Patron!"></a>

The instructions for this tutorial can be found [in this YouTube video](https://youtu.be/EVpKdNLba4s).

You can copy and paste the code used in this video, but please make sure that you replace the entities in this code by your own entities.

**The Template Sensors:**

```
- sensor:
    ##### Sprinkler Total Expected Precipitation ##################################
    - name: "Sprinkler Total Expected Precipitation"
      unique_id: 7f8aca37-be26-436d-9459-d82b6f9e96b1
      icon: mdi:weather-pouring
      unit_of_measurement: mm
      state: >
        {%- set totalprecipitation = 0 | float -%}
        {%- set ns = namespace() -%} 
        {%- set ns.totalprecipitation = 0 -%}
        {%- for daypart in range(0, 7) -%}
          {%- set precipitation = state_attr('weather.openweathermap', 'forecast')[daypart].precipitation -%} 
          {%- set precipitation_probability = state_attr('weather.openweathermap', 'forecast')[daypart].precipitation_probability / 100 %}
          {% if precipitation_probability > 0 -%}
            {%- set precipitation = precipitation * precipitation_probability -%}
          {%- endif -%}
          {%- set ns.totalprecipitation = ns.totalprecipitation + precipitation -%}
        {%- endfor %}
        {{ ns.totalprecipitation | float | round(0) }}

    ##### Sprinkler Total Rain Fallen Plus Expected ##################################
    - name: "Sprinkler Total Rain Fallen Plus Expected"
      unique_id: b0fafacb-9eda-463d-9ac9-bafd4d0c0a26
      icon: mdi:weather-pouring
      unit_of_measurement: mm
      state: >
        {{ (states('input_number.sprinkler_total_rain_fallen') | float + states('sensor.sprinkler_total_expected_precipitation') | float) | round(2) }}

    ##### Sprinkler Days Since Last Watering Day ##################################
    - name: "Sprinkler Days Since Last Watering Day"
      unique_id: 89b640e1-4234-4dc8-896f-24579c130199
      icon: mdi:calendar
      state: >
        {{ ((as_timestamp(now()) - as_timestamp(states("input_datetime.sprinkler_last_watering_day"))) / 86400) | float | round(2) }}

    ##### Sprinkler Current Temperature Is Higher ##################################
    - name: "Sprinkler Current Temperature Is Higher"
      unique_id: d6eba539-5ba5-49ed-bd15-27e8b0f21e3b
      icon: mdi:check
      state: >
        {%- if states('sensor.openweathermap_temperature') | float > states('input_number.sprinkler_maximum_temperature_measured') | float -%}
          true
        {%- else -%}
          false
        {%- endif %}
```

**The Automations:**

```
alias: 'Sprinkler: Add Current Rain to Total Rain Fallen'
description: ''
trigger:
  - platform: state
    entity_id:
      - sensor.openweathermap_rain
condition: []
action:
  - data_template:
      entity_id: input_number.sprinkler_total_rain_fallen
      value: >-
        {{ states("input_number.sprinkler_total_rain_fallen")|float +
        states("sensor.openweathermap_rain")|float }}
    service: input_number.set_value
mode: single
```

```
alias: 'Sprinkler: Check if Garden should be Watered'
description: ''
trigger:
  - platform: sun
    event: sunrise
    offset: 0
condition: []
action:
  - choose:
      - conditions:
          - condition: numeric_state
            entity_id: input_number.sprinkler_maximum_temperature_measured
            above: '31'
          - condition: numeric_state
            entity_id: sensor.sprinkler_total_rain_fallen_plus_expected
            below: '20.1'
        sequence:
          - service: input_number.set_value
            data:
              value: 90
            target:
              entity_id: input_number.sprinkler_watering_duration
          - service: script.sprinkler_water_the_garden
            data: {}
      - conditions:
          - condition: numeric_state
            entity_id: sensor.sprinkler_days_since_last_watering_day
            above: '2'
            below: '3'
          - condition: numeric_state
            entity_id: input_number.sprinkler_maximum_temperature_measured
            above: '26'
            below: '31.1'
          - condition: numeric_state
            entity_id: sensor.sprinkler_total_rain_fallen_plus_expected
            below: '15.1'
        sequence:
          - service: input_number.set_value
            data:
              value: 75
            target:
              entity_id: input_number.sprinkler_watering_duration
          - service: script.sprinkler_water_the_garden
            data: {}
      - conditions:
          - condition: numeric_state
            entity_id: sensor.sprinkler_days_since_last_watering_day
            above: '3'
            below: '4'
          - condition: numeric_state
            entity_id: input_number.sprinkler_maximum_temperature_measured
            above: '21'
            below: '26.1'
          - condition: numeric_state
            entity_id: sensor.sprinkler_total_rain_fallen_plus_expected
            below: '10.1'
        sequence:
          - service: input_number.set_value
            data:
              value: 60
            target:
              entity_id: input_number.sprinkler_watering_duration
          - service: script.sprinkler_water_the_garden
            data: {}
      - conditions:
          - condition: numeric_state
            entity_id: sensor.sprinkler_days_since_last_watering_day
            above: '3'
            below: '4'
          - condition: numeric_state
            entity_id: input_number.sprinkler_maximum_temperature_measured
            above: '15'
            below: '21.1'
          - condition: numeric_state
            entity_id: sensor.sprinkler_total_rain_fallen_plus_expected
            below: '10.1'
        sequence:
          - service: input_number.set_value
            data:
              value: 45
            target:
              entity_id: input_number.sprinkler_watering_duration
          - service: script.sprinkler_water_the_garden
            data: {}
      - conditions:
          - condition: numeric_state
            entity_id: sensor.sprinkler_days_since_last_watering_day
            above: '3'
            below: '4'
        sequence:
          - service: script.sprinkler_reset_helper_values
            data: {}
    default: []
mode: single
```

```
alias: 'Sprinkler: Check Maximum Temperature when Temperature Changes'
description: ''
trigger:
  - platform: state
    entity_id:
      - sensor.openweathermap_temperature
condition:
  - condition: state
    entity_id: sensor.sprinkler_current_temperature_is_higher
    state: 'true'
action:
  - service: input_number.set_value
    data_template:
      value: '{{ states(''sensor.openweathermap_temperature'') }}'
    target:
      entity_id: input_number.sprinkler_maximum_temperature_measured
mode: single
```

**The Scripts:**

```
alias: 'Sprinkler: Reset Helper Values'
sequence:
  - service: input_number.set_value
    data:
      value: 0
    target:
      entity_id:
        - input_number.sprinkler_total_rain_fallen
        - input_number.sprinkler_watering_duration
  - service: input_datetime.set_datetime
    entity_id: input_datetime.sprinkler_last_watering_day
    data_template:
      datetime: '{{ now() }}'
  - service: input_number.set_value
    data_template:
      value: '{{ states(''sensor.openweathermap_temperature'') }}'
    target:
      entity_id: input_number.sprinkler_maximum_temperature_measured
  - service: notify.mobile_app_iphone_x_ed
    data:
      message: Now resetting the Sprinkler values
mode: single
icon: mdi:refresh
```

```
alias: 'Sprinkler: Water the Garden'
sequence:
  - service: notify.mobile_app_iphone_x_ed
    data:
      message: >-
        Start watering the garden for {{
        states("input_number.sprinkler_watering_duration") | int }} minutes.
  - type: turn_on
    device_id: 8137a99e9f2fc80d6d0b0192ef801c0a
    entity_id: switch.sw_plug_2
    domain: switch
  - delay:
      minutes: |
        {{ states("input_number.sprinkler_watering_duration") | int }}
  - type: turn_off
    device_id: 8137a99e9f2fc80d6d0b0192ef801c0a
    entity_id: switch.sw_plug_2
    domain: switch
  - service: script.sprinkler_reset_helper_values
    data: {}
  - service: notify.mobile_app_iphone_x_ed
    data:
      message: Stopped Watering the Garden
mode: single
icon: mdi:sprinkler
```

## EXTRA

Some people asked me what would happen if Home Assistant reboots during watering. In that case, the sprinkler would go on forever, but you can easily circumvent this:

1. Create a toggle (input_boolean) helper: Sprinkler State
2. Change the script: **Sprinkler: Water the garden** to turn on the sprinkler state when the sprinkler starts:

```
alias: 'Sprinkler: Water the Garden'
sequence:
  - service: input_boolean.turn_on
    data: {}
    target:
      entity_id: input_boolean.sprinkler_state
  - service: notify.mobile_app_iphone_x_ed
    data:
      message: >-
        Start watering the garden for {{
        states("input_number.sprinkler_watering_duration") | int }} minutes.
  - type: turn_on
    device_id: 8137a99e9f2fc80d6d0b0192ef801c0a
    entity_id: switch.sw_plug_2
    domain: switch
  - delay:
      minutes: |
        {{ states("input_number.sprinkler_watering_duration") | int }}
  - type: turn_off
    device_id: 8137a99e9f2fc80d6d0b0192ef801c0a
    entity_id: switch.sw_plug_2
    domain: switch
  - service: script.sprinkler_reset_helper_values
    data: {}
  - service: notify.mobile_app_iphone_x_ed
    data:
      message: Stopped Watering the Garden
mode: single
icon: mdi:sprinkler
```
3. Change the script: **Sprinkler: Reset Helper Values** to turn off the sprinkler state too:

```
alias: 'Sprinkler: Reset Helper Values'
sequence:
  - service: input_number.set_value
    data:
      value: 0
    target:
      entity_id:
        - input_number.sprinkler_total_rain_fallen
        - input_number.sprinkler_watering_duration
  - service: input_datetime.set_datetime
    entity_id: input_datetime.sprinkler_last_watering_day
    data_template:
      datetime: '{{ now() }}'
  - service: input_number.set_value
    data_template:
      value: '{{ states(''sensor.openweathermap_temperature'') }}'
    target:
      entity_id: input_number.sprinkler_maximum_temperature_measured
  - service: input_boolean.turn_off
    data: {}
    target:
      entity_id: input_boolean.sprinkler_state
  - service: notify.mobile_app_iphone_x_ed
    data:
      message: Now resetting the Sprinkler values
mode: single
icon: mdi:refresh
```

4. Create an automation that checks if the sprinkler is still running if Home Assistant is rebooted and stop the sprinkler if that is the case:
```
alias: >-
  Sprinkler: Check if Sprinkler is still running after a reboot of Home
  Assistant
description: ''
trigger:
  - platform: homeassistant
    event: start
condition:
  - condition: state
    entity_id: input_boolean.sprinkler_state
    state: 'on'
action:
  - type: turn_off
    device_id: 8137a99e9f2fc80d6d0b0192ef801c0a
    entity_id: switch.sw_plug_2
    domain: switch
  - service: script.sprinkler_reset_helper_values
    data: {}
mode: single
```

If this helped and saved you time, you can support me by becoming my Patron or buy my a coffee (or two ;). I'd really appreciate that.

<a href="https://www.patreon.com/bePatron?u=50155158" target="_blank"><img src="https://github.com/smarthomejunkie/Home-Assistant-Tutorials/blob/master/become-a-patron.png?raw=true" alt="Become a Patron!"></a>

<a href="https://www.buymeacoffee.com/smarthomejunkie" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/default-blue.png" alt="Buy Me A Coffee" height="51" width="217" ></a>

## DISCLAIMER
* **NEVER REPLACE YOUR FILES BY THE FILES IN THIS REPOSITORY WITHOUT CREATING A BACKUP FIRST!**
* **THESE FILES CONTAIN ONLY PART OF THE CODE OF YOUR ORIGINAL FILES.**
* **ALWAYS COPY THE CODE IN THESE FILES AND PASTE THEM WITHIN YOUR ORIGINAL FILES.**
