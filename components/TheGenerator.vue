<template>
  <main class="h-screen flex flex-col items-center justify-center">
    <img
      class="-mt-10 mb-10"
      src="/logo.png"
      alt="GABUT ! Logo"
      width="100"
    />

    <h1 class="text-3xl sm:text-5xl lg:text-7xl xl:text-8xl 2xl:text-9xl text-center font-bold select-none mb-10">
      {{ formattedNumber }}
    </h1>

    <div class="flex items-center">
      <BaseButton
        class="bg-pink-600 hover:bg-pink-700 text-white"
        @click="generate"
      >generate</BaseButton>

      <BaseButton
        class="text-pink-600 ml-4"
        @click="copy"
      >
        <!-- boxicons: copy-alt -->
        <svg
          class="h-6 w-6"
          xmlns="http://www.w3.org/2000/svg"
          width="100%"
          height="100%"
          viewBox="0 0 24 24"
          fill="currentColor"
        >
          <path d="M20 2H10c-1.103 0-2 .897-2 2v4H4c-1.103 0-2 .897-2 2v10c0 1.103.897 2 2 2h10c1.103 0 2-.897 2-2v-4h4c1.103 0 2-.897 2-2V4c0-1.103-.897-2-2-2zM4 20V10h10l.002 10H4zm16-6h-4v-4c0-1.103-.897-2-2-2h-4V4h10v10z"></path>
          <path d="M6 12h6v2H6zm0 4h6v2H6z"></path>
        </svg>
        <span class="ml-4">copy</span>
      </BaseButton>
    </div>

    <TheCopyright />

    <TheToast
      class="bg-gray-700 text-white"
      :visible="copied"
    >Item copied to the clipboard</TheToast>
  </main>
</template>

<script>
export default {
  data() {
    return {
      timer: null,
      copied: false,
      max_length: 8,
      numbers: Array(8).fill(0),
    }
  },
  computed: {
    formattedNumber() {
      return this.numbers.join(' ')
    },
  },
  destroyed() {
    this.clearTimer()
  },
  methods: {
    /**
     * Free up resource used by the timer.
     *
     * @return void
     */
    clearTimer() {
      if (this.timer) clearTimeout(this.timer)
    },

    /**
     * Copy the number to the clipboard.
     *
     * @return void
     */
    copy() {
      this.clearTimer()

      if (process.browser) {
        navigator.clipboard.writeText(this.formattedNumber)
        this.copied = true

        this.timer = setTimeout(() => {
          this.copied = false
        }, 3000)
      }
    },

    /**
     * Generate number between min and max.
     *
     * @return {Number}
     */
    generateBetween(min, max) {
      return Math.floor(Math.random() * (max - min + 1) + min)
    },

    /**
     * Generate and display togel number.
     *
     * @return void
     */
    generate() {
      let numbers = []

      for (let i = 1; i <= this.max_length; i++) {
        const generated = this.generateBetween(
          1,
          i >= this.max_length ? 20 : 35
        )

        if (numbers.includes(generated)) {
          return this.generate()
        }

        numbers = [...numbers, generated]
      }

      this.numbers = numbers
    },
  },
}
</script>