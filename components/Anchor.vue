<template>
  <NuxtLink v-if="anchorTo" tag="a" :to="anchorTo">
    <slot>{{ text }}</slot></NuxtLink
  >
  <a v-else :href="anchorHref"
    ><slot>{{ text }}</slot></a
  >
</template>

<script lang="ts" setup>
const anchorProps = defineProps({
  text: {
    type: String,
    default: ''
  },
  to: {
    type: [String, Object],
    default: undefined
  },
  href: {
    type: String,
    default: ''
  }
})

const anchorHref = toRef(anchorProps, 'href')
const anchorTo = toRef(anchorProps, 'to')
</script>

<style></style>
