# WebBLE

Initial partial implementation of the [Web Bluetooth](https://webbluetoothcg.github.io/web-bluetooth/) 
spec for iOS, originally forked from [Paul Thierault](https://github.com/pauljt)'s [original implementation](https://github.com/pauljt/BleBrowser).

WebBLE is licensed under the Apache Version 2.0 License as per the [LICENSE](LICENSE) file.

### Distributions

-  [WebBLE](https://apps.apple.com/gb/app/webble/id1193531073) was the first distribution and the one that I (daphtdazz) maintain and support. Purchasing this is the best way to support the project.

Others are available on the app store which provide varying levels of support / alternative features.

> If you would like to add your distribution to this list then please send a PR, but it should provide some extra functionality over WebBLE and not just be a direct clone.


## Supported APIs v1.0

### `navigator.bluetooth`

- `.requestDevice(options)`
  - `options.acceptAllDevices = true` to ask for any device
  - `options.filters` is a list of filters (mutually exclusive with `acceptAllDevices`) with properties
    - `name`: devices with the given name will be included
    - `namePrefix`: devices with names with this prefix will be included
    - `services`: list of service aliases or uuids.

### `BluetoothDevice`

- `.id`
- `.name`
- `.gatt`
- `.gattserverdisconnected: EventHandler`

### `BluetoothRemoteGATTServer`

- `.connected`
- `.connect()`
- `.disconnect()`
- `.getPrimaryService(uuid)`
- `.getPrimaryServices()`

### `BluetoothRemoteGATTService`

- `.uuid`
- `.device`
- `.getCharacteristic(uuid)`
- `.getCharacteristics`

### `BluetoothRemoteGATTCharacteristic`

- `.service`
- `.uuid`
- `.value`
- `.readValue()`
- `.writeValue(value)`
- `.writeValueWithoutResponse(value)`
- `.oncharacteristicvaluechanged: EventHandler`
- `.startNotifications()`
- `.stopNotifications()`
- `.addEventListener()`
- `.removeEventListener()`

Everything else is TBD!

## Development

Info if you want to add features / fix bugs in the project.

### Setup

If you want to build and run locally, you just have to do the following:

- Set your `DEVELOPMENT_TEAM` ID in Locations -> Custom Paths as per [this stackoverflow](https://stackoverflow.com/questions/39669661/how-to-prevent-xcode-8-from-saving-development-team-in-pbxproj/40424891#40424891) answer, which is to avoid pushing personal / conflicting team IDs to github. 

### Testing

The [end-to-end "device" tests](DeviceTests/) are run semi-manually before WebBLE versions are released to the App Store.

> 💡 Just run a simple http server from the root of the codebase using e.g `python3 -m http.server` and navigate to your machine's address on your network to run these tests in webble on your iOS device

Currently there are no unit tests... partly because it's time-consuming and difficult to write meaningful unit tests since there are three things to test: the javascript APIs, the native glue layer and the actual behaviour of a bluetooth device at the other end. Instead end-to-end tests which require some real devices to be used are hosted [here](https://www.greenparksoftware.co.uk/projects/webble/pucktest), and these tests are run / fixed before new versions of [WebBLE](https://apps.apple.com/gb/app/webble/id1193531073) are released to the App store.

If you are maintaining your own release you can use those tests or write your own. If you want to spend the effort to start adding actual unit tests then that would be marvellous.

> 💡 If you have a device you'd like me to add tests for please get in contact with me!
