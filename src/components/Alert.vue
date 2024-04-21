<template>
  <p :class="isError">
    {{ alert.message }}
  </p>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  alert: {
    type: Object,
    required: true
  }
})

const isError = computed(() => props.alert.type === 'error' ? 'text-red-500' : 'text-green-500');
</script>
