# Custom QR Code

[![Version](https://img.shields.io/npm/v/custom-qr-code.svg)](https://www.npmjs.org/package/custom-qr-code)

JavaScript library for generating QR codes with a logo and styling.

This is a fork of the currently unmaintained [repository by kozakdenys](https://github.com/kozakdenys/qr-code-styling) & [repository by KillianB](https://github.com/KilianB/styled-qr-code) fixing multiple issues:

- [#49](https://github.com/kozakdenys/qr-code-styling/issues/105) [#105 QR code is not valid by some scanners](https://github.com/kozakdenys/qr-code-styling/issues/105)
- outdated dependencies
- release for es2017
- migrated from webpack to vite
- added support for react (`import { CustomQRCode } from 'custom-qr-code/react'`)

Try the old version here https://qr-code-styling.com to get a feel

### Examples

<p float="left">
<img style="display:inline-block" src="https://raw.githubusercontent.com/kozakdenys/qr-code-styling/master/src/assets/facebook_example_new.png" width="240" />
<img style="display:inline-block" src="https://raw.githubusercontent.com/kozakdenys/qr-code-styling/master/src/assets/qr_code_example.png" width="240" />
<img style="display:inline-block" src="https://raw.githubusercontent.com/kozakdenys/qr-code-styling/master/src/assets/telegram_example_new.png" width="240" />
</p>

### Installation

```
npm install custom-qr-code
```

or

```
yarn add custom-qr-code
```

### Usage

**React**

```tsx
import { CustomQRCode } from 'custom-qr-code/react'

export const App = () => {
    return (
        <CustomQRCode
            {....{
                width: 300,
                height: 300,
                type: "svg",
                data: "https://www.facebook.com/",
                image: "https://upload.wikimedia.org/wikipedia/commons/5/51/Facebook_f_logo_%282019%29.svg",
                dotsOptions: {
                    color: "#4267b2",
                    type: "rounded"
                },
                backgroundOptions: {
                    color: "#e9ebee",
                },
                imageOptions: {
                    crossOrigin: "anonymous",
                    margin: 20
                }
            }}
        />
    )
}
```

**Classic:**

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>QR Code Styling</title>
    <script type="text/javascript" src="https://unpkg.com/qr-code-styling@1.5.0/lib/qr-code-styling.js"></script>
</head>
<body>
<div id="canvas"></div>
<script type="text/javascript">

    const qrCode = new CustomQRCode({
        width: 300,
        height: 300,
        type: "svg",
        data: "https://www.facebook.com/",
        image: "https://upload.wikimedia.org/wikipedia/commons/5/51/Facebook_f_logo_%282019%29.svg",
        dotsOptions: {
            color: "#4267b2",
            type: "rounded"
        },
        backgroundOptions: {
            color: "#e9ebee",
        },
        imageOptions: {
            crossOrigin: "anonymous",
            margin: 20
        }
    });

    qrCode.append(document.getElementById("canvas"));
    qrCode.download({ name: "qr", extension: "svg" });
</script>
</body>
</html>
```

---

[**React example (Codesandbox)**](https://codesandbox.io/s/qr-code-styling-react-example-l8rwl?file=/src/App.js)

[**Angular example (Codesandbox)**](https://codesandbox.io/s/agitated-panini-tpgb2?file=/src/app/app.component.ts)

---

[**React example (source)**](https://github.com/kozakdenys/qr-code-styling-examples/tree/master/examples/react)

[**Angular example (source)**](https://github.com/kozakdenys/qr-code-styling-examples/tree/master/examples/angular)

[**Vue example (source)**](https://github.com/kozakdenys/qr-code-styling-examples/tree/master/examples/vue)

---

### API Documentation

#### CustomQRCode instance

`new QRCodeStyling(options) => QRCodeStyling`

| Param   | Type   | Description |
| ------- | ------ | ----------- |
| options | object | Init object |

`options` structure

| Property                | Type                      | Default Value | Description                                                                                   |
| ----------------------- | ------------------------- | ------------- | --------------------------------------------------------------------------------------------- |
| width                   | number                    | `300`         | Size of canvas                                                                                |
| height                  | number                    | `300`         | Size of canvas                                                                                |
| type                    | string (`'canvas' 'svg'`) | `canvas`      | The type of the element that will be rendered                                                 |
| data                    | string                    |               | The date will be encoded to the QR code                                                       |
| image                   | string                    |               | The image will be copied to the center of the QR code                                         |
| margin                  | number                    | `0`           | Margin around canvas                                                                          |
| qrOptions               | object                    |               | Options will be passed to `qrcode-generator` lib                                              |
| imageOptions            | object                    |               | Specific image options, details see below                                                     |
| dotsOptions             | object                    |               | Dots styling options                                                                          |
| cornersSquareOptions    | object                    |               | Square in the corners styling options                                                         |
| cornersDotOptionsHelper | object                    |               | Dots in the corners styling options                                                           |
| backgroundOptions       | object                    |               | QR background styling options                                                                 |
| useLegacyDotRotation    | boolean                   | false         | Use the mirrored qr creation strategy of the original library. (Some scanners might not work) |

`options.qrOptions` structure

| Property             | Type                                               | Default Value |
| -------------------- | -------------------------------------------------- | ------------- |
| typeNumber           | number (`0 - 40`)                                  | `0`           |
| mode                 | string (`'Numeric' 'Alphanumeric' 'Byte' 'Kanji'`) |
| errorCorrectionLevel | string (`'L' 'M' 'Q' 'H'`)                         | `'Q'`         |

`options.imageOptions` structure

| Property           | Type                                    | Default Value | Description                                                                    |
| ------------------ | --------------------------------------- | ------------- | ------------------------------------------------------------------------------ |
| hideBackgroundDots | boolean                                 | `true`        | Hide all dots covered by the image                                             |
| imageSize          | number                                  | `0.4`         | Coefficient of the image size. Not recommended to use ove 0.5. Lower is better |
| margin             | number                                  | `0`           | Margin of the image in px                                                      |
| crossOrigin        | string(`'anonymous' 'use-credentials'`) | `anonymous`   |                                                                                |

`options.dotsOptions` structure

| Property | Type                                                                           | Default Value | Description         |
| -------- | ------------------------------------------------------------------------------ | ------------- | ------------------- |
| color    | string                                                                         | `'#000'`      | Color of QR dots    |
| gradient | object                                                                         |               | Gradient of QR dots |
| type     | string (`'rounded' 'dots' 'classy' 'classy-rounded' 'square' 'extra-rounded'`) | `'square'`    | Style of QR dots    |

`options.backgroundOptions` structure

| Property | Type   | Default Value |
| -------- | ------ | ------------- |
| color    | string | `'#fff'`      |
| gradient | object |

`options.cornersSquareOptions` structure

| Property | Type                                      | Default Value | Description                |
| -------- | ----------------------------------------- | ------------- | -------------------------- |
| color    | string                                    |               | Color of Corners Square    |
| gradient | object                                    |               | Gradient of Corners Square |
| type     | string (`'dot' 'square' 'extra-rounded'`) |               | Style of Corners Square    |

`options.cornersDotOptions` structure

| Property | Type                      | Default Value | Description             |
| -------- | ------------------------- | ------------- | ----------------------- |
| color    | string                    |               | Color of Corners Dot    |
| gradient | object                    |               | Gradient of Corners Dot |
| type     | string (`'dot' 'square'`) |               | Style of Corners Dot    |

Gradient structure

`options.dotsOptions.gradient`

`options.backgroundOptions.gradient`

`options.cornersSquareOptions.gradient`

`options.cornersDotOptions.gradient`

| Property   | Type                         | Default Value | Description                                                                            |
| ---------- | ---------------------------- | ------------- | -------------------------------------------------------------------------------------- |
| type       | string (`'linear' 'radial'`) | "linear"      | Type of gradient spread                                                                |
| rotation   | number                       | 0             | Rotation of gradient in radians (Math.PI === 180 degrees)                              |
| colorStops | array of objects             |               | Gradient colors. Example `[{ offset: 0, color: 'blue' }, { offset: 1, color: 'red' }]` |

Gradient colorStops structure

`options.dotsOptions.gradient.colorStops[]`

`options.backgroundOptions.gradient.colorStops[]`

`options.cornersSquareOptions.gradient.colorStops[]`

`options.cornersDotOptions.gradient.colorStops[]`

| Property | Type             | Default Value | Description                         |
| -------- | ---------------- | ------------- | ----------------------------------- |
| offset   | number (`0 - 1`) |               | Position of color in gradient range |
| color    | string           |               | Color of stop in gradient range     |

#### QRCodeStyling methods

`QRCodeStyling.append(container) => void`

| Param     | Type        | Description                                              |
| --------- | ----------- | -------------------------------------------------------- |
| container | DOM element | This container will be used for appending of the QR code |

`QRCodeStyling.getRawData(extension) => Promise<Blob>`

| Param     | Type                                 | Default Value | Description |
| --------- | ------------------------------------ | ------------- | ----------- |
| extension | string (`'png' 'jpeg' 'webp' 'svg'`) | `'png'`       | Blob type   |

`QRCodeStyling.update(options) => void`

| Param   | Type   | Description                            |
| ------- | ------ | -------------------------------------- |
| options | object | The same options as for initialization |

`QRCodeStyling.download(downloadOptions, quality) => Promise<void>`

| Param           | Type   | Description                                                                                                                                                                                                                                                                                                 |
| --------------- | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| downloadOptions | object | Options with extension and name of file (not required)                                                                                                                                                                                                                                                      |
| quality         | number | A Number between 0 and 1 indicating the image quality to be used when creating images using file formats that support lossy compression (such as image/jpeg or image/webp). A user agent will use its default quality value if this option is not specified, or if the number is outside the allowed range. |

`downloadOptions` structure

| Property  | Type                                 | Default Value | Description                 |
| --------- | ------------------------------------ | ------------- | --------------------------- |
| name      | string                               | `'qr'`        | Name of the downloaded file |
| extension | string (`'png' 'jpeg' 'webp' 'svg'`) | `'png'`       | File extension              |

`QRCodeStyling.toDataUrl(extension, quality) => Promise<void>`

| Param     | Type                           | Default Value | Description                                                                                                                                                                                                                                                                                                  |
| --------- | ------------------------------ | ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| extension | string (`'png' 'jpeg' 'webp')` | 'png'         | Blob type                                                                                                                                                                                                                                                                                                    |
| quality   | number                         | undefined     | [A Number between 0 and 1 indicating the image quality to be used when creating images using file formats that support lossy compression (such as image/jpeg or image/webp). A user agent will use its default quality value if this option is not specified, or if the number is outside the allowed range. |

### License

[MIT License](https://raw.githubusercontent.com/kozakdenys/qr-code-styling/master/LICENSE). Copyright (c) 2021 Denys Kozak
