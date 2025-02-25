[![NPM](https://nodei.co/npm/react-native-qrcode-svg.png)](https://npmjs.org/package/react-native-qrcode-svg)
![circleci](https://circleci.com/gh/awesomejerry/react-native-qrcode-svg.svg?style=shield&circle-token=185bdd4fed561139178638f5b9f9c48ddefc9288)

# react-native-qrcode-svg

A QR Code generator for React Native based on react-native-svg and javascript-qrcode.

Discussion: https://discord.gg/RvFM97v

## Features

* Easily render QR code images
* Optionally embed a logotype

<img src="https://raw.githubusercontent.com/awesomejerry/react-native-qrcode-svg/master/screenshot/android.png" width="150">
<img src="https://raw.githubusercontent.com/awesomejerry/react-native-qrcode-svg/master/screenshot/ios.png" width="150">

## Installation

Please install react-native-svg first.
```
npm install react-native-svg --save
react-native link react-native-svg
npm install react-native-qrcode-svg --save
```

## Examples

```
import QRCode from 'react-native-qrcode-svg';

//Simple usage, defaults for all but the value
render() {
  return (
    <QRCode
      value="http://awesome.link.qr"
    />
  );
};

```

```
// 30px logo from base64 string with transparent background
render() {
  let base64Logo = 'data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAOEAA..';
  return (
    <QRCode
      value="Just some string value"
      logo={{uri: base64Logo}
      logoSize={30}
      logoBackgroundColor='transparent'
    />
  );
};

```

```
// 20% (default) sized logo from local file string with white logo backdrop
render() {
  let logoFromFile = require('../assets/logo.png');
  return (
    <QRCode
      value="Just some string value"
      logo={logoFromFile}
    />
  );
};

```

```
// get base64 string encode of the qrcode (currently logo is not included)
getDataURL() {
  this.svg.toDataURL(this.callback);
}
callback(dataURL) {
  console.log(dataURL);
}
render() {
  return (
    <QRCode
      value="Just some string value"
      getRef={(c) => (this.svg = c)}
    />
  );
}
```


## Props

Name            | Default    | Description
----------------|------------|--------------
size            | 100        | Size of rendered image in pixels
value           | 'this is a QR code' | Value of the QR code
color           | 'black'        | Color of the QR code
backgroundColor | 'white'        | Color of the background
logo | null        | Image source object. Ex. {uri: 'base64string'} or {require('pathToImage')}
logoSize | 20% of size | Size of the imprinted logo. Bigger logo = less error correction in QR code
logoBackgroundColor | backgroundColor        | The logo gets a filled quadratic background with this color. Use 'transparent' if your logo already has its own backdrop.
logoMargin | 2 | logo's distance to its wrapper
logoBorderRadius | 0 | the border-radius of logo image (Android is not supported)
getRef          | null       | Get SVG ref for further usage
ecl             | 'M'        | Error correction level
onError(error)  | undefined  | Callback fired when exception happened during the code generating process


## Saving generated code to gallery
 _Note: Experimental only ( not tested on iOS) , uses getRef() and needs [RNFS module](https://github.com/itinance/react-native-fs)_

npm install --save react-native-fs

### Example for Android:
```
import { CameraRoll , ToastAndroid } from "react-native"
import RNFS from "react-native-fs"
...

  saveQrToDisk() {
   	this.svg.toDataURL((data) => {
   		RNFS.writeFile(RNFS.CachesDirectoryPath+"/some-name.png", data, 'base64')
   		  .then((success) => {
   			  return CameraRoll.saveToCameraRoll(RNFS.CachesDirectoryPath+"/some-name.png", 'photo')
   		  })
   		  .then(() => {
   			  this.setState({ busy: false, imageSaved: true  })
   			  ToastAndroid.show('Saved to gallery !!', ToastAndroid.SHORT)
   		  })
   	})
  }
```


## Dependencies

### PeerDependencies

* [react-native-svg](https://github.com/magicismight/react-native-svg)

### Dependencies

* [node-qrcode](https://github.com/soldair/node-qrcode)

---

If you like this project, please consider buy me a coffee :)

https://www.buymeacoffee.com/LquC7mid5

