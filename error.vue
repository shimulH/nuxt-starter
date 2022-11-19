<template>
  <div class="min-h-screen flex items-center justify-center">
    <ErrorDisplay :code="parseInt(error.statusCode)" />
  </div>
</template>

<script setup>
// default props available on error.vue
const props = defineProps({
  error: Object,
});

const error = useError();
</script>
