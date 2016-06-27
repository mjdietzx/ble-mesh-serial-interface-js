ble-mesh-serial-interface-js
=========

An npm package for Node.js that provides an API to control a router node in a BLE mesh network via the serial port.

## Installation

  `npm install ble-mesh-serial-interface-js`

## Usage

```javascript
'use strict';

const BLEMeshSerialInterface = require('./index');

const MESH_ACCESS_ADDR = 0x8E89BED6;
const MESH_INTERVAL_MIN_MS = 100;
const MESH_CHANNEL = 38;

const bleMeshSerialInterfaceAPI = new BLEMeshSerialInterface('COM45', err => {
  bleMeshSerialInterfaceAPI.init(MESH_ACCESS_ADDR, MESH_INTERVAL_MIN_MS, MESH_CHANNEL, err => {
    if (err) {
      console.log(err);
    }
    console.log('device initialized');
    bleMeshSerialInterfaceAPI.valueSet(0, new Buffer([0x00, 0x01, 0x02]), err => {
      if (err) {
        console.log(err);
      }
      console.log('valueSet() handle = 0, value = [0, 1, 2]');
      bleMeshSerialInterfaceAPI.valueGet(0, (err, res) => {
        if (err) {
          console.log(err);
        }
        console.log('valueGet() res: ', res);
        bleMeshSerialInterfaceAPI.radioReset(err => {
          if (err) {
            console.log(err);
          }
          console.log('device reset');
        });
      });
    });
  });
});
```

## Tests

  `npm test`

## Contributing

In lieu of a formal style guide, take care to maintain the existing coding style. Add unit tests for any new or changed functionality. Lint and test your code.
