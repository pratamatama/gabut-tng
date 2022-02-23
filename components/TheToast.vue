<template>
  <Transition
    enter-active-class="duration-300 ease-out"
    enter-from-class="transform opacity-0"
    enter-to-class="opacity-100"
    leave-active-class="duration-200 ease-in"
    leave-from-class="opacity-100"
    leave-to-class="transform opacity-0"
  >
    <div
      v-if="visible"
      class="p-4 py-2 fixed bottom-10 left-1/2 transform -translate-x-1/2 rounded-lg text-center"
    >
      <slot>Hello from Toast!</slot>
    </div>
  </Transition>
</template>

<script>
export default {
  props: {
    visible: {
      type: Boolean,
      default: false,
    },
  },
}
</script>