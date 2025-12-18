# make2d

# [<img src="https://img.shields.io/npm/dw/make2d.svg?style=for-the-badge&color=success" alt="npm downloads per week" />](https://www.npmjs.com/package/make2d) @ [<img src="https://img.shields.io/npm/v/make2d?style=for-the-badge&color=success" alt="npm version" />](https://www.npmjs.com/package/make2d?activeTab=versions)

Game FrameWork for JavaScript 2D WebGL Games. Unity-inspired architecture: GameObject, Physics, Body, Container, Sprite, Animator, StateMachine, TextureAtlas, Resources loading.

## Why use this?

After making countless indie games, dozens made in html5 webgl, I like to have in such:

1. efficient and mobile friendly drawing ✔️ (pixi)
2. lifecycle management ✔️ (solution below)
3. efficient collision detection or physics ✔️ (make2d)

### Lifecycle management problem

- When you create a game world, its good to organize it in a tree like way of hierarchy of objects.
- Let's take almost any entity in any game, most likely it has some stuff attached in this hierarchy (a home might have some chairs, a tank might have a driver and ammunition, etc.)
- If you don't properly manage destroying an entity, stuff it had attached to it will become a memory leak and kill the app.

### Lifecycle management solution

- So, [all classes](https://nenjack.github.io/make2d/hierarchy.html#Lifecycle) of this framework implement [LifecycleProps](https://nenjack.github.io/make2d/interfaces/LifecycleProps.html).
- When a Lifecycle is destroyed, it emits and closes `destroy$` event subject.
- Along with destroying his children, which in turn behave the same.

## Usage

```ts
import { Scene, GameObject } from 'make2d'

// create a scene
const scene = new Scene({
  visible: true,
  autoSort: true
})

// enable physics for scene
scene.update$.pipe(takeUntil(scene.destroy$)).subscribe(() => {
  scene.physics.separate()
})

// create entity
const gameObject = new GameObject('Entity Name')

// add entity to scene
scene.addChild(gameObject)

// rxjs - subscribe to update function until entity is destroyed
gameObject.update$
  .pipe(takeUntil(gameObject.destroy$))
  .subscribe((deltaTime) => {
    gameObject.update(gameObject, deltaTime)
  })
```

## Demo Structure

```
[pixi WebGL Canvas]
└──[Scene]
   └──[Collision Detection]
      └──[GameObject x 50]
          ├──[Body]
          └──[Animator]
             └──[StateMachine]
```

## Demo SandBox

Check out the [demo sandbox](https://nenjack.github.io/make2d/demo/?fps&debug) to see below code in action.

## Demo Code

- [src/demo/index.ts](src/demo/index.ts)
- [src/demo/sprite.prefab.ts](src/demo/sprite.prefab.ts)

## This FrameWork exports

- **Lifecycle**: base class for managing destroying whole branches of object-tree
- **Component**: base of anything
- **Sprite**: mix of `PIXI.Sprite` and `Lifecycle`
- **Container**: mix of `PIXI.Container` and `Lifecycle`,
- **Animator**: container of multiple `PIXI.AnimatedSprite`
- **GameObject**: basic concept from `Unity`, has components
- **Prefab**: may be used instead of normal JS instantiation
- **SceneSSR**: scene replacement in `node.js environment`
- **Scene**: basic container and `main class`
- **Resources**: easy to use resources loader
- **StateMachine**: basic `state management` component
- **CircleBody**: circular collider for collisions
- **PolygonBody**: polygonal collider for collisions
- **BoxBody**: rectangular collider for collisions
- **TextureAtlas**: for cutting atlases into frames

## Installation

```bash
yarn add -D make2d
```

## API Docs

Here is the in-depth [api documentation](https://nenjack.github.io/make2d/modules.html) easy to browse.
