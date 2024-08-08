<script setup>
import { ref, provide } from 'vue';
import AppNews from './components/AppNews.vue';

const currentDate = ref(new Date());
const options = {
  day: '2-digit',
  month: 'short',
  year: 'numeric'
};
const vueNews = ref([
  {
    id: 1,
    title: "Vue 3.2 released with enhanced reactivity and improved TypeScript support.",
    content: "The Vue.js team has officially released version 3.2, bringing significant improvements to reactivity and TypeScript support. This release focuses on performance optimizations and developer experience enhancements. Key features include better integration with TypeScript, new APIs for creating reactive objects, and improvements to the Composition API. Developers can now build more efficient and maintainable applications with these updates.",
    isOpen: false,
    isRead: false,
  },
  {
    id: 2,
    title: "Nuxt 3 enters beta, promising faster performance and new features.",
    content: "Nuxt.js, the popular framework for building Vue.js applications, has announced the beta release of Nuxt 3. This version aims to deliver faster performance, thanks to a new server engine and optimized rendering process. Nuxt 3 also introduces new features such as automatic component imports, enhanced static site generation, and improved developer tools. The community is eagerly testing these new capabilities to provide feedback before the stable release.",
    isOpen: false,
    isRead: false,
  },
  {
    id: 3,
    title: "Vue Conf 2024 announced, featuring workshops and talks from core team members.",
    content: "The highly anticipated Vue Conf 2024 has been officially announced, promising a lineup of engaging workshops and talks from Vue.js core team members and industry experts. Scheduled to take place in April, the conference will cover the latest advancements in Vue.js, best practices for development, and real-world case studies. Attendees will have the opportunity to network with other developers, participate in hands-on sessions, and gain insights into the future of the Vue ecosystem.",
    isOpen: false,
    isRead: false,
  },
  {
    id: 4,
    title: "Vue Storefront gains traction as a leading e-commerce frontend framework.",
    content: "Vue Storefront continues to gain popularity as a leading e-commerce frontend framework, providing a modern and performant solution for online retailers. Built with Vue.js, it offers a fully customizable and platform-agnostic approach to building storefronts. Recent updates include improved integration with popular e-commerce platforms, new plugins for extended functionality, and enhanced performance optimizations. Businesses adopting Vue Storefront are seeing significant improvements in their site speed, user experience, and overall conversion rates.",
    isOpen: false,
    isRead: false,
  },
  {
    id: 5,
    title: "Pinia becomes the official state management library for Vue 3.",
    content: "The Vue.js team has officially designated Pinia as the state management library for Vue 3. Pinia offers a more intuitive and flexible approach to managing application state, with a focus on simplicity and modularity. It leverages the Composition API introduced in Vue 3, providing a seamless and powerful state management experience. Pinia's adoption has been rapidly growing, with many developers praising its ease of use and robust features. This endorsement by the Vue.js team marks a significant milestone in its development.",
    isOpen: false,
    isRead: false,
  }
]);
const openedCount = ref(0);
const readCount = ref(0);

provide('vueNews', vueNews);

function openCard(id) {
  const idx = vueNews.value.findIndex((value) => value.id === id);
  vueNews.value[idx].isOpen = true;
}

function closeCard(id) {
  const idx = vueNews.value.findIndex((value) => value.id === id);
  vueNews.value[idx].isOpen = false;
}

function markRead(id) {
  const idx = vueNews.value.findIndex((value) => value.id === id);
  vueNews.value[idx].isRead = true;
  closeCard(id);
  readCount.value++;
}

function markUnread(id) {
  const idx = vueNews.value.findIndex((value) => value.id === id);
  vueNews.value[idx].isRead = false;
  readCount.value--;
}

</script>

<template>
  <main>
    <div class="container">
      <section class="news">
        <h2 class="news__title">Actual News on {{ currentDate.toLocaleDateString('en-UK', options) }}</h2>
        <p>Opened: <strong>{{ openedCount }}</strong> | Read: <strong>{{ readCount }}</strong></p>
        <div class="news__cards">
          <app-news v-for="card in vueNews" :key="card.id" :card="card" :openCard="openCard" :closeCard="closeCard" :markRead="markRead" :markUnread="markUnread"></app-news>
        </div>
      </section>
    </div>
  </main>
</template>

<style scoped lang="scss">
$first: #fff;
$second: #FF9F1C;
$third: #FFBF69;
$fourth: #CBF3F0;
$fifth: #2EC4B6;

main {
  height: 100vh;
  background-color: $first;
  padding: 40px 0;
}

.container {
  width: 1320px;
  margin: 0 auto;
}

.news {
  display: flex;
  flex-direction: column;
  gap: 20px;

  &__title {
    font-weight: 800;
    font-size: 2rem;
  }

  &__cards {
    display: grid;
    grid-template-columns: 1fr;
    gap: 20px;
    width: 50%;
  }
}

strong {
  font-weight: 600;
}

</style>
