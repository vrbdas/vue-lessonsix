<script setup>
import { inject } from 'vue';
const vueNews = inject('vueNews');
</script>

<template>
  <div class="news-list">
    <hr>
    <h4 class="news-list__title">List of all news</h4>
    <ul>
      <li v-for="item in vueNews" :key="item.id"
        :class="item.isRead === true ? 'news-list__li news-list__li_read' : 'news-list__li'">
        {{ item.title }}
      </li>
    </ul>
  </div>
</template>

<style scoped lang="scss">
$first: #fff;
$second: #FF9F1C;
$third: #FFBF69;
$fourth: #CBF3F0;
$fifth: #2EC4B6;

.news-list {
  display: grid;
  gap: 10px;

  &__title {
    font-weight: 600;
  }

  &__li {
    list-style: none;
    font-size: 0.8rem;

    &_read {
      color: $fifth;
    }
  }
}
</style>