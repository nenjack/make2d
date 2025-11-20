# make2d

Game FrameWork for JavaScript 2D WebGL Games. Unity-inspired architecture: GameObject, Physics, Body, Container, Sprite, Animator, StateMachine, TextureAtlas, Resources loading.

## Demo SandBox

Check out the [demo sandbox](https://jackie-aniki.github.io/make2d/demo/?fps&debug) to see below code in action.

## Demo Structure

```
[pixi WebGL Canvas]
└──[Scene]
   ├──[Collision Detection]
      └──[GameObject x 50]
          ├──[Body]
          └──[Animator]
             └──[StateMachine]
```

## Features

- [Drawing on WebGL canvas](https://npmjs.com/package/pixi.js)
- [Collision detection](https://npmjs.com/package/detect-collisions)
- [Lifecycle cleanup management](https://www.html5gamedevs.com/topic/44780-best-way-to-remove-objects-from-the-stage/)
- [Reactive events](https://www.learnrxjs.io/learn-rxjs/subjects)
- [State management](https://gamedevelopment.tutsplus.com/tutorials/finite-state-machines-theory-and-implementation--gamedev-11867)
- [Unity-inspired architecture](https://docs.unity3d.com/Manual/CreatingGameplay.html)
- Compatible with pixi version 6, 7 and ~8

## This FrameWork exports all those

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

Here is the in-depth [api documentation](https://jackie-aniki.github.io/make2d/modules.html) easy to browse.

## Demo Code

- [src/demo/index.ts](src/demo/index.ts)
- [src/demo/sprite.prefab.ts](src/demo/sprite.prefab.ts)
