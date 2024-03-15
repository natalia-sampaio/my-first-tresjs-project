<script setup lang="ts">
import { TresCanvas } from '@tresjs/core';
import { BasicShadowMap, NoToneMapping, SRGBColorSpace, Vector3 } from 'three';
import { OrbitControls, Stars, vLightHelper, vAlwaysLookAt } from '@tresjs/cientos';
import HoustonModel from './HoustonModel.vue';
import { useControls } from '@tresjs/leches';

/* const gl = {
  clearColor: '#181c3e',
  shadows: true,
  alpha: false,
  shadowMapType: BasicShadowMap,
  outputColorSpace: SRGBColorSpace,
  toneMapping: NoToneMapping
}; */

const { value: position } = useControls({
  position: new Vector3(-3, 3, 3)
});

const { value: distance } = useControls({
  distance: 1
});

const { value: decay } = useControls({
  decay: 3
});

const { value: penumbra } = useControls({
  penumbra: 0.5
});
</script>

<template>
  <TresCanvas clear-color="black" shadows>
    <TresPerspectiveCamera :position="[5, 5, 5]" :look-at="[0, 1, 0]" />
    <!-- <Stars /> -->
    <OrbitControls />
    <!-- <Suspense>
      <HoustonModel />
    </Suspense> -->
    <TresGroup>
      <TresMesh cast-shadow receive-shadow :position="[0, 2, 0]">
        <TresTorusGeometry :args="[1, 0.4, 32, 32]" />
        <TresMeshStandardMaterial color="white" />
      </TresMesh>
      <TresMesh cast-shadow :position="[-4, 2, 0]">
        <TresTorusKnotGeometry :args="[1, 0.4, 32, 32]" />
        <TresMeshStandardMaterial color="white" />
      </TresMesh>
      <TresMesh cast-shadow :position="[2, 4, 2]">
        <TresBoxGeometry :args="[2, 2, 2]" />
        <TresMeshStandardMaterial color="white" />
      </TresMesh>
    </TresGroup>
    <TresMesh receive-shadow :rotate-x="-Math.PI / 2">
      <TresPlaneGeometry :args="[15, 15]" />
      <TresMeshStandardMaterial color="white" />
    </TresMesh>
    <TresAmbientLight :intensity="1" />
    <!-- <TresDirectionalLight
      :position="[-4, -2, 2]"
      :intensity="1"
      cast-shadow
      color="#fff"
      v-light-helper
    /> -->
    <TresDirectionalLight
      :position="[5, 8, 3]"
      :args="['white', 2]"
      cast-shadow
      :shadow-mapSize-width="2048"
      :shadow-mapSize-height="2048"
      :shadow-camera-near="0.1"
      :shadow-camera-far="1000"
      :shadow-radius="10"
      v-light-helper
    />
    <TresHemisphereLight :args="['red', 'blue', 0.5]" v-light-helper />
    <TresPointLight
      :args="['yellow', 2]"
      :position="[10, 10, 10]"
      :distance="7"
      :decay="3"
      v-light-helper
    />
    <TresSpotLight
      :args="['white', 9]"
      :angle="Math.PI / 4"
      :distance="distance"
      :decay="decay"
      :position-x="position.x"
      :position-y="position.y"
      :position-z="position.z"
      :penumbra="penumbra"
      cast-shadow
      :shadow-radius="5"
      v-light-helper
    />
    <TresRectAreaLight
      :args="['hotpink', 2, 5, 5]"
      :position="[0, 1, 2]"
      v-always-look-at="[-4, 0, 0]"
    />
  </TresCanvas>
</template>
