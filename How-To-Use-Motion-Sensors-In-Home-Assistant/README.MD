# How to use Motion Sensors in Home Assistant

<a href="https://youtu.be/m_fbo_Co-TU" target="_blank"><img src="https://github.com/smarthomejunkie/Home-Assistant-Tutorials/blob/master/How-To-Use-Motion-Sensors-In-Home-Assistant/How-To-Use-Motion-Sensors-In-Home-Assistant-Tutorial-thumb.png?raw=true"></a>

<a href="https://www.patreon.com/bePatron?u=50155158" target="_blank"><img src="https://github.com/smarthomejunkie/Home-Assistant-Tutorials/blob/master/become-a-patron.png?raw=true" alt="Become a Patron!"></a>

The instructions for this tutorial can be found [in this YouTube video](https://youtu.be/m_fbo_Co-TU) and [in this blog post](https://www.smarthomejunkie.net/how-to-use-motion-sensors-in-home-assistant).

View the list of my devices and the devices that I recommend [on this page](https://github.com/smarthomejunkie/MyDevices/)

You can copy and paste the code used in this video, but please make sure that you replace the entities in this code by your own entities.
This code is here for your convenience and works 100% if everything is installed correctly. If something is not working in your install, please review your installation to see what might be missing in your setup.

The code used in this video [can be downloaded here](https://ko-fi.com/s/11a4bf8abc).


# Extra Use Cases:

**Use Case 4: Turn off the lights if someone approached the house and decides not to go in**

Currently, in Use Case 2, if someone approaches the house, the lights outside and inside turn on. If he decides not to enter the house,
only the outside light will turn off. To fix this use case, we have to add a Helper Group of type binary sensor to Home Assistant. Let's call the Helper Group "all motion sensors hall". Add the motion sensor for the hall outside and the motion sensor for the hall inside to this group. Leave the setting "All entities" to off.

Now, create an automation that turns off all lights if all motion sensors stopped detecting motion for 5 minutes.

**Use Case 5: Turn off the lights if someone only enters the boiler room, does not enter the garage, and goes back upstairs**

Currently, in Use Case 3, if someone enters the boiler room, the lights in the staircase, boiler room, and garage turn on. If he decides not to enter the garage, only the light in the boiler room and staircase will turn off. The light in the garage will stay turned on. To fix this use case, we have to add a Helper Group of type binary sensor to Home Assistant. Let's call the Helper Group "all motion sensors". Add the motion sensor for the staircase, the boiler room, and the garage to this group. Leave the setting "All entities" to off.

Now, create an automation that turns off all lights if all motion sensors stopped detecting motion for 5 minutes.


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
