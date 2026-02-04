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

manager.addEventListener('hand-detected', (e) => {
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
