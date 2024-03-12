<script setup lang="ts">
import { TresCanvas } from '@tresjs/core';
import { SRGBColorSpace } from 'three';
import { OrbitControls } from '@tresjs/cientos';

const positionsArray = new Float32Array([0, 0, 0, 0, 1, 0, 1, 0, 0]);
</script>

<template>
  <TresCanvas clear-color="#2c3846" :output-color-space="SRGBColorSpace">
    <TresPerspectiveCamera />
    <OrbitControls />
    <TresMesh>
      <TresBufferGeometry :position="[positionsArray, 3]" />
      <TresMeshBasicMaterial color="#ff0000" wireframe />
    </TresMesh>
    <TresAxesHelper :args="[0.5]" />
  </TresCanvas>
</template>
