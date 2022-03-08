<script setup lang="ts">
import type { Mesh } from 'babylonjs'
import { ArcRotateCamera, Engine, HemisphericLight, MeshBuilder, Scene, Sound, Vector3 } from 'babylonjs'
// const canvas: any = document.getElementById('renderCanvas')
const renderCanvas = ref(null)
onMounted(() => {
  const canvas = renderCanvas.value
  const engine: Engine = new Engine(canvas, true)
  function createScene(): Scene {
    const scene: Scene = new Scene(engine)

    const camera: ArcRotateCamera = new ArcRotateCamera('Camera', Math.PI / 1.7, Math.PI / 1.7, 2, Vector3.Zero(), scene)
    camera.attachControl(canvas, true)

    const light1: HemisphericLight = new HemisphericLight('light1', new Vector3(1, 1, 0), scene)

    const sphere: Mesh = MeshBuilder.CreateSphere('sphere', { diameter: 1 }, scene)
    sphere.position.y = 1
    const ground = MeshBuilder.CreateGround('ground', { width: 10, height: 10 }, scene)
    const sound = new Sound('test', 'https://m10.music.126.net/20220304185042/dfb74b6796c6eebbfdfbae5b8af2a262/yyaac/obj/wonDkMOGw6XDiTHCmMOi/2508810259/d306/d047/a144/b42b3a1e9400ac91171c39e702f51180.m4a',
      scene, () => {}, { loop: true, autoplay: true })
    return scene
  }
  const scene: Scene = createScene()
  engine.runRenderLoop(() => {
    scene.render()
  })
})
</script>

<template>
  <div text-gray:80 text-center>
    <h2>BabylonJS</h2>
    <canvas
      ref="renderCanvas"
      mx-auto my-20 p-2 w-full
      h-200
    />
  </div>
</template>
