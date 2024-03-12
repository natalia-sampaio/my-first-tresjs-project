<script setup lang="ts">
import { TresCanvas, useRenderLoop } from '@tresjs/core'
import { shallowRef, watchEffect } from 'vue'

const { onLoop } = useRenderLoop()

const cubeRef = shallowRef()

onLoop(({ delta, elapsed }) => {
  if (cubeRef.value) {
    cubeRef.value.rotation.y += delta
    cubeRef.value.rotation.z = elapsed

    cubeRef.value.position.y = Math.sin(elapsed * 2)
    cubeRef.value.scale.set(Math.sin(elapsed * 2), Math.sin(elapsed * 2), Math.sin(elapsed * 2))
  }
})

watchEffect(() => {
  console.log({ cubeRef })
})
</script>

<template>
  <TresCanvas>
    <TresPerspectiveCamera />
    <TresMesh ref="cubeRef" :position="[0, 0, 0]">
      <TresBoxGeometry />
      <TresMeshNormalMaterial />
    </TresMesh>
    <TresAxesHelper />
  </TresCanvas>
</template>

<style>
html,
body,
#app {
  margin: 0;
  padding: 0;
  height: 100%;
  width: 100%;
}
</style>
