# Afvalwijzer code for Home Assistant
This is the **step by step copy and paste code** you need for the integration of Afvalwijzer in Home Assistant. 

![](screenshot.png?raw=true)

All credits for coding the integration go to [Xirixiz](https://github.com/xirixiz/Home-Assistant-Sensor-Afvalwijzer). 
I did not write this integration. I just created some code for you to copy and paste to make it look nice in Home Assistant. 

If this helped and saved you time, you can support me by becoming my Patron. I'd really appreciate that.

<a href="https://www.patreon.com/bePatron?u=50155158" target="_blank"><img src="https://github.com/smarthomejunkie/Home-Assistant-Tutorials/blob/master/become-a-patron.png?raw=true" alt="Become a Patron!"></a>

Supported services are:

* mijnafvalwijzer
* afvalstoffendienstkalender (all)
* rova
* acv
* almere
* areareiniging
* avalex
* avri
* bar
* hellendoorn
* meerlanden
* meppel
* rad
* twentemilieu
* waardlanden
* westland
* ximmio
* reinis
* alkmaar
* alphenaandenrijn
* berkelland
* blink
* cranendonck
* cyclus
* dar
* denhaag
* gad
* hvc
* lingewaard
* middelburgngen
* montfoort
* peelenmaas
* prezero
* purmerend
* rmn
* schouwenand
* spaarnelanden
* sudwestfryslan
* suez
* venray
* voorschoten
* waalre
* zrd

1. Please make sure you've installed [HACS](https://youtu.be/BNQw--FCp24)
2. Install [Afvalwijzer](https://github.com/xirixiz/Home-Assistant-Sensor-Afvalwijzer) with HACS. (Module written by [xirixiz](https://github.com/xirixiz))
2. With HACS you can install [hui-element](https://github.com/thomasloven/lovelace-hui-element) and [auto-enttities](https://github.com/thomasloven/lovelace-auto-entities) which are needed to position some of the elements in your lovelace dashboard.
3. Restart Home Assistant after you've installed the HACS plugins.
4. Copy the code in the config folder of this repository to your own configuration.yaml and customize.yaml. 
5. Copy the images in the config/www folder in this repository to your own config/www folder.
6. Add the code in the entries_for_lovelace.yaml in this repository to your own lovelace dashboard in a Manual Custom card.

If this code helped you in any way, you can support me by subscribing to my YouTube channel. You will find loads of other interesting tutorials there.
Visit my YouTube channel: [Smart Home Junkie](https://www.youtube.com/channel/UCVtQ4AOSmCFUuvixddYiSxw)

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
