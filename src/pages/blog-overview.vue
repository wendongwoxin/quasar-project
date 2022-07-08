<template>
  <q-page class="q-px-lg q-pb-md">
    <q-timeline dark :layout="layout" color="secondary">
      <q-timeline-entry heading> My Blogs </q-timeline-entry>

      <q-timeline-entry
        v-for="item in list"
        :key="item.title"
        :title="item.title"
        :subtitle="item.subtitle"
        :side="item.side"
        :icon="item.icon"
        @click="showBlog(item)"
      >
        <div>
          {{ item.content }}
        </div>
      </q-timeline-entry>
    </q-timeline>
  </q-page>
</template>

<script>
import { useQuasar } from 'quasar';
import { computed } from 'vue';

export default {
  setup() {
    const $q = useQuasar();

    const list = [
      {
        title: 'Welcome to my Blog',
        subtitle: 'July 8, 2022',
        content: 'How to have your own blog? Why i Blog?',
        side: 'left',
        icon: 'done',
        path: 'StartBlog'
      },
      {
        title: 'Welcome to my Blog',
        subtitle: 'July 8, 2022',
        content: 'How to have your own blog? Why i Blog?',
        side: 'right',
        icon: 'done',
        path: 'start'
      },
    ];

    const showBlog = (item) => {
        localStorage.setItem('blogName', item.path)
        window.location.href = `#/blog-show`
    }
    return {
      list,
      showBlog,
      layout: computed(() => {
        return $q.screen.lt.sm
          ? 'dense'
          : $q.screen.lt.md
          ? 'comfortable'
          : 'loose';
      }),
    };
  },
};
</script>
