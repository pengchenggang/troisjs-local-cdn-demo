<template>
  <Renderer :params="{ }" ref="renderer" antialias :orbit-ctrl="{ enableDamping: true }" resize="window" :pixel-ratio="pixelRatio">
    <Camera :position="{ z: 10 }" />
    <Scene>
      <PointLight :position="{ y: 50, z: 50 }" />
      <Box :size="1" ref="box" :rotation="{ y: Math.PI / 4, z: Math.PI / 4 }">
        <LambertMaterial><Texture src="" /></LambertMaterial>
      </Box >
    </Scene>
  </Renderer>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { Box, Camera, LambertMaterial, MeshPublicInterface, PointLight, Renderer, RendererPublicInterface, Scene, Texture } from './export'

export default defineComponent({
  components: { Box, Camera, LambertMaterial, PointLight, Renderer, Scene, Texture },
  data () {
    return {
      pixelRatio: window.devicePixelRatio,
    }
  },
  mounted() {
    const renderer = this.$refs.renderer as RendererPublicInterface
    const mesh = (this.$refs.box as MeshPublicInterface).mesh
    if (renderer && mesh) {
      renderer.onBeforeRender(() => {
        mesh.rotation.x += 0.01
      })
    }
  },
})
</script>

<style>
body, html {
  margin: 0;
}
canvas {
  display: block;
  width: 100%;
  height: 100%;
}
</style>
