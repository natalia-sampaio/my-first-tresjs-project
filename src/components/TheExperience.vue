<script setup lang="ts">
import { TresCanvas } from '@tresjs/core';
import { reactive, shallowRef, watch } from 'vue';
import { BasicShadowMap, SRGBColorSpace, NoToneMapping, PerspectiveCamera } from 'three';
import gsap from 'gsap';

const state = reactive({
  clearColor: '#2B3846',
  shadows: true,
  alpha: false,
  shadowMapType: BasicShadowMap,
  outputColorSpace: SRGBColorSpace,
  toneMapping: NoToneMapping
});

const cameraRef = shallowRef<PerspectiveCamera>();

watch(cameraRef, (camera) => {
  if (camera) {
    gsap.to(camera.position, {
      delay: 1,
      duration: 2,
      x: 11,
      y: 11,
      z: 11,
      ease: 'power3.out',
      onUpdate: () => {
        camera.lookAt(0, 0, 0);
      }
    });
  }
});
</script>

<template>
  <TresCanvas v-bind="state">
    <TresPerspectiveCamera ref="cameraRef" :args="[45, 1, 0.1, 1000]" />
    <TresMesh :position="[0, 0.5, 0]">
      <TresBoxGeometry />
      <TresMeshNormalMaterial />
    </TresMesh>

    <TresGridHelper :args="[4]" />
  </TresCanvas>
</template>
