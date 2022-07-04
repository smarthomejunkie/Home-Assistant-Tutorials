# Zemismart Smart Super Curtain Robot Motor - Product Review

<a href="https://youtu.be/c1cnccmgl3k" target="_blank"><img src="https://github.com/smarthomejunkie/Home-Assistant-Tutorials/blob/master/Zemismart-Smart-Super-Curtain-Robot-Motor/Zemismart-Smart-Super-Curtain-Robot-Motor-thumb.png?raw=true"></a>

<a href="https://www.patreon.com/bePatron?u=50155158" target="_blank"><img src="https://github.com/smarthomejunkie/Home-Assistant-Tutorials/blob/master/become-a-patron.png?raw=true" alt="Become a Patron!"></a>

The product review can be found [in this YouTube video](https://youtu.be/8tXyjVQEF8o).

View the list of my devices and the devices that I recommend [on this page](https://github.com/smarthomejunkie/MyDevices/)

You can copy and paste the code used in this video

**The code to add to the configuration.yaml of Zigbee2MQTT:**

```
advanced:
  log_level: debug
external_converters:
  - TS0601.js
```

**The code to add to the TS0601.js file:**
```
const tz = require('zigbee-herdsman-converters/converters/toZigbee');
const exposes = require('zigbee-herdsman-converters/lib/exposes');
const tuya = require('zigbee-herdsman-converters/lib/tuya');

const fzDeviceSpecific = {
    cluster: 'manuSpecificTuya',
    type: ['commandSetDataResponse', 'commandGetData'],
    convert: (model, msg, publish, options, meta) => {
        const dp = msg.data.dp;
        const value = tuya.getDataValue(msg.data.datatype, msg.data.data);

        switch (dp) {
        case tuya.dataPoints.state: // Confirm opening/closing/stopping (triggered from Zigbee)
        case tuya.dataPoints.coverPosition: // Started moving to position (triggered from Zigbee)
        case tuya.dataPoints.coverChange: // Started moving (triggered by transmitter or pulling on curtain)
        case tuya.dataPoints.coverArrived: { // Arrived at position
            const running = dp === tuya.dataPoints.coverArrived ? false : true;
            return {running}; // Position does not seem to be working, so respective code removed
        }
        case tuya.dataPoints.config: // Returned by configuration set; ignore
            break;
        case 13: // Battery; apparently only sent when triggered via hardware remote?
            return {battery: value};
        default: // Unknown code
            meta.logger.warn(`ZM85EL-2Z: Unhandled DP #${dp}: ${JSON.stringify(msg.data)}`);
        }
    },
}

const definition = {
    fingerprint: [{modelID: 'TS0601', manufacturerName: '_TZE200_nw1r9hp6'}],
    model: 'ZM85EL-2Z',
    vendor: 'Zemismart',
    description: 'Zigbee/RF curtain motor',
    fromZigbee: [fzDeviceSpecific],
    toZigbee: [tz.tuya_cover_control],
    exposes: [
        exposes.cover(),
        exposes.presets.battery(),
    ],
    meta: {
        configureKey: 1,
        battery: {dontDividePercentage: true}
    },
};

module.exports = definition;
```

If this helped and saved you time, you can support me by becoming my Patron or buy my a coffee (or two ;). I'd really appreciate that.

<a href="https://www.patreon.com/bePatron?u=50155158" target="_blank"><img src="https://github.com/smarthomejunkie/Home-Assistant-Tutorials/blob/master/become-a-patron.png?raw=true" alt="Become a Patron!"></a>

<a href="https://www.buymeacoffee.com/smarthomejunkie" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/default-blue.png" alt="Buy Me A Coffee" height="51" width="217" ></a>

## DISCLAIMER
* **NEVER REPLACE YOUR FILES BY THE FILES IN THIS REPOSITORY WITHOUT CREATING A BACKUP FIRST!**
* **THESE FILES CONTAIN ONLY PART OF THE CODE OF YOUR ORIGINAL FILES.**
* **ALWAYS COPY THE CODE IN THESE FILES AND PASTE THEM WITHIN YOUR ORIGINAL FILES.**
