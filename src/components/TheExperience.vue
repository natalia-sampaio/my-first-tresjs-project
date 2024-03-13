<script setup lang="ts">
import { TresCanvas } from '@tresjs/core';
import { BasicShadowMap, NoToneMapping, SRGBColorSpace } from 'three';
import { OrbitControls, Stars } from '@tresjs/cientos';
import HoustonModel from './HoustonModel.vue';

const gl = {
  clearColor: '#181c3e',
  shadows: true,
  alpha: false,
  shadowMapType: BasicShadowMap,
  outputColorSpace: SRGBColorSpace,
  toneMapping: NoToneMapping
};
</script>

<template>
  <TresCanvas v-bind="gl">
    <TresPerspectiveCamera :position="[5, 5, 5]" :look-at="[0, 1, 0]" />
    <Stars />
    <OrbitControls />
    <Suspense>
      <HoustonModel />
    </Suspense>
    <TresAmbientLight :intensity="1" />
    <TresDirectionalLight :position="[-4, -2, 2]" :intensity="1" cast-shadow color="#fff" />
    <TresDirectionalLight :position="[4, 6, 4]" :intensity="2" cast-shadow color="white" />
  </TresCanvas>
</template>
