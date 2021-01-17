<template>
  <div
    v-if="loading"
    class="h-screen flex justify-center items-center p-4 text-white text-4xl lg:text-6xl transition duration-500"
    :class="bg"
  >
    Fetching data
    <span v-for="dot in dots" :key="dot">.</span>
  </div>
  <div v-else>
    {{results}}
  </div>
</template>

<script>

export default {
  name: 'Results',
  props: {
    results: {
      type: Array,
      required: false
    },
    loading: {
      type: Boolean,
      required: true
    }
  },
  data () {
    return {
      bg: 'bg-gray-800',
      dots: 0
    }
  },
  mounted () {
    setInterval(() => {
      this.dots = (this.dots + 1)%4
    }, 1000)

    setInterval(() => {
      this.bg = this.bg === 'bg-gray-700' ? 'bg-gray-800' : 'bg-gray-700'
    }, 500)
  }
}
</script>
