<p align="center">
  <img src="https://github.com/staskobzar/vue-audio-visual/blob/master/static/logo.png?raw=true"/>
</p>

# vue-audio-visual

[![Build Status](https://travis-ci.org/staskobzar/vue-audio-visual.svg?branch=master)](https://travis-ci.org/staskobzar/vue-audio-visual)
[![codecov](https://codecov.io/gh/staskobzar/vue-audio-visual/branch/master/graph/badge.svg)](https://codecov.io/gh/staskobzar/vue-audio-visual)
[![Codacy Badge](https://api.codacy.com/project/badge/Grade/bcc7e911360b4ef4a4d987ca5a846caa)](https://www.codacy.com/app/staskobzar/vue-audio-visual?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=staskobzar/vue-audio-visual&amp;utm_campaign=Badge_Grade)
[![bitHound Code](https://www.bithound.io/github/staskobzar/vue-audio-visual/badges/code.svg)](https://www.bithound.io/github/staskobzar/vue-audio-visual)
[![MIT](https://img.shields.io/npm/l/vue-audio-visual.svg?maxAge=2592000)](https://github.com/staskobzar/vue-audio-visual/blob/master/LICENSE)
[![npm](https://img.shields.io/npm/v/vue-audio-visual.svg)](https://www.npmjs.com/package/vue-audio-visual)

> Vue HTML5 audio visualization components

- [Overview](#overview)
- [Install and setup](#install-and-setup)
- [API](#api)
  * [Common props](#common-props)
  * [AvLine props](#avline-props)
  * [AvBars props](#avbars-props)
  * [AvCircle props](#avcircle-props)
- [Todo](#todo)
- [License](#license)

## Overview
An audio spectrum visualizer plugin for [VueJS](https://vuejs.org/) framework. It is built with HTML5
[Web Audio API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Audio_API) and compatible with all browsers that support HTML5 audio API.
It provides several Vue components that allows to draw light and nice visualization for "audio" HTML elements.

Component **AvLine**. Vue template name **&lt;av-line&gt;**
```html
    <av-line
      :line-width="2"
      line-color="lime"
      audio-src="/static/music.mp3"
    ></av-line>
```
This will create following element:

![AvLine Intro](https://github.com/staskobzar/vue-audio-visual/blob/master/static/overview-vav-line.png?raw=true)

Component **AvBars**. Vue template name **&lt;av-bars&gt;**
```html
    <av-bars
      caps-color="#FFF"
      :bar-color="['#f00', '#ff0', '#0f0']"
      canv-fill-color="#000"
      :caps-height="2"
      audio-src="/static/bach.mp3"
    ></av-bars>
```
This will create following element:

![AvBars Intro](https://github.com/staskobzar/vue-audio-visual/blob/master/static/overview-vav-bars.png?raw=true)

Component **AvCircle**. Vue template name **&lt;av-circle&gt;**
```html
    <av-circle
      :outline-width="0"
      :progress-width="5"
      :outline-meter-space="5"
      :playtime="true"
      playtime-font="18px Monaco"
      audio-src="/static/bach.mp3"
    ></av-circle>
```
This will create following element:

![AvCircle Intro](https://github.com/staskobzar/vue-audio-visual/blob/master/static/overview-vav-circle.png?raw=true)

## Install and setup

Install using npm
```
npm install --save vue-audio-visual
```

Enable plugin in main.js:
```javascript
import Vue from 'vue'
import AudioVisual from 'vue-audio-visual'

Vue.use(AudioVisual)
```

Example of usage in App.vue or any other Vue component:
```html
  <av-bars
    audio-src="/static/bach.mp3">
  </av-bars>
```

## API

There are three components that comes with plugin: av-line, av-bars, av-circle.

There are a lot of **props** available to configurate each component.
The only mandatory "prop" to pass to component: **audio-src**.
Prop **audio-src** value should contain URL to media file. Example:
```
audio-src="http://example.com/media/song.mp3"
```
You may also specify an **audio** prop which allows you to use an already existing audio element or an instance of `Audio`. Example:
```
:audio="$refs.audioElement"
```

Plugin will generate "audio" to control media playback (unless one is specified) and "canvas" element for visualization.

There are props that are common for all components and special props for each component.

### Common props

<table>
  <thead>
    <tr>
      <th width="150">Name</th>
      <th>Type</th>
      <th>Default</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>audio-controls</td>
      <td><code>Boolean</code></td>
      <td><code>true</code></td>
      <td>
        Audio element controls attribute. When provided should
        display audio element with controls.
      </td>
    </tr>
    <tr>
      <td>cors-anonym</td>
      <td><code>Boolean</code></td>
      <td><code>false</code></td>
      <td>
        Set CORS attribute for audio element. Set this attribute when using
        audio source is pointing to different host/domain. When set, parameter
        crossOrigin of audio element will be set to 'anonymous'.
      </td>
    </tr>
    <tr>
      <td>audio-class</td>
      <td><code>String</code></td>
      <td><code>null</code></td>
      <td>Audio element css class name.</td>
    </tr>
    <tr>
      <td>canv-class</td>
      <td><code>String</code></td>
      <td><code>null</code></td>
      <td>Canvas element css class name.</td>
    </tr>
    <tr>
      <td>canv-top</td>
      <td><code>Boolean</code></td>
      <td><code>false</code></td>
      <td>By default plugin creates "audio" element wrapped in "div"
          and puts "canvas" element below. When "canv-top" is "true" then
          "canvas" element is set on top. Example:
          <code> :canv-top="true"</code> or
          <code> v-bind:canv-top="true"</code>
      </td>
    </tr>
    <tr>
      <td>canv-fill-color</td>
      <td><code>String</code>, <code>Array</code></td>
      <td><code>null</code></td>
      <td>Canvas fill background color. Can be string RGB color or Array of RGB color.
          When Array is given, plugin creates linear gradient and set it as background.
          Array value should be binded.
          Default is null, which makes background transperent.
          Examples:<br/>
          <code>canv-fill-color="#00AAFF"</code><br/>
          <code>:canv-fill-color="['#FFF', 'rgb(0,255,127)', '#00f']"</code>
      </td>
    </tr>
    <tr>
      <td>enabled</td>
      <td><code>Boolean</code></td>
      <td><code>true</code></td>
      <td>Determines whether the main loop is running or not.
      Examples: <br />
      <code>:enabled="someComputedVariable"</code>
      <code>:enabled="visible"</code>
    </tr>
  </tbody>
</table>

### AvLine props

<table>
  <thead>
    <tr>
      <th width="150">Name</th>
      <th>Type</th>
      <th>Default</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>canv-width</td>
      <td><code>Number</code></td>
      <td><code>300</code></td>
      <td>Canvas element width. Default 300.
          Example: <code>:canv-width="600"</code>
      </td>
    </tr>
    <tr>
      <td>canv-height</td>
      <td><code>Number</code></td>
      <td><code>80</code></td>
      <td>Canvas element height. Default 80.
          Example: <code>:canv-height="120"</code>
      </td>
    </tr>
    <tr>
      <td>line-width</td>
      <td><code>Number</code></td>
      <td><code>2</code></td>
      <td>Graph line width in px. Integer or float number.
          Example: <code>:line-width="0.5"</code>
      </td>
    </tr>
    <tr>
      <td>line-color</td>
      <td><code>String</code>, <code>Array</code></td>
      <td><code>#9F9</code></td>
      <td>Graph line color. Can be string RGB color or Array of RGB color.
          When Array is given, plugin creates linear gradient and set it as background.
          Array value should be binded.
          Examples:<br/>
          <code>line-color="#00AAFF"</code><br/>
          <code>:line-color="['#FFF', 'rgb(0,255,127)', '#00f']"</code>
      </td>
    </tr>
    <tr>
      <td>fft-size</td>
      <td><code>Number</code></td>
      <td><code>128</code></td>
      <td>Represents the window size in samples that is used when performing
          a Fast Fourier Transform (FFT) to get frequency domain data.<br/>
          Must be power of 2 between 2<sup>5</sup> and 2<sup>15</sup>.
          Example: <code>:fft-size="512"</code>
      </td>
    </tr>
  </tbody>
</table>

### AvBars props

<table>
  <thead>
    <tr>
      <th width="150">Name</th>
      <th>Type</th>
      <th>Default</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>canv-width</td>
      <td><code>Number</code></td>
      <td><code>300</code></td>
      <td>Canvas element width. Default 300.
          Example: <code>:canv-width="600"</code>
      </td>
    </tr>
    <tr>
      <td>canv-height</td>
      <td><code>Number</code></td>
      <td><code>80</code></td>
      <td>Canvas element height. Default 80.
          Example: <code>:canv-height="120"</code>
      </td>
    </tr>
    <tr>
      <td>bar-width</td>
      <td><code>Number</code></td>
      <td><code>5</code></td>
      <td>Width of bars in pixels. Example: <code>:bar-width="12"</code>
      </td>
    </tr>
    <tr>
      <td>bar-space</td>
      <td><code>Number</code></td>
      <td><code>1</code></td>
      <td>Space between bars. Example: <code>:bar-space="1.6"</code></td>
    </tr>
    <tr>
      <td>bar-color</td>
      <td><code>String</code>, <code>Array</code></td>
      <td><code>#0A0AFF</code></td>
      <td>Bar fill color. Can be string RGB color or canvas gradients array.<br/>
          Examples:<br/>
          <code>bar-color="#00AAFF"</code><br/>
          <code>:bar-color="['#FFF', 'rgb(0,255,127)', 'green']"</code>
      </td>
    </tr>
    <tr>
      <td>caps-height</td>
      <td><code>Number</code></td>
      <td><code>0</code></td>
      <td>Create caps on bars with given height in pixels.
          When zero no caps created. Example: <code>:caps-height="2"</code>
      </td>
    </tr>
    <tr>
      <td>caps-drop-speed</td>
      <td><code>Number</code></td>
      <td><code>0.9</code></td>
      <td>Caps drop down animation speed. The higher nubmer the faster caps are going down.
          Example: <code>:caps-drop-speed="0.5"</code>
      </td>
    </tr>
    <tr>
      <td>caps-color</td>
      <td><code>String</code></td>
      <td><code>#A0A0FF</code></td>
      <td>Caps rectangles RGB color.
          Example: <code>caps-color="lime"</code>
      </td>
    </tr>
    <tr>
      <td>brick-height</td>
      <td><code>Number</code></td>
      <td><code>0</code></td>
      <td>Draw bar as bricks when height is set and not zero.<br/>
          Example: <code>:brick-height="6"</code><br/>
          <img src="https://github.com/staskobzar/vue-audio-visual/blob/master/static/vav-bars-bricks.png?raw=true" />
      </td>
    </tr>
    <tr>
      <td>brick-space</td>
      <td><code>Number</code></td>
      <td><code>1</code></td>
      <td>Space between bricks. Example: <code>:brick-space="2"</code>
      </td>
    </tr>
    <tr>
      <td>symmetric</td>
      <td><code>Boolean</code></td>
      <td><code>false</code></td>
      <td>Draw bars symmetric to canvas vertical center.
          Example: <code>:symmetric="true"</code><br/>
          <img src="https://github.com/staskobzar/vue-audio-visual/blob/master/static/vav-bars-symm.png?raw=true" />
      </td>
    </tr>
    <tr>
      <td>fft-size</td>
      <td><code>Number</code></td>
      <td><code>1024</code></td>
      <td>Represents the window size in samples that is used when performing
          a Fast Fourier Transform (FFT) to get frequency domain data.<br/>
          Must be power of 2 between 2<sup>5</sup> and 2<sup>15</sup>.
          Example: <code>:fft-size="2048"</code>
      </td>
    </tr>
  </tbody>
</table>

### AvCircle props

<table>
  <thead>
    <tr>
      <th width="150">Name</th>
      <th>Type</th>
      <th>Default</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>canv-width</td>
      <td><code>Number</code></td>
      <td><code>100</code></td>
      <td>Canvas element width.
          Example: <code>:canv-width="600"</code>
      </td>
    </tr>
    <tr>
      <td>canv-height</td>
      <td><code>Number</code></td>
      <td><code>100</code></td>
      <td>Canvas element height.
          Example: <code>:canv-height="120"</code>
      </td>
    </tr>
    <tr>
      <td>radius</td>
      <td><code>Number</code></td>
      <td><code>0</code></td>
      <td>Base circle radius. If zero, then will be calculated from canvas
          width: (canv-width / 2) * 0.7
          Example: <code>:radius="20"</code>
      </td>
    </tr>
    <tr>
      <td>line-width</td>
      <td><code>Number</code></td>
      <td><code>1</code></td>
      <td>Frequency bit line width to draw.
          Example: <code>:line-width="0.4"</code>
      </td>
    </tr>
    <tr>
      <td>line-space</td>
      <td><code>Number</code></td>
      <td><code>1</code></td>
      <td>Space between lines to draw.
          Example: <code>:line-space="2"</code>
      </td>
    </tr>
    <tr>
      <td>outline-color</td>
      <td><code>String</code></td>
      <td><code>#0000FF</code></td>
      <td>Outline (contour) style RGB color.
          Example: <code>outline-color="rgb(0,255,0)"</code>
      </td>
    </tr>
    <tr>
      <td>outline-width</td>
      <td><code>Number</code></td>
      <td><code>0.3</code></td>
      <td>Outline (contour) line width. Float value.
          Example: <code>:outline-width="1"</code>
      </td>
    </tr>
    <tr>
      <td>bar-width</td>
      <td><code>Number</code></td>
      <td><code>1</code></td>
      <td>Frequency graph bar width.
          Example: <code>:bar-width="1"</code>
      </td>
    </tr>
    <tr>
      <td>bar-length</td>
      <td><code>Number</code></td>
      <td><code>0</code></td>
      <td>Frequency graph bar length/height.
          Default is a difference between radius and canvas width.
          Example: <code>:bar-length="27"</code>
      </td>
    </tr>
    <tr>
      <td>bar-color</td>
      <td><code>String</code>, <code>Array</code></td>
      <td><code>[#FFF,#00F]</code></td>
      <td>Bar style RGB color or radient gradient when array.
          Example: <code>:bar-color="#12AA55"</code>
      </td>
    </tr>
    <tr>
      <td>progress</td>
      <td><code>Boolean</code></td>
      <td><code>true</code></td>
      <td>Draw playtime progress meter.
          Example: <code>:progress="false"</code>
      </td>
    </tr>
    <tr>
      <td>progress-width</td>
      <td><code>Number</code></td>
      <td><code>1</code></td>
      <td>Playtime progress meter width.
          Example: <code>:progress-width="2.4"</code>
      </td>
    </tr>
    <tr>
      <td>progress-color</td>
      <td><code>String</code></td>
      <td><code>#0000FF</code></td>
      <td>Playtime progress meter color.
          Example: <code>:progress-color="green"</code>
      </td>
    </tr>
    <tr>
      <td>progress-clockwise</td>
      <td><code>Boolean</code></td>
      <td><code>false</code></td>
      <td>Playtime progress meter arc draw direction.
          Example: <code>:progress-clockwise="true"</code>
      </td>
    </tr>
    <tr>
      <td>outline-meter-space</td>
      <td><code>Number</code></td>
      <td><code>3</code></td>
      <td>Space between outline and progress meter. The bigger the closer to the circle centre.
          Example: <code>:outline-meter-space="1"</code>
      </td>
    </tr>
    <tr>
      <td>playtime</td>
      <td><code>Boolean</code></td>
      <td><code>false</code></td>
      <td>Draw played time as text in the center of the circle.
          Example: <code>:playtime="true"</code>
      </td>
    </tr>
    <tr>
      <td>playtime-font</td>
      <td><code>String</code></td>
      <td><code>14px Monaco</code></td>
      <td>Played time print font.
          Example: <code>playtime-font="18px monospace"</code>
      </td>
    </tr>
    <tr>
      <td>playtime-color</td>
      <td><code>String</code></td>
      <td><code>#00f</code></td>
      <td>Played time font color.
          Example: <code>playtime-color="green"</code>
      </td>
    </tr>
    <tr>
      <td>rotate-graph</td>
      <td><code>Boolean</code></td>
      <td><code>false</code></td>
      <td>Rotate graph clockwise enable.
          Example: <code>:rotate-graph="true"</code>
      </td>
    </tr>
    <tr>
      <td>rotate-speed</td>
      <td><code>Number</code></td>
      <td><code>0.001</code></td>
      <td>Rotate graph speed.
          Example: <code>:rotate-speed="0.2"</code>
      </td>
    </tr>
    <tr>
      <td>fft-size</td>
      <td><code>Number</code></td>
      <td><code>1024</code></td>
      <td>Represents the window size in samples that is used when performing
          a Fast Fourier Transform (FFT) to get frequency domain data.<br/>
          Must be power of 2 between 2<sup>5</sup> and 2<sup>15</sup>.
          Example: <code>:fft-size="2048"</code>
      </td>
    </tr>
  </tbody>
</table>

## Todo
- Using Vue refs to parent audio element as alternative to "audio-src".
  This will allow to use single audio element with many different plugin components.
- Pre-load media source and create waveform graph.

## License

[MIT](http://opensource.org/licenses/MIT)
Copyright (c) 2018-present, Stas Kobzar
