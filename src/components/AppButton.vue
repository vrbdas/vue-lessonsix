<script setup>
  import { defineProps, defineEmits } from 'vue';
  const props = defineProps(['btnClass', 'btnText']);
  const emits = defineEmits(['btnAction']);
</script>

<template>
  <button 
    :class="btnClass"
    @click="$emit('btnAction')"
    >
    {{ btnText }}
  </button>
</template>

<style scoped lang="scss">

</style>