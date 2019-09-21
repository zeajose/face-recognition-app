# face-api.js

[![Build Status](https://travis-ci.org/justadudewhohacks/face-api.js.svg?branch=master)](https://travis-ci.org/justadudewhohacks/face-api.js)
[![Slack](https://slack.bri.im/badge.svg)](https://slack.bri.im)

**JavaScript face recognition API for the browser and nodejs implemented on top of tensorflow.js core ([tensorflow/tfjs-core](https://github.com/tensorflow/tfjs-core))**

![faceapi](https://user-images.githubusercontent.com/31125521/57224752-ad3dc080-700a-11e9-85b9-1357b9f9bca4.gif)

## **[Click me for Live Demos!](https://justadudewhohacks.github.io/face-api.js/)**

## Tutorials

* **[face-api.js — JavaScript API for Face Recognition in the Browser with tensorflow.js](https://itnext.io/face-api-js-javascript-api-for-face-recognition-in-the-browser-with-tensorflow-js-bcc2a6c4cf07)**
* **[Realtime JavaScript Face Tracking and Face Recognition using face-api.js’ MTCNN Face Detector](https://itnext.io/realtime-javascript-face-tracking-and-face-recognition-using-face-api-js-mtcnn-face-detector-d924dd8b5740)**
* **[Realtime Webcam Face Detection And Emotion Recognition - Video](https://youtu.be/CVClHLwv-4I)**
* **[Easy Face Recognition Tutorial With JavaScript - Video](https://youtu.be/AZ4PdALMqx0)**

## Table of Contents

* **[Features](#features)**
* **[Running the Examples](#running-the-examples)**
* **[face-api.js for the Browser](#face-api.js-for-the-browser)**
* **[face-api.js for Nodejs](#face-api.js-for-nodejs)**
* **[Usage](#getting-started)**
  * **[Loading the Models](#getting-started-loading-models)**
  * **[High Level API](#getting-started-high-level-api)**
  * **[Displaying Detection Results](#getting-started-displaying-detection-results)**
  * **[Face Detection Options](#getting-started-face-detection-options)**
  * **[Utility Classes](#getting-started-utility-classes)**
  * **[Other Useful Utility](#other-useful-utility)**
* **[Available Models](#models)**
  * **[Face Detection](#models-face-detection)**
  * **[Face Landmark Detection](#models-face-landmark-detection)**
  * **[Face Recognition](#models-face-recognition)**
  * **[Face Expression Recognition](#models-face-expression-recognition)**
  * **[Age Estimation and Gender Recognition](#models-age-and-gender-recognition)**
* **[API Documentation](https://justadudewhohacks.github.io/face-api.js/docs/globals.html)**

# Features

## Face Recognition

![face-recognition](https://user-images.githubusercontent.com/31125521/57297377-bfcdfd80-70cf-11e9-8afa-2044cb167bff.gif)

## Face Landmark Detection

![face_landmark_detection](https://user-images.githubusercontent.com/31125521/57297731-b1ccac80-70d0-11e9-9bd7-59d77f180322.jpg)

## Face Expression Recognition

![preview_face-expression-recognition](https://user-images.githubusercontent.com/31125521/50575270-f501d080-0dfb-11e9-9676-8f419efdade4.png)

## Age Estimation & Gender Recognition

![age_gender_recognition](https://user-images.githubusercontent.com/31125521/57297736-b5603380-70d0-11e9-873d-8b6c7243eb64.jpg)

<a name="running-the-examples"></a>

# Running the Examples

Clone the repository:

``` bash
git clone https://github.com/justadudewhohacks/face-api.js.git
```

## Running the Browser Examples

``` bash
cd face-api.js/examples/examples-browser
npm i
npm start
```

Browse to http://localhost:3000/.

## Running the Nodejs Examples

``` bash
cd face-api.js/examples/examples-nodejs
npm i
```

Now run one of the examples using ts-node:

``` bash
ts-node faceDetection.ts
```

Or simply compile and run them with node:

``` bash
tsc faceDetection.ts
node faceDetection.js
```

<a name="face-api.js-for-the-browser"></a>

# face-api.js for the Browser

Simply include the latest script from [dist/face-api.js](https://github.com/justadudewhohacks/face-api.js/tree/master/dist).

Or install it via npm:

``` bash
npm i face-api.js
```

<a name="face-api.js-for-nodejs"></a>

# face-api.js for Nodejs

We can use the equivalent API in a nodejs environment by polyfilling some browser specifics, such as HTMLImageElement, HTMLCanvasElement and ImageData. The easiest way to do so is by installing the node-canvas package.

Alternatively you can simply construct your own tensors from image data and pass tensors as inputs to the API.

Furthermore you want to install @tensorflow/tfjs-node (not required, but highly recommended), which speeds things up drastically by compiling and binding to the native Tensorflow C++ library:

``` bash
npm i face-api.js canvas @tensorflow/tfjs-node
```

Now we simply monkey patch the environment to use the polyfills:

``` javascript
// import nodejs bindings to native tensorflow,
// not required, but will speed up things drastically (python required)
import '@tensorflow/tfjs-node';

// implements nodejs wrappers for HTMLCanvasElement, HTMLImageElement, ImageData
import * as canvas from 'canvas';

import * as faceapi from 'face-api.js';

// patch nodejs environment, we need to provide an implementation of
// HTMLCanvasElement and HTMLImageElement, additionally an implementation
// of ImageData is required, in case you want to use the MTCNN
const { Canvas, Image, ImageData } = canvas
faceapi.env.monkeyPatch({ Canvas, Image, ImageData })
```

<a name="getting-started"></a>
