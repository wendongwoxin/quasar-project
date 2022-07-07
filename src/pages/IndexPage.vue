<template>
  <q-page class="row items-center justify-evenly">
    <introduce-component></introduce-component>
  </q-page>
</template>

<script lang="ts">
import introduceComponent from 'components/introduceComponent.vue'
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'IndexPage',
  components: { introduceComponent },
});
</script>
