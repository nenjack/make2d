# make2d

## [<img valign="middle" src="https://img.shields.io/npm/dw/make2d.svg?style=for-the-badge&color=success" alt="npm downloads per week" />](https://www.npmjs.com/package/make2d) @ [<img valign="middle" src="https://img.shields.io/npm/v/make2d?style=for-the-badge&color=success" alt="npm version" />](https://www.npmjs.com/package/make2d?activeTab=versions)

**make2d** is a lightweight game framework for building **2D WebGL games in JavaScript**.

It provides a **Unity-inspired architecture** on top of **PIXI.js**, focusing on:

- predictable **object hierarchy**
- **safe lifecycle management**
- efficient **collision detection**
- reactive, composable **update loops**

### highlights

- fast, mobile-friendly rendering (PIXI.js)
- Unity-like scene & entity hierarchy
- lifecycle-safe object destruction
- efficient 2D collision system (check2d)
- RxJS-driven update & event model

---

## demo

👉 https://nenjack.github.io/make2d/demo/?fps&debug

---

## demo code

```ts
import { Scene, GameObject } from 'make2d'
import { takeUntil } from 'rxjs'

const scene = new Scene({
  visible: true,
  autoSort: true
})

// scene-level update loop
scene.update$.pipe(takeUntil(scene.destroy$)).subscribe(() => {
  scene.physics.separate()
})

const gameObject = new GameObject('Entity Name')
scene.addChild(gameObject)

// game object update loop
gameObject.update$
  .pipe(takeUntil(gameObject.destroy$))
  .subscribe((deltaTime) => {
    gameObject.update(gameObject, deltaTime)
  })
```

---

## demo structure

```
[HTML5 Canvas + WebGL]
└── [Scene]
    └── [Collision System]
        └── [GameObject x 50]
            ├── [Body]
            └── [Animator]
                └── [StateMachine]
```

The hierarchy and API are intentionally similar to Unity, making it easy to reason about complex scenes.

## why make2d?

When building multiple indie and HTML5 WebGL games, a few recurring problems show up:

1. managing deeply nested game entities
2. avoiding memory leaks during object destruction
3. keeping update logic predictable and composable

**make2d addresses these by design**, using a strict hierarchy and lifecycle model inspired by Unity.

---

## lifecycle & update model

Every object in make2d participates in a **tree-based lifecycle**.

Examples:

- `tank → turret → ammo`
- `house → furniture → props`

### lifecycle guarantees

- All framework classes implement **`Lifecycle`**
- Destroying any object:
  - emits and completes `destroy$`
  - recursively destroys all children

- RxJS subscriptions can safely bind to `destroy$`

### update propagation

- Every object exposes an `update$` observable
- Updates flow **top-down through the hierarchy**
- When a parent updates, all children update automatically
- `deltaTime` is provided each frame

This makes it easy to compose behavior without manual bookkeeping.

---

## exports

make2d provides a small but complete set of building blocks:

### core

- **Lifecycle** – destroy entire branches safely
- **Component** – base class for attachable behavior
- **GameObject** – Unity-like entity container
- **Scene** – root container and game entry point
- **SceneSSR** – Scene replacement for Node.js

### rendering & containers

- **Container** – `PIXI.Container` + lifecycle
- **Sprite** – `PIXI.Sprite` + lifecycle
- **Animator** – manages multiple `PIXI.AnimatedSprite`
- **TextureAtlas** – atlas frame slicing

### state & structure

- **StateMachine** – simple state handling
- **Prefab** – declarative entity creation
- **Resources** – asset loader

### physics

- **CircleBody** – circular collider
- **BoxBody** – rectangular collider
- **PolygonBody** – polygon collider

---

## installation

```bash
yarn add make2d
```

---

## documentation

- API reference
  https://nenjack.github.io/make2d/modules.html
- Lifecycle & hierarchy
  https://nenjack.github.io/make2d/hierarchy.html

---

## license

MIT
