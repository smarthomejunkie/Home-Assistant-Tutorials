# Mailbox automation code for Home Assistant

<a href="https://www.youtube.com/watch?v=-4KGdPh6ur0" target="_blank"><img src="https://github.com/smarthomejunkie/Home-Assistant-Tutorials/blob/master/Mailbox-Automation/Youve-Got-Mail-In-Home-Assistant-thumb.png?raw=true"></a>

<a href="https://www.patreon.com/bePatron?u=50155158" target="_blank"><img src="https://github.com/smarthomejunkie/Home-Assistant-Tutorials/blob/master/become-a-patron.png?raw=true" alt="Become a Patron!"></a>

The instructions for this tutorial can be found [in this YouTube video](https://www.youtube.com/watch?v=-4KGdPh6ur0).

Get the [Aqara Door Sensor](https://s.click.aliexpress.com/e/_A26g2H)

## NEW WAY OF CREATING TEMPLATE SENSORS
At the time when I created the video, there was a different (old) way of creating template sensors. In the meantime, a new modern way is developed. The code below uses the new modern way of using template sensors. The video is still valid, but you should use the new approach if you use a templates.yaml file.

**Step 1:** Create a templates.yaml file in your config folder
**Step 2:** Add the following line to your configuration.yaml:

```
template: !include templates.yaml
```
**Step 3:** Add the following code to your templates.yaml:

```
- sensor:
    #### Mailbox Sensor ##################################
    - name: Mailbox Last Triggered Formatted
      state: >
        {% if (
            (( as_timestamp(now()) | timestamp_custom("%m%d")) | int) - ((as_timestamp(states("input_datetime.mailbox_last_triggered")) | timestamp_custom("%m%d")) | int)
            ) == 0 -%}
          {{ as_timestamp(states("input_datetime.mailbox_last_triggered")) | timestamp_custom("%H:%M") }}
        {%- else -%}
          none
        {%- endif %}
```
**Step 5:** Add the following code to your lovelace dashboard manual card:

```
type: 'custom:button-card'
entity: input_boolean.mail_arrived
color: white
show_state: false
tap_action: none
state:
  - value: 'on'
    color: yellow
    icon: 'mdi:mailbox'
    name: |
      [[[
        var time_delivered = states["sensor.mailbox_last_triggered_formatted"].state;
        return 'Mail delivered at ' + time_delivered 
      ]]]
  - value: 'off'
    icon: 'mdi:mailbox-open-up-outline'
    name: No mail today!
```

** MAKE SURE THAT YOU DO NOT HAVE ANY TEMPLATE SENSOR SEFINITIONS IN YOUR CONFIGURATION.YAML OR SENSORS.YAML ANYMORE IF YOU USE THE TEMPLATES.YAML

If this helped and saved you time, you can support me by becoming my Patron or buy my a coffee (or two ;). I'd really appreciate that.

<a href="https://www.patreon.com/bePatron?u=50155158" target="_blank"><img src="https://github.com/smarthomejunkie/Home-Assistant-Tutorials/blob/master/become-a-patron.png?raw=true" alt="Become a Patron!"></a>

<a href="https://www.buymeacoffee.com/smarthomejunkie" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/default-blue.png" alt="Buy Me A Coffee" height="51" width="217" ></a>

## DISCLAIMER
* **NEVER REPLACE YOUR FILES BY THE FILES IN THIS REPOSITORY WITHOUT CREATING A BACKUP FIRST!**
* **THESE FILES CONTAIN ONLY PART OF THE CODE OF YOUR ORIGINAL FILES.**
* **ALWAYS COPY THE CODE IN THESE FILES AND PASTE THEM WITHIN YOUR ORIGINAL FILES.**
