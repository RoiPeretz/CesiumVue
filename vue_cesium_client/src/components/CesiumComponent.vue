<script lang="ts">
import { defineComponent, onMounted, ref } from "vue";
import { Cartesian3, Viewer, Terrain } from "cesium";
import "cesium/Build/Cesium/Widgets/widgets.css";

export default defineComponent({
  name: "CesiumComponent",
  setup() {
    const cesiumContainer = ref<HTMLElement | null>(null);

    onMounted(() => {
      if (!cesiumContainer.value) return;

      const viewer: Viewer = new Viewer(cesiumContainer.value, {
        terrain: Terrain.fromWorldTerrain(),
      });

      viewer.camera.flyTo({
        destination: Cartesian3.fromDegrees(-117.16, 32.71, 15000.0),
      });
    });

    return { cesiumContainer };
  },
});
</script>

<template>
  <div class="viewer" ref="cesiumContainer"></div>
</template>

<style>
@import url("/node_modules/cesium/Build/Cesium/Widgets/widgets.css");

.viewer {
  width: 100%;
  height: 100%;
  margin: 0;
  padding: 0;
  overflow: hidden;
  position: absolute;
}
</style>
