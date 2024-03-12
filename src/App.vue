<script setup lang="ts">
import { TresCanvas } from '@tresjs/core';
import { OrbitControls } from '@tresjs/cientos';
import { reactive } from 'vue';
import { BasicShadowMap, NoToneMapping } from 'three';

const state = reactive({
  clearColor: '#82dbc5',
  shadows: true,
  alpha: false,
  shadowMapType: BasicShadowMap,
  toneMapping: NoToneMapping
});
</script>

<template>
  <TresCanvas v-bind="state" window-size>
    <TresPerspectiveCamera :position="[7, 7, 7]" :look-at="[0, 0, 0]" />
    <OrbitControls />
    <TresMesh :position="[0, 2, 0]" cast-shadow>
      <TresSphereGeometry />
      <TresMeshToonMaterial color="#E8751A" />
    </TresMesh>
    <TresAxesHelper />
    <TresGridHelper :args="[10, 10, 0x444444, 'teal']" />
  </TresCanvas>
</template>
