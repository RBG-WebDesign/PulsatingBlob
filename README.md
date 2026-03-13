# Robot Heart Shader - API & Integration Guide

The heart shader exposes a simple set of global JavaScript functions. These can be triggered directly from your robot's main application logic, state machine, or external event listeners.

## 1. Configuration (Debug Mode)

At the very top of the `<script>` tag in `index.html`, there is a `CONFIG` object.

```js
const CONFIG = {
    showDebugControls: true // Set to false to hide the UI buttons
};
```

Change this to `false` before deploying to the physical robot. This will hide the HTML buttons, leaving only the fullscreen canvas.

## 2. Triggering Emotions & States

To change the robot's emotional state, call the global `window.setState(index)` function.

The shader handles the smooth color/shape transitions automatically. By default, any emotion triggered will play for **3 seconds** before automatically fading back to the Idle state.

### Idle (Default)
```js
window.setState(0);
```
**Effect:** Calm Samsung Blue, slow breathing heartbeat (0.8 BPM), gentle floating drift.

### Get Happy
```js
window.setState(1);
```
**Effect:** Shifts to bright Mint/Cyan, faster upbeat pulse (1.6 BPM), slightly expanded core.

### Get Angry
```js
window.setState(2);
```
**Effect:** Shifts to deep Red/Orange, aggressive fast pulse (2.8 BPM), spiky core displacement, intense camera shake.

### Say Hello
```js
window.setState(3);
```
**Effect:** Shifts to a lighter blue, slower base heartbeat, with a rapid oscillating size change that simulates the envelope of an audio waveform.

> **Note:** If you call the same state repeatedly while it is active, the 3-second auto-revert timer will reset, keeping the state alive.

## 3. Triggering the Camera Flash

To trigger the camera flash effect (e.g., when the robot takes a picture), call:

### Take Picture
```js
window.triggerFlash();
```
**Effect:** Instantly blows out the screen to 100% white, then rapidly decays back to the current shader state over about 0.5 seconds.

> **Note:** This can be triggered simultaneously with any of the emotional states above without interrupting them.
