<script setup>
import { ref, defineProps } from 'vue';
import AppButton from './AppButton.vue';
import AppNewsList from './AppNewsList.vue';
const props = defineProps(['card', 'openCard', 'closeCard', 'markRead', 'markUnread']);
</script>

<template>
  <div class="card">
    <h3 class="card__title" :class="card.isRead ? 'card__title_read' : ''">
      {{ card.title }}
      <app-button 
        :btnClass="!card.isOpen  ? 'icon-circle-down' : 'icon-circle-down icon-circle-down_rotate'" 
        @btnAction="!card.isOpen ? openCard(card.id) : closeCard(card.id)"
      ></app-button>
    </h3>
    <transition name="fade">
      <div class="card__content" v-show="card.isOpen">
        <p>{{ card.content }}</p>
        <app-button 
          :btnClass="!card.isRead ? 'card__content-btn' : 'card__content-btn card__content-btn_read'"
          :btnText="!card.isRead ? 'mark as read' : 'mark as unread'"
          @btnAction="!card.isRead ? markRead(card.id) : markUnread(card.id)"
        ></app-button>
        <app-news-list></app-news-list>
      </div>
    </transition>
  </div>
</template>

<style scoped lang="scss">
$first: #fff;
$second: #FF9F1C;
$third: #FFBF69;
$fourth: #CBF3F0;
$fifth: #2EC4B6;

.card {
  display: flex;
  flex-direction: column;
  justify-content: center;
  position: relative;

  &__title {
    border-radius: 5px;
    padding: 20px;
    font-weight: 600;
    font-size: 1.3rem;
    position: relative;
    background-color: $third;

    &_read {
      background-color: $fifth;
    }
  }

  &__content {
    transform: translateX(4%);
    background-color: $fourth;
    border-radius: 5px;
    padding: 20px;
    display: grid;
    gap: 10px;

    &-btn {
      width: fit-content;
      font-size: 1rem;
      cursor: pointer;
      text-transform: uppercase;
      border: none;
      background-color: $third;
      border-radius: 5px;
      padding: 5px;
      font-weight: 500;
      justify-self: end;

      &_read {
        background-color: $fifth;
      }
    }
  }
}

.icon-circle-down {
  position: absolute;
  left: 0;
  bottom: 0;
  transform: translateX(50%) translateY(50%);
  z-index: 1;
  display: block;
  font-size: 1.5rem;
  cursor: pointer;
  transition: 0.5s all;
  border: none;
  background-color: transparent;

  &_rotate {
    transform: translateX(50%) translateY(50%) rotate(-90deg);
  }
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
