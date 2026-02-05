# Digit

Hand tracking module using MediaPipe and TensorFlow.js.

## Installation

```bash
npm install digit
```

## Development

```bash
npm run dev
```

This will start a development server with hot reload at `http://localhost:5173`.

## Usage

```javascript
import { HandLandmarkManager } from 'digit';

const manager = new HandLandmarkManager({
    modelType: 'full', // 'lite' or 'full'
    mirror: true
});

await manager.init();

manager.addEventListener(HandLandmarkManager.EVENTS.HAND_DETECTED, (e) => {
    const results = e.detail;
    
    // 2D Normalized Landmarks (0-1)
    const landmarks = results.landmarks; 
    
    // 3D World Landmarks (in meters)
    const worldLandmarks = results.worldLandmarks;
    
    console.log(worldLandmarks);
});
```

## API

### HandLandmarkManager

#### Events

The `HandLandmarkManager` exposes event names via the static `EVENTS` property:

| Event Constant | Value | Description |
| :--- | :--- | :--- |
| `HandLandmarkManager.EVENTS.HAND_DETECTED` | `'hand-detected'` | Dispatched when hands are detected. Contains `results` with `landmarks` and `worldLandmarks` in `event.detail`. |
| `HandLandmarkManager.EVENTS.ERROR` | `'error'` | Dispatched when an error occurs during detection. |

#### `constructor(options)`
- `options.modelType`: 'LITE' | 'FULL' (default: 'FULL')
- `options.numHands`: number (default: 2)
- `options.mirror`: boolean (default: true)

#### `init(cameraManager?: CameraManager)`
Initialize the manager. Optionally pass an existing `CameraManager` instance.

#### `start()`
Start the detection loop.

#### `stop()`
Stop the detection loop.

#### `dispose()`
Clean up resources.

#### `getVertices()`
Returns array of 3D vertices for the first detected hand.

#### `getHandCount()`
Returns number of hands detected.
