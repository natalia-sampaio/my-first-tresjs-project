<script setup lang="ts">
import { TresCanvas } from '@tresjs/core';
import { DoubleSide, SRGBColorSpace } from 'three';
import { OrbitControls } from '@tresjs/cientos';

const positionsArray = new Float32Array([0, 0, 0, 0, 1, 0, 1, 0, 0]);
</script>

<template>
  <TresCanvas clear-color="#2c3846" :output-color-space="SRGBColorSpace" alpha>
    <TresPerspectiveCamera />
    <OrbitControls />
    <TresMesh>
      <TresTorusKnotGeometry :args="[1, 0.4, 32, 32]" />
      <TresMeshPhysicalMaterial color="silver" :emissive-intensity="0.5" />
    </TresMesh>
    <TresMesh :position="[4, 0, 0]">
      <TresTorusGeometry :args="[1, 0.4, 100, 1000]" />
      <TresMeshToonMaterial color="pink" />
    </TresMesh>
    <TresAmbientLight :args="[0xffffff, 1]" />
    <TresDirectionalLight :args="[0xffffff, 2]" :position="[0, 4, 0]" />
  </TresCanvas>
</template>
