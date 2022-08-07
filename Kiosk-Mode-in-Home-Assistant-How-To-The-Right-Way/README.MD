# Kiosk Mode in Home Assistant – How To – The Right Way!

<a href="https://youtu.be/G3lT4zgjER8" target="_blank"><img src="https://github.com/smarthomejunkie/Home-Assistant-Tutorials/blob/master/Kiosk-Mode-in-Home-Assistant-How-To-The-Right-Way/Kiosk-Mode-In-Home-Assistant-thumb.jpg?raw=true"></a>

<a href="https://www.patreon.com/bePatron?u=50155158" target="_blank"><img src="https://github.com/smarthomejunkie/Home-Assistant-Tutorials/blob/master/become-a-patron.png?raw=true" alt="Become a Patron!"></a>

The instructions for this tutorial can be found [in this YouTube video](https://youtu.be/G3lT4zgjER8) and [in this blog post](https://www.smarthomejunkie.net/kiosk-mode-in-home-assistant-the-right-way).

View the list of my devices and the devices that I recommend [on this page](https://github.com/smarthomejunkie/MyDevices/)

You can copy and paste the code used in this video, but please make sure that you replace the entities in this code by your own entities.
This code is here for your convenience and works 100% if everything is installed correctly. If something is not working in your install, please review your installation to see what might be missing in your setup.

## The Code:

**First simple code:**

```
kiosk_mode:
  non_admin_settings:
    kiosk: true
    ignore_entity_settings: true
```

**Second step: switch kiosk mode on and off**

```
kiosk_mode:
  non_admin_settings:
    kiosk: true
    ignore_entity_settings: true
  entity_settings:
    - entity:
        input_boolean.kiosk_mode: 'on'
      hide_header: true
    - entity:
        input_boolean.kiosk_mode: 'off'
      hide_header: false
``` 

**Third step: hide buttons for non-admins**

```
type: custom:state-switch
entity: group
states:
  admin:
    type: custom:mushroom-chips-card
    chips:
      - type: menu
      - type: template
        icon: |
          {% if is_state('input_boolean.kiosk_mode','on') %}
            mdi:arrow-expand-vertical
          {% else %}
            mdi:arrow-collapse-up
          {% endif %}
        icon_color: light-green
        tap_action:
          action: call-service
          service: input_boolean.toggle
          data: {}
          target:
            entity_id: input_boolean.kiosk_mode
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
