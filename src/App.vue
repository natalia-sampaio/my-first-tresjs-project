<script setup lang="ts">
import { TresCanvas, useRenderLoop } from '@tresjs/core';
import { ref } from 'vue';
import { OrbitControls } from '@tresjs/cientos';

const torusRef = ref();
const torusPosition = ref([0, 0, 0]);

const { onLoop } = useRenderLoop();

onLoop(({ delta, elapsed }) => {
  if (!torusRef.value) return;

  torusRef.value.rotation.x += delta;
  torusRef.value.rotation.y += delta;
});
</script>

<template>
  <TresCanvas window-size>
    <TresPerspectiveCamera :args="[75, 1, 0.1, 1000]" :position="[3, 1, 4]" :look-at="[0, 0, 0]" />
    <OrbitControls />
    <TresScene>
      <TresMesh ref="torusRef" :position="torusPosition">
        <TresTorusKnotGeometry :args="[1, 0.4, 100, 16]" />
        <TresMeshNormalMaterial />
      </TresMesh>
    </TresScene>
    <TresAxesHelper />
  </TresCanvas>
</template>
