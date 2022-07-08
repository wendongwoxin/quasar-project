<template>
  <q-page class="row items-center justify-evenly">
    <q-card dark bordered class="bg-grey-9 my-card">
      <q-card-section>
        <div class="text-h6">About me</div>
        <div class="text-subtitle2">front end engineer</div>
      </q-card-section>

      <q-separator dark inset />

      <q-card-section>
        <p>
          I, Jinwen Wu, graduated from Hefei University of Technology with a
          major in Computer and Science, now a front-end development engineer.
        </p>
        <p>
          I am now working in Hefei, responsible for the development of some web
          pages, technical research, etc.
        </p>
        <p>
          I am looking forward to learning and sharing front-end related
          knowledge with you all, Of course, I will not refuse other related
          technologies.This is also the original intention of my blog.
        </p>
        <p>
          Besides, I'm a big fan of games, except 3D games.Therefore, if you
          want to find a friend who can play games with you, you can also try to
          contact me.
        </p>
      </q-card-section>
    </q-card>
    <article>
      <h1>The Skills</h1>
      <ul>
        <li>
          A solid foundation in JavaScript, proficient in the use of the <a style="color:green" href="https://vuejs.org/" target="'_blank'">Vue</a>
          series technology stack, and completed more than 20 project
          development from zero to one.
        </li>
        <li>
          Have the design and development capabilities of general components,
          complete the development of more than n components.
        </li>
        <li>
          Able to develop independently or collaboratively, with open source
          experience and leading experience
        </li>
        <li>
          Have experience in business system architecture design and R&D, and
          have completed more than n system business architecture design and
          development
        </li>
      </ul>
    </article>
    <div>
      <h2>tech stack</h2>
      <wordcloud-component></wordcloud-component>
    </div>
  </q-page>
</template>

<script lang="ts" setup>
import WordcloudComponent from 'components/WordcloudComponent.vue';
</script>

<style scoped lang="scss">
h1 {
  color: blueviolet;
  font-weight: bold;
  text-align: left;
}
h2 {
  color: burlywood;
  font-weight: bold;
}
.my-card {
  max-width: 450px;
  + .my-card {
    margin-left: 20px;
  }
}

article {
  max-width: 450px;
  color: #fff;
  li {
    font-size: 16px;
    + li {
      margin-top: 10px;
    }
  }
}
</style>
