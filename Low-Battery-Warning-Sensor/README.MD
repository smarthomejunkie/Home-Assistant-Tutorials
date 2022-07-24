# Create your own Low Battery Warning Sensor - TUTORIAL

<a href="https://youtu.be/VgV_ExVeSfE" target="_blank"><img src="https://github.com/smarthomejunkie/Home-Assistant-Tutorials/raw/master/Low-Battery-Warning-Sensor/Low-Battery-Warning-Sensor-In-Home-Assistant-Thumb.png?raw=true"></a>

<a href="https://www.patreon.com/bePatron?u=50155158" target="_blank"><img src="https://github.com/smarthomejunkie/Home-Assistant-Tutorials/blob/master/become-a-patron.png?raw=true" alt="Become a Patron!"></a>

The instructions for this tutorial can be found [in this YouTube video](https://youtu.be/VgV_ExVeSfE) and [in this blog post](https://www.smarthomejunkie.net/create-your-own-low-battery-warning-sensor-in-home-assistant-tutorial/).

View the list of my devices and the devices that I recommend [on this page](https://github.com/smarthomejunkie/MyDevices/)

The Sensor Template code :

```
- sensor:
    ##### Low Battery list ##################################
    - name: "Low Battery Devices"
      unique_id: ba292875-ae67-480d-9867-29cdb20afaea
      icon: >
        mdi:battery-low
      state: >
        {% set threshold = states('input_number.battery_threshold') | int %}
        {%- set ns = namespace(sensors=[]) -%}
        {%- for state in states.sensor 
          | selectattr('attributes.device_class', 'defined') 
          | selectattr('attributes.state_class', 'defined') 
          | selectattr('attributes.device_class', '==', 'battery') 
          | selectattr('attributes.state_class', '==', 'measurement') 
          | selectattr('state', 'is_number') -%}
          {%- if state.state | int <= threshold -%}
            {% set ns.sensors = ns.sensors + [dict(name = state.name | replace(' battery', '') | replace(' Battery', ''), state = state.state | int)] %}
          {%- endif -%}
        {%- endfor -%}
        {%- set batt = ns.sensors | sort(attribute='state') %}
        {%- set ns = namespace(batt='') -%}
        {%- for state in batt -%}
            {% set ns.batt= ns.batt + (state.name  ~ ' (' ~ state.state ~'%)' ~ "\n") %}
        {%- endfor -%}

        {% if ns.batt | count > 0 %}
          {{ ns.batt | truncate(255, true, '...') }}
        {% else %}
          {{ 'unavailable' }}
        {% endif %}
```

The code for the Conditional Card on the dashboard:

```
{{states('sensor.low_battery_devices')}}
```

Visit my YouTube channel: [Smart Home Junkie](https://www.youtube.com/c/SmartHomeJunkie)

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
