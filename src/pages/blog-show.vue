<template>
  <q-page class="items-center justify-evenly">
    <component :is="name"></component>
    <div class="page-change">
      <div class="page" v-if="index !== 0">
        <a
          class="pager-link prev"
          @click="pagerTo(index, false)"
          ><span class="desc" data-v-176f99de="">Previous page</span
          ><span class="title" data-v-176f99de="">{{list[index - 1]}}</span></a
        >
      </div>
      <div
        class="page"
        style="padding-left: 16px"
        v-if="index + 1 < list.length"
      >
        <a
          class="pager-link prev"
          @click="pagerTo(index, true)"
          ><span class="desc" data-v-176f99de="">next page</span
          ><span class="title" data-v-176f99de="">{{list[index + 1]}}</span></a
        >
      </div>
    </div>
  </q-page>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import StartBlog from '../blogs/start-blog.vue';
import vuePrinciple_1 from '../blogs/vue-pr-1.vue'
import vuePrinciple_2 from '../blogs/vue-pr-2.vue'
import vuePrinciple_3 from '../blogs/vue-pr-3.vue'
import vuePrinciple_4 from '../blogs/vue-pr-4.vue'
export default defineComponent({
  components: { StartBlog, vuePrinciple_1, vuePrinciple_2, vuePrinciple_3, vuePrinciple_4 },
  setup() {
    const list: string[] = ['StartBlog', 'vuePrinciple_1', 'vuePrinciple_2', 'vuePrinciple_3', 'vuePrinciple_4'];
    let name = ref(localStorage.getItem('blogName'));
    let index = ref(-1);
    if (name.value) index.value = list.indexOf(name.value);

    const pagerTo = (i:number, type:boolean) => {
      if (type) {
        name.value = list[i + 1]
      } else {
        name.value = list[i - 1]
      }
      localStorage.setItem('blogName', name.value)
      if (name.value) index.value = list.indexOf(name.value);
    }
    return {
      name,
      list,
      index,
      pagerTo
    };
  },
});
</script>

<style scoped lang="scss">
.q-page {
  margin: 0 10px;
}
.page-change {
  width: 70%;
  display: flex;
  border-top: 1px solid rgba(255, 255, 255, 0.2);
  padding: 20px 0;
  .page {
    display: flex;
    flex-direction: column;
    flex-shrink: 0;
    width: 50%;
    .pager-link {
      display: block;
      border: 1px solid rgba(255, 255, 255, 0.2);
      border-radius: 8px;
      padding: 11px 16px 13px;
      width: 100%;
      height: 100%;
      transition: border-color 0.25s;
      text-decoration: none;
      .desc {
        display: block;
        line-height: 20px;
        font-size: 12px;
        font-weight: 500;
        color: rgba(255, 255, 255, 0.7);
      }
      .title {
        display: block;
        line-height: 20px;
        font-size: 14px;
        font-weight: 500;
        color: #42b883;
        transition: color 0.25s;
      }
    }
  }
}
</style>
