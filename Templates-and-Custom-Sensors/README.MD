# Templates and Custom Sensors in Home Assistant

The instructions for this tutorial can be found [in this YouTube video](https://youtu.be/cdz32TLu_gw).

If this helped and saved you time, you can support me by becoming my Patron. I'd really appreciate that.
Please visit [Patreon](https://www.patreon.com/smarthomejunkie) to sponsor me.

The custom sensor code used in the video is:
 

	##### Count number of lights on ##################################
	- platform: template
	  sensors:
	    number_lights_on:
	      friendly_name: Number Lights On
	      value_template: >-
	        {{ states.light 
	                  | rejectattr('attributes.is_deconz_group', 'eq', true)
	                  | rejectattr('attributes.entity_id', 'defined') 
	                  | selectattr('state', 'eq', 'on')
	                  | list | count }}
	      icon_template: mdi:lightbulb-group

	##### Battery Kitchen ##################################
	- platform: template
	  sensors:
	    battery_status_kitchen:
	      friendly_name: Battery Status Kitchen
	      value_template: >-
	        {{ states('sensor.kitchen_motion_sensor_battery_level') }}
	      icon_template: >-
	        {% set batterylevel = states('sensor.kitchen_motion_sensor_battery_level') | int %}
	        {% if batterylevel == 100 %}
	          mdi:battery
	        {% else %}
	          mdi:battery-{{batterylevel}}
	        {% endif %}
	      unit_of_measurement: "%"
	      

## DISCLAIMER
* **NEVER REPLACE YOUR FILES BY THE FILES IN THIS REPOSITORY WITHOUT CREATING A BACKUP FIRST!**
* **THESE FILES CONTAIN ONLY PART OF THE CODE OF YOUR ORIGINAL FILES.**
* **ALWAYS COPY THE CODE IN THESE FILES AND PASTE THEM WITHIN YOUR ORIGINAL FILES.**

<a href="https://www.buymeacoffee.com/smarthomejunkie" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/default-blue.png" alt="Buy Me A Coffee" height="51" width="217" ></a>
