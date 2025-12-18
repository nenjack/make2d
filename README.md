# make2d

# [<img src="https://img.shields.io/npm/dw/make2d.svg?style=for-the-badge&color=success" alt="npm downloads per week" />](https://www.npmjs.com/package/make2d) @ [<img src="https://img.shields.io/npm/v/make2d?style=for-the-badge&color=success" alt="npm version" />](https://www.npmjs.com/package/make2d?activeTab=versions)

Game Framework for JavaScript 2D WebGL Games.

Unity-inspired architecture built on top of **PIXI.js**, focused on
**lifecycle management**, **collision detection**, and **clean object hierarchies**.

- fast and mobile friendly rendering ✔️ (pixi)
- lifecycle-safe entity hierarchy ✔️
- efficient collision detection ✔️ (check2d)
- rxjs-driven update loop ✔️ (rxjs)

## demo

https://nenjack.github.io/make2d/demo/

## demo code

```ts
import { Scene, GameObject } from 'make2d'

const scene = new Scene({
  visible: true,
  autoSort: true
})

scene.update$.pipe(takeUntil(scene.destroy$)).subscribe(() => {
  scene.physics.separate()
})

const gameObject = new GameObject('Entity Name')
scene.addChild(gameObject)

gameObject.update$
  .pipe(takeUntil(gameObject.destroy$))
  .subscribe((deltaTime) => {
    gameObject.update(gameObject, deltaTime)
  })
```

## why make2d?

While building many indie games (including html5 WebGL titles), a few core needs
appear repeatedly:

1. drawing that works well on desktop and mobile
2. predictable lifecycle management
3. collision detection without memory leaks

### lifecycle management

Every object in a game tends to own other objects
(e.g. tank → turret → ammo, house → furniture).

If an entity is destroyed without handling its children properly,
memory leaks will eventually kill the application.

**make2d solves this by design.**

- All framework classes implement `Lifecycle`
- Destroying an object:
  - emits and completes `destroy$`
  - recursively destroys all children

- rxjs subscriptions can be safely bound to lifecycle

## demo structure

```
[pixi WebGL Canvas]
└──[Scene]
   └──[Collision Detection]
      └──[GameObject x 50]
          ├──[Body]
          └──[Animator]
             └──[StateMachine]
```

## exports

make2d provides a small but complete set of building blocks:

- **Lifecycle** – base class for destroying whole branches of object tree
- **Component** – base of all components
- **GameObject** – Unity-like entity with components
- **Scene** – main container and entry point
- **SceneSSR** – scene replacement for node.js
- **Container** – `PIXI.Container` + `Lifecycle`
- **Sprite** – `PIXI.Sprite` + `Lifecycle`
- **Animator** – container of multiple `PIXI.AnimatedSprite`
- **StateMachine** – simple state management
- **Resources** – easy-to-use asset loader
- **Prefab** – declarative entity creation
- **CircleBody** – circular collider
- **BoxBody** – rectangular collider
- **PolygonBody** – polygon collider
- **TextureAtlas** – atlas frame slicing

## installation

```bash
yarn add make2d
```

## docs

- API reference: [https://nenjack.github.io/make2d/modules.html](https://nenjack.github.io/make2d/modules.html)
- Lifecycle docs: [https://nenjack.github.io/make2d/hierarchy.html](https://nenjack.github.io/make2d/hierarchy.html)

## license

MIT
