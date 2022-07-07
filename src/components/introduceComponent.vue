<template>
  <div>
    <h3>Wendongwoxin's Blog</h3>
    <article>
      <p>
        Hi, I'm Jinwen Wu, a Front-end engineer from China! I'm glad you all saw
        my blog from so many sites,If you find me an interesting person in the
        process of browsing the blog, you can communicate with me by email, we
        can share and learn together.
      </p>
    </article>
    <div class="row">
      <q-card class="my-card">
        <img src="https://cdn.quasar.dev/img/mountains.jpg" />

        <q-card-section>
          <div class="text-h6">My Blogging Purpose</div>
          <div class="text-subtitle2">
            written by <a target="_blank" href="https://quasar.dev/">Quasar</a>
          </div>
        </q-card-section>

        <q-card-section class="q-pt-none">
          <router-link to="purpose">
            {{ purpose }}
          </router-link>
        </q-card-section>
      </q-card>

      <q-card class="my-card">
        <img src="https://cdn.quasar.dev/img/parallax1.jpg" />

        <q-card-section>
          <div class="text-h6">Getting In Touch</div>
          <!-- <div class="text-subtitle2">by John Doe</div> -->
        </q-card-section>

        <q-card-section class="q-pt-none">
          <q-btn no-caps flat :icon="mdiGithub" @click="navToGit">https://github.com/wendongwoxin</q-btn>
          <q-btn no-caps flat icon="email">1844287682@qq.com</q-btn>
        </q-card-section>
      </q-card>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { mdiGithub } from '@quasar/extras/mdi-v6';
const purpose = 'share what I learned, to be a writer';
const navToGit = () => {
  window.open('https://github.com/wendongwoxin')
}
</script>

<style scoped lang="scss">
a:-webkit-any-link {
  text-decoration: none;
  color: #000;
}
h3 {
  font-weight: 700;
  color: yellow;
}
article {
  color: white;
  max-width: 500px;
  font-size: 14px;
}
.row {
  // flex-wrap: nowrap;
}
.my-card {
  max-width: 450px;
  + .my-card {
    margin-left: 20px;
  }
}
</style>
