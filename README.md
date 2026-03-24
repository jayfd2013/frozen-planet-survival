# Frozen Planet Survival - Three.js Game Skeleton

A comprehensive guide and skeleton for building a Three.js game.

---

## Table of Contents

1. [Project Structure](#1-project-structure)
2. [Core Setup](#2-core-setup---scene-camera-renderer-animation-loop)
3. [Game Loop Architecture](#3-game-loop-architecture)
4. [Input Handling](#4-input-handling)
5. [Asset Loading](#5-asset-loading)
6. [Physics Integration](#6-physics-integration)
7. [UI/HUD Overlay](#7-uihud-overlay)
8. [State Management](#8-state-management)
9. [Lighting and Environment](#9-lighting-and-environment)
10. [Performance Considerations](#10-performance-considerations)
11. [Modern Tooling - Vite Setup](#11-modern-tooling---vite-setup)
12. [Best NPM Packages](#12-best-npm-packages-for-threejs-games)

---

## 1. Project Structure

```
my-three-game/
├── src/
│   ├── index.ts
│   ├── main.ts
│   ├── core/
│   │   ├── Game.ts          # Main game class
│   │   ├── Clock.ts         # Delta time management
│   │   └── InputManager.ts
│   ├── scenes/
│   │   ├── Scene.ts         # Base scene class
│   │   ├── GameScene.ts
│   │   ├── MenuScene.ts
│   │   └── PauseScene.ts
│   ├── entities/
│   │   ├── Entity.ts        # Base entity class
│   │   ├── Player.ts
│   │   └── Enemy.ts
│   ├── loaders/
│   │   ├── AssetLoader.ts   # Unified asset loading
│   │   ├── ModelLoader.ts
│   │   └── TextureLoader.ts
│   ├── physics/
│   │   └── PhysicsWorld.ts
│   ├── ui/
│   │   ├── HUD.ts
│   │   ├── Menu.ts
│   │   └── styles.css
│   ├── utils/
│   │   ├── ObjectPool.ts
│   │   └── helpers.ts
│   └── assets/
│       ├── models/
│       ├── textures/
│       ├── sounds/
│       └── shaders/
├── public/
│   ├── models/
│   ├── textures/
│   └── sounds/
├── index.html
├── vite.config.js
├── package.json
└── tsconfig.json
```

---

## 2. Core Setup - Scene, Camera, Renderer, Animation Loop

### Recommended Starter Templates

- [Sean Bradley's Three.js TypeScript Boilerplate](https://github.com/Sean-Bradley/Three.js-TypeScript-Boilerplate)
- [Vite Three.js TypeScript Template](https://github.com/pachoclo/vite-threejs-ts-template)
- [Boilerplate Builder](https://jeromeetienne.github.io/threejsboilerplatebuilder/)

### Basic Initialization

```typescript
import * as THREE from 'three';

class Game {
  scene: THREE.Scene;
  camera: THREE.PerspectiveCamera;
  renderer: THREE.WebGLRenderer;
  clock: THREE.Clock;

  constructor() {
    // Scene setup
    this.scene = new THREE.Scene();
    this.scene.background = new THREE.Color(0x1a1a2e);
    this.scene.fog = new THREE.Fog(0x1a1a2e, 50, 200);

    // Camera setup
    this.camera = new THREE.PerspectiveCamera(
      75,
      window.innerWidth / window.innerHeight,
      0.1,
      1000
    );
    this.camera.position.z = 10;

    // Renderer setup
    this.renderer = new THREE.WebGLRenderer({
      antialias: true,
      alpha: true,
    });
    this.renderer.setSize(window.innerWidth, window.innerHeight);
    this.renderer.shadowMap.enabled = true;
    this.renderer.shadowMap.type = THREE.PCFSoftShadowMap;
    document.body.appendChild(this.renderer.domElement);

    // Clock for delta time
    this.clock = new THREE.Clock();

    // Handle window resize
    window.addEventListener('resize', () => this.onWindowResize());
  }

  onWindowResize() {
    const width = window.innerWidth;
    const height = window.innerHeight;
    this.camera.aspect = width / height;
    this.camera.updateProjectionMatrix();
    this.renderer.setSize(width, height);
  }

  start() {
    this.gameLoop();
  }

  gameLoop = () => {
    requestAnimationFrame(this.gameLoop);

    const deltaTime = this.clock.getDelta(); // In seconds

    this.update(deltaTime);
    this.render();
  };

  update(deltaTime: number) {
    // Update game logic here
  }

  render() {
    this.renderer.render(this.scene, this.camera);
  }
}

const game = new Game();
game.start();
```

---

## 3. Game Loop Architecture

### Delta Time and Frame-Rate Independent Movement

Delta time (in seconds) allows smooth movement regardless of frame rate:

```typescript
// Bad - frame rate dependent
object.position.x += 5;

// Good - frame rate independent
const speed = 10; // units per second
object.position.x += speed * deltaTime;
```

### Fixed Timestep Pattern (for physics)

```typescript
const FIXED_TIMESTEP = 1 / 60; // 60 FPS physics
let accumulator = 0;

gameLoop = (currentTime: number) => {
  requestAnimationFrame(this.gameLoop);

  const deltaTime = Math.min(this.clock.getDelta(), 0.1); // Cap at 100ms
  accumulator += deltaTime;

  // Fixed timestep physics updates
  while (accumulator >= FIXED_TIMESTEP) {
    this.physicsWorld.step(FIXED_TIMESTEP);
    accumulator -= FIXED_TIMESTEP;
  }

  // Variable timestep for rendering
  this.update(deltaTime);
  this.render();
};
```

---

## 4. Input Handling

Three.js doesn't provide built-in input handling, so use standard web APIs.

### Keyboard Input

```typescript
class InputManager {
  keys: { [key: string]: boolean } = {};

  constructor() {
    window.addEventListener('keydown', (e) => {
      this.keys[e.key.toLowerCase()] = true;
    });

    window.addEventListener('keyup', (e) => {
      this.keys[e.key.toLowerCase()] = false;
    });
  }

  isKeyPressed(key: string): boolean {
    return this.keys[key.toLowerCase()] || false;
  }

  getMovementVector(): { x: number; z: number } {
    return {
      x: (this.isKeyPressed('d') ? 1 : 0) - (this.isKeyPressed('a') ? 1 : 0),
      z: (this.isKeyPressed('w') ? 1 : 0) - (this.isKeyPressed('s') ? 1 : 0),
    };
  }
}
```

### Mouse Input

```typescript
constructor() {
  window.addEventListener('mousemove', (e) => {
    this.mouseX = (e.clientX / window.innerWidth) * 2 - 1;
    this.mouseY = -(e.clientY / window.innerHeight) * 2 + 1;
  });

  window.addEventListener('click', (e) => {
    this.onMouseClick(e);
  });
}
```

### Gamepad Input

```typescript
getGamepadInput(): { x: number; y: number } {
  const gamepads = navigator.getGamepads();
  if (!gamepads[0]) return { x: 0, y: 0 };

  const gp = gamepads[0];
  const deadzone = 0.1;
  const x = Math.abs(gp.axes[0]) > deadzone ? gp.axes[0] : 0;
  const y = Math.abs(gp.axes[1]) > deadzone ? gp.axes[1] : 0;

  return { x, y };
}
```

---

## 5. Asset Loading

### Using Official Three.js Loaders

```typescript
import { GLTFLoader } from 'three/examples/jsm/loaders/GLTFLoader.js';

class AssetLoader {
  private gltfLoader = new GLTFLoader();
  private textureLoader = new THREE.TextureLoader();
  private audioLoader = new THREE.AudioLoader();
  private loadingManager = new THREE.LoadingManager();

  async loadModel(path: string): Promise<THREE.Group> {
    return new Promise((resolve, reject) => {
      this.gltfLoader.load(
        path,
        (gltf) => resolve(gltf.scene),
        (progress) =>
          console.log(`Loading: ${(progress.loaded / progress.total) * 100}%`),
        (error) => reject(error)
      );
    });
  }

  async loadTexture(path: string): Promise<THREE.Texture> {
    return new Promise((resolve, reject) => {
      this.textureLoader.load(path, resolve, undefined, reject);
    });
  }

  async loadAudio(path: string): Promise<AudioBuffer> {
    return new Promise((resolve, reject) => {
      this.audioLoader.load(path, resolve, undefined, reject);
    });
  }
}
```

---

## 6. Physics Integration

### Engine Comparison

| Engine       | Status                   | Use Case                                      |
| ------------ | ------------------------ | --------------------------------------------- |
| **Rapier**   | Modern (Rust/WebAssembly)| High performance, continuous collision detection |
| **Cannon-es**| Maintained fork          | Easy to implement, good for most games         |
| **Ammo.js**  | Most established         | Widely used, reliable                          |

### Basic Rapier Setup

```typescript
import RAPIER from '@dimforge/rapier3d';

class PhysicsWorld {
  world: RAPIER.World;

  constructor() {
    this.world = new RAPIER.World(new RAPIER.Vector3(0, -9.8, 0));
  }

  step(deltaTime: number) {
    this.world.step();
  }

  createRigidBody(position: THREE.Vector3, shape: RAPIER.ColliderDesc) {
    const bodyDesc = RAPIER.RigidBodyDesc.dynamic().setTranslation(
      position.x,
      position.y,
      position.z
    );
    const body = this.world.createRigidBody(bodyDesc);
    this.world.createCollider(shape, body);
    return body;
  }
}
```

---

## 7. UI/HUD Overlay

### HTML/CSS Overlay (Recommended)

Layer HTML/CSS on top of the Three.js canvas:

```html
<!-- index.html -->
<div id="hud" class="hud">
  <div class="score">Score: <span id="score">0</span></div>
  <div class="health">Health: <span id="health">100</span></div>
</div>

<canvas id="game-canvas"></canvas>
```

```css
.hud {
  position: absolute;
  top: 20px;
  left: 20px;
  color: white;
  font-family: Arial, sans-serif;
  z-index: 10;
  pointer-events: none;
}

.score,
.health {
  margin-bottom: 10px;
  font-size: 20px;
}
```

### CSS2DRenderer for 3D-Positioned Labels

```typescript
import {
  CSS2DRenderer,
  CSS2DObject,
} from 'three/examples/jsm/renderers/CSS2DRenderer.js';

const labelRenderer = new CSS2DRenderer();
labelRenderer.setSize(window.innerWidth, window.innerHeight);
labelRenderer.domElement.style.position = 'absolute';
labelRenderer.domElement.style.top = '0px';
labelRenderer.domElement.style.pointerEvents = 'none';
document.body.appendChild(labelRenderer.domElement);

// Create a label that follows a 3D object
const label = document.createElement('div');
label.textContent = 'Enemy';
const labelObject = new CSS2DObject(label);
enemy.add(labelObject);

// In render loop
labelRenderer.render(scene, camera);
```

---

## 8. State Management

### State Stack Pattern

```typescript
enum GameState {
  MENU = 'menu',
  PLAYING = 'playing',
  PAUSED = 'paused',
  GAME_OVER = 'game_over',
}

class StateManager {
  private currentState: GameState = GameState.MENU;
  private stateStack: GameState[] = [];

  setState(state: GameState) {
    this.currentState = state;
    this.onStateChange();
  }

  pushState(state: GameState) {
    this.stateStack.push(this.currentState);
    this.setState(state);
  }

  popState() {
    const previousState = this.stateStack.pop();
    if (previousState) this.setState(previousState);
  }

  update(deltaTime: number) {
    switch (this.currentState) {
      case GameState.MENU:
        // Update menu
        break;
      case GameState.PLAYING:
        // Update game logic
        break;
      case GameState.PAUSED:
        // Don't update game logic
        break;
    }
  }

  private onStateChange() {
    console.log(`State changed to: ${this.currentState}`);
  }
}
```

---

## 9. Lighting and Environment

### Recommended Game Lighting Setup

```typescript
// Ambient light - base illumination
const ambientLight = new THREE.AmbientLight(0xffffff, 0.4);
this.scene.add(ambientLight);

// Directional light - like the sun
const directionalLight = new THREE.DirectionalLight(0xffffff, 0.8);
directionalLight.position.set(10, 20, 10);
directionalLight.castShadow = true;
directionalLight.shadow.mapSize.width = 2048;
directionalLight.shadow.mapSize.height = 2048;
directionalLight.shadow.camera.far = 100;
this.scene.add(directionalLight);

// Hemisphere light - for outdoor scenes
const hemisphereLight = new THREE.HemisphereLight(0x87ceeb, 0x8b6f47, 0.7);
this.scene.add(hemisphereLight);

// Environment mapping for realistic reflections
const loader = new THREE.TextureLoader();
const envTexture = await loader.loadAsync('path/to/envmap.hdr');
this.scene.environment = envTexture;
this.scene.background = envTexture;
```

---

## 10. Performance Considerations

### Object Pooling

```typescript
class ObjectPool {
  private pool: THREE.Mesh[] = [];
  private available: THREE.Mesh[] = [];

  constructor(size: number, mesh: THREE.Mesh) {
    for (let i = 0; i < size; i++) {
      const clone = mesh.clone() as THREE.Mesh;
      clone.visible = false;
      this.pool.push(clone);
      this.available.push(clone);
    }
  }

  get(): THREE.Mesh | null {
    if (this.available.length > 0) {
      return this.available.pop() || null;
    }
    return null;
  }

  release(mesh: THREE.Mesh) {
    mesh.visible = false;
    this.available.push(mesh);
  }
}
```

### Frustum Culling

Three.js automatically culls objects outside the camera's view (enabled by default via `mesh.frustumCulled = true`). This alone can eliminate up to 50% of draw calls for non-visible objects.

### LOD (Level of Detail)

```typescript
const lod = new THREE.LOD();
lod.addLevel(highQualityMesh, 0); // 0m distance
lod.addLevel(mediumQualityMesh, 50); // 50m distance
lod.addLevel(lowQualityMesh, 100); // 100m distance
this.scene.add(lod);
```

### Instancing for Many Similar Objects

```typescript
const geometry = new THREE.BoxGeometry(1, 1, 1);
const material = new THREE.MeshStandardMaterial();
const instancedMesh = new THREE.InstancedMesh(geometry, material, 10000);

const dummy = new THREE.Object3D();
for (let i = 0; i < 10000; i++) {
  dummy.position.set(
    Math.random() * 100,
    Math.random() * 100,
    Math.random() * 100
  );
  dummy.updateMatrix();
  instancedMesh.setMatrixAt(i, dummy.matrix);
}
instancedMesh.instanceMatrix.needsUpdate = true;
this.scene.add(instancedMesh);
```

### Memory Management

```typescript
// Dispose of unused assets
geometry.dispose();
material.dispose();
texture.dispose();

// Monitor VRAM
console.log(renderer.info.memory);
// { geometries: X, textures: Y }
```

---

## 11. Modern Tooling - Vite Setup

### vite.config.js

```javascript
import { defineConfig } from 'vite';

export default defineConfig({
  server: {
    port: 3000,
  },
  build: {
    minify: 'terser',
    target: 'es2020',
  },
  resolve: {
    alias: {
      '@': '/src',
    },
  },
});
```

### package.json

```json
{
  "name": "frozen-planet-survival",
  "type": "module",
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview"
  },
  "dependencies": {
    "three": "^0.183.0"
  },
  "devDependencies": {
    "vite": "^5.0.0",
    "typescript": "^5.3.0"
  }
}
```

---

## 12. Best NPM Packages for Three.js Games

| Package        | Purpose                | Notes                                      |
| -------------- | ---------------------- | ------------------------------------------ |
| **three**      | Core 3D library        | Essential                                  |
| **cannon-es**  | Physics engine         | Easy to use, well-maintained fork          |
| **rapier3d**   | Physics engine         | Modern, WebAssembly, high performance      |
| **gsap**       | Animation/tweening     | Industry-standard, works great with Three.js |
| **zustand**    | State management       | Lightweight alternative to Redux           |
| **three-nebula** | Particle systems     | Advanced effects                           |
| **theatre**    | Motion design          | Interactive animation timeline             |
| **lil-gui**    | Debug UI               | Lightweight parameter tweaking             |
| **tone.js**    | Web audio              | Game audio and sound effects               |

---

## Quick Start

```bash
npm install
npm run dev
```

---

## References

- [Three.js Documentation](https://threejs.org/docs/)
- [Discover Three.js - Animation Loop](https://discoverthreejs.com/book/first-steps/animation-loop/)
- [Three.js Journey - Physics](https://threejs-journey.com/lessons/physics)
- [Sean Bradley's Three.js TypeScript Boilerplate](https://github.com/Sean-Bradley/Three.js-TypeScript-Boilerplate)
- [Vite Three.js Template](https://github.com/pachoclo/vite-threejs-ts-template)
