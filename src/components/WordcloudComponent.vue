<template>
  <div id="word-cloud"></div>
</template>

<script lang="ts" setup>
import { onMounted } from 'vue';
import WordCloud from 'wordcloud';
onMounted(() => {
  initWordCloud();
});

const initWordCloud = () => {
  const list = [
    ['Javascript', 50],
    ['TypeScript', 20],
    ['Vue', 60],
    ['React', 20],
    ['Angular', 30],
    ['Node.js', 36],
    ['HTML', 30],
    ['CSS', 20],
    ['UI frameworks', 25],
    ['micro frontend', 18],
    ['CI/CD', 22],
  ];
  WordCloud(document.getElementById('word-cloud'), {
    backgroundColor: '#014a88',
    list: list,
  });
};
</script>

<style scoped lang="scss">
#word-cloud {
  width: 300px;
  height: 300px;
}
</style>
