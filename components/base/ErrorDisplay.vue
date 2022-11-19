<template>
  <div>
    <h1 class="text-center mb-6 leading-3">
      <span class="font-bold text-8xl block">{{ error.code }}</span>
      <span class="block italic">{{ error.message }}</span>
    </h1>
    <Button @click="handleError" text="Home" size="sm" />
  </div>
</template>

<script setup>
const props = defineProps({
  code: {
    type: Number,
    default: 400,
  },
});

const errorsMap = {
  400: 'Bad Request',
  401: 'Unauthorized',
  403: 'Forbidden',
  404: 'Not Found',
};

const error = computed(() => {
  const { code } = props;
  return {
    code,
    message: errorsMap[code.toString()] || 'Unknown Error',
  };
});

// clear error and redirect to home page
const handleError = () => {
  clearError({ redirect: '/' });
};
</script>
