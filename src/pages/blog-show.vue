<template>
  <q-page class="items-center justify-evenly">
    <component :is="name"></component>
  </q-page>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import StartBlog from '../blogs/start-blog.vue';
export default defineComponent({
  components: { StartBlog },
  setup() {
    const name = localStorage.getItem('blogName');
    return {
      name,
    };
  },
});
</script>

<style scoped lang="scss">
</style>
