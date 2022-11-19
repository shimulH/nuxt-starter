<template>
  <div>
    <Link
      rel="stylesheet"
      href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.10.2/font/bootstrap-icons.css"
    />
    <header
      class="bg-gray-200 text-[#002D74] py-3.5 px-6 shadow md:flex justify-between items-center"
    >
      <div class="flex items-center cursor-pointer">
        <span class="text-[#002D74] text-xl mr-1"></span>
        <h1 class="text-xl">Boom</h1>
      </div>

      <span
        @click="openNavMenu()"
        class="absolute md:hidden right-6 top-1.5 cursor-pointer text-4xl"
      >
        <i :class="[isOpen ? 'bi bi-x' : 'bi bi-filter-left']"></i>
      </span>

      <ul
        class="md:flex md:items-center md:px-0 px-10 md:pb-0 pb-10 md:static absolute bg-gray-200 md:w-auto w-full"
        :class="[isOpen ? 'left-0' : 'left-[-100%]']"
      >
        <li
          class="md:mx-4 md:my-0 my-6"
          v-for="(navLink, i) in navLinks"
          :key="i"
        >
          <BaseAnchor
            v-if="navLink.type === 'link'"
            :to="navLink.route ? navLink.route : undefined"
            :href="navLink.href ? navLink.href : undefined"
            class="text-xl hover:text-[#002D80]"
            >{{ navLink.name }}</BaseAnchor
          >
          <BaseButton
            v-else-if="navLink.type === 'button'"
            :text="navLink.name"
            size="md"
            class="capitalize"
            :to="navLink.route ? navLink.route : undefined"
            >Login</BaseButton
          >
        </li>
      </ul>
    </header>
  </div>
</template>

<script lang="ts" setup>
const isOpen = ref<boolean>(false);

const navLinks = computed((): any => [
  { name: 'Home', type: 'link', route: { name: 'home' } },
  { name: 'About', type: 'link', route: { name: 'home' } },
  { name: 'Blog', type: 'link', route: { name: 'home' } },
  { name: 'Services', type: 'link', route: { name: 'home' } },
  { name: 'Contact', type: 'link', route: { name: 'home' } },
  { name: 'Login', type: 'button', route: { name: 'home' } },
]);

const openNavMenu = () => (isOpen.value = !isOpen.value);
</script>
