<template>
  <div id="app">
    <WordSphere id="id_sphere_object" ref="ref_sphere_object"
        :items_list="sphere_items"
        :radius="12"
        :text_color="'red'"
        :font_size_max="2"/>
  </div>
</template>

<script>
import { defineComponent } from 'vue';
import WordSphere from '@/WordSphere.vue';

export default defineComponent({
  name: 'ServeDev',
  components: {
    WordSphere
  },
  data() {
    return {
      sphere_items: [
        "Robotics",
        "Software",
        "3D Dev",
        "Interface",
        "Firmware",
        "Front-end",
        "Algorithms",
        "Procedural",
        "Database",
        "3D Design",
        "Electronics"
      ]
    }
  }
});
</script>

<style scoped>
  .container {
    background: red;
    height: 100vh;
    width: 100vw;
    top: 0;
    left: 0;
    min-height: 100%;
    min-width: 100%;
  }
</style>
