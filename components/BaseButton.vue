<template>
  <button
    class="px-4 py-3 font-medium tracking-widest uppercase flex items-center rounded-lg"
    @click="$emit('click')"
  >
    <slot />
  </button>
</template>