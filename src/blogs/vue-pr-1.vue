<template>
  <h2>Before</h2>
  <article>
    <p>
      Before writing this content, I was very hesitant. After all, this is a
      relatively difficult content,I'm not that senior front-end engineer
      either. If my description is not professional and not easy to understand,
      it will be a disaster blog.However, I am still happy to share my insights
      on these principles. If there are any questions, I hope you can
      communicate with me and discuss these issues together.
    </p>
  </article>
  <h2>Analysis of Vue Principle --- MVVM</h2>
  <h3>what is MVVM?</h3>
  <article>
    <p>
      As we all know, vue is an MVVM progressive framework. MVVM is the design
      pattern of vue. In the vue framework, data will automatically drive the
      view.
    </p>
    <q-img src="../assets/vue/mvvm.png" />
    <p>
      There is an introduction to the MVVM pattern on the Vue official website.
    </p>
    <p>
      As shown above, The View layer and the Model layer are not directly
      connected, but interact through the ViewModel layer.The ViewModel layer
      connects the View layer and the Model layer through two-way data binding,
      so that the synchronization between the View layer and the Model layer is
      completely automatic.
    </p>
    <p>
      In the traditional development mode, we need to frequently operate the DOM
      in the js code. For example
    </p>
    <p>
      <input v-model="number_1" type="number" />
      +
      <input v-model="number_2" type="number" />
      =
      {{ number_1 + number_2 }}
    </p>
    <p>
      As shown above, When we need to dynamically calculate the sum of two
      numbers,it is easy to use the framework of vue.
    </p>
    <p>
    <pre v-html="html"></pre>
    </p>
    <p>
      However, if use traditional framework like JQuery, First we need to monitor the update of the two input boxes,
      then sum the values in the input boxes and render them to the dom; At this time, our operations of monitoring dom
      and rendering dom are in js.Although the framework of vue also achieves the same function through js operation, it
      is already encapsulated, This encapsulated way is viewModel. This is what the vue official website says, Vue.js is
      focused on the ViewModel layer of the MVVM pattern.
    </p>
    <h3>how to achieve it?</h3>
    <p>
      When we know what MVVM is, the next step is how do they implement the two-way binding in MVVM?
    </p>
    <p>There are several ways to implement two-way data binding! like Dirty Checking in Angular or Data hijacking
      in vue.Next, in the next chapter, i will introduce in detail how vue's data hijacking is implemented.
    </p>
    <p>
      Thanks for reading!
    </p>
  </article>
</template>

<script lang="ts" setup>
import Prism from 'prismjs';
import { ref } from 'vue';
const number_1 = ref(0);
const number_2 = ref(0);
const code = `<div>
      <input v-model="number_1" type="number" />
      +
      <input v-model="number_2" type="number" />
      =
      {{ number_1 + number_2 }}
</div>`;

// Returns a highlighted HTML string
const html = Prism.highlight(code, Prism.languages.html, 'html');
</script>

<style scoped lang="scss">
.q-img {
  max-width: 500px;
  margin: 10px auto;
  margin-left: 20px;
}

input {
  width: 40px;
}
</style>
