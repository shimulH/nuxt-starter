<template>
  <NuxtLink
    v-if="to"
    tag="a"
    :to="to"
    :class="`${defaultStyle} ${defineStyle} ${defineSize}`"
  >
    <slot>{{ text }}</slot>
  </NuxtLink>
  <a
    v-else
    :class="`${defaultStyle} ${defineStyle} ${defineSize}`"
    :href="href"
    @click="onClick"
  >
    <slot>{{ text }}</slot>
  </a>
</template>

<script lang="ts" setup>
const buttonProps = defineProps({
  text: {
    type: String,
    default: '',
  },
  type: {
    type: String,
    default: 'primary',
  },
  to: {
    type: [String, Object],
    default: undefined,
  },
  href: {
    type: String,
    default: undefined,
  },
  size: {
    type: String,
    default: 'md',
  },
});

const defaultStyle = `
  bg-[#002D74] hover:bg-[#002D50] duration-300 font-sm text-white rounded py-1.5 px-4
    cursor-pointer
    border transition-color duration-300
    focus:outline-none focus:ring-1 focus:ring-offset-1 focus:dark:ring-offset-gray-50 focus:dark:ring-gray-400 focus:ring-gray-600/[0.6] focus:ring-offset-gray-800/[0.6]
    flex items-center justify-center font-semibold
  `;

const styles = reactive<{
  [key: string]: string;
}>({
  none: '',
  primary: 'text-white bg-primary-500 hover:bg-primary-400 border-primary-500',
  secondary:
    'text-slate-800 bg-gray-200 border-gray-200 hover:bg-gray-300 dark:text-white dark:border-slate-800 dark:bg-slate-800 dark:hover:bg-slate-700',
  opposite:
    'text-white bg-gray-800 hover:bg-white hover:text-gray-800 hover:border-gray-900 dark:text-gray-800 dark:bg-gray-100 dark:hover:bg-gray-800 dark:hover:text-gray-100 dark:border-white',
});

const sizes = reactive<{
  [key: string]: string;
}>({
  lg: 'h-13 px-8 text-lg rounded-lg',
  md: 'h-10 px-6 text-base rounded',
  sm: 'h-9 px-4 text-sm rounded',
  xs: 'h-6 px-3 text-xs rounded',
});

const defineStyle = computed(() =>
  buttonProps.type in styles ? styles[buttonProps.type] : styles.primary
);
const defineSize = computed(() => sizes[buttonProps.size] || sizes.lg);

const onClick = (event: MouseEvent) => {
  const router = useRouter();
  if (buttonProps.to) {
    router.push(buttonProps.to);
  }
  if (!buttonProps.href) {
    event.preventDefault();
  }
};
</script>
