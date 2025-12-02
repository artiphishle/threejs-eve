# Three.js

## Quickstart

```bash
bun install
bun dev
```

## Chapters

### Camera

- **Perspective Camera**: @todo
- **Ortographic Camera**: @todo

### Renderer

@todo

### Material

@todo

### GUI

#### DAT GUI

```bash
bun add --dev dat.gui
bun add --dev @types/dat.gui
```

#### LIL GUI

```bash
bun add --dev lil-gui
```

BUT: If you want to use the version shipped with ThreeJS:

```ts
import { GUI } from 'three/addons/libs/lil-gui.module.min.js'
```

### Light

- **Ambient Light**: Lights all directions equally
- **Directional Light**: No fix light emerging position
- **Point Light**: Particular light emerging position

### Shadow

- **Cast Shadow**: Object causes shadow
- **Receive Shadow**: Object receives shadowing from other objects

### Animation

#### Lerp

Linear interpolation. Used to animate properties over time.

#### JEasings

Advanced way to control animations compared to lerp.

```bash
bun add --dev jeasings
```

#### GLTF Animation

```ts
let mixer: THREE.AnimationMixer

await gltfLoader.loadAsync('models/bunny_compressed.glb').then((gltf) => {
  mixer = new THREE.AnimationMixer(gltf.scene)
  mixer.clipAction(gltf.animations[0]).play()

  scene.add(gltf.scene)
})
```

### DRACO

#### Compress .glb

```bash
gltf-transform optimize ./models/my_model.glb ./models/my_model_compressed.glb --compress draco --texture-compress webp
```

#### Load compressed .glb

```ts
const gltfLoader = new GLTFLoader()
const dracoLoader = new DRACOLoader()

gltfLoader.setDRACOLoader(dracoLoader)
dracoLoader.setDecoderPath('https://www.gstatic.com/draco/v1/decoders/')
```

### Rapier

Physics engine – calculate rigid body forces, velocities, contacts, constraints

```bash
bun add --dev @dimforge/rapier3d
```

#### Gravity example:

```ts
const gravity = new RAPIER.Vector3(0.0, -9.81, 0.0)
const world = new RAPIER.World(gravity)

// .dynamic() means it's a moving object (so putting it somewhere > 0 on the y axis will make it fall due to gravity)
// .fixed() means it's a non-moving object
const cubeBody = world.createRigidBody(RAPIER.RigidBodyDesc.dynamic().setTranslation(0, 5, 0).setCanSleep(false))
const cubeShape = RAPIER.ColliderDesc.cuboid(0.5, 0.5, 0.5).setMass(1).setRestitution(1.1)

world.createCollider(cubeShape, cubeBody)
dynamicBodies.push([cubeMesh, cubeBody])
```
