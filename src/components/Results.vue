<template>
  <div
    v-if="status === 'loading'"
    class="h-screen flex justify-center items-center p-4 text-white text-4xl text-center lg:text-6xl transition duration-500"
    :class="bg"
  >
    Fetching data
    <span v-for="dot in dots" :key="dot">.</span>
  </div>
  <div
    v-else-if="status === 'error'"
    class="h-screen flex justify-center items-center p-4 text-red-100 text-4xl bg-red-800 text-center lg:text-6xl"
  >
    Oops! An error happened. Please, try again in a few minutes
  </div>
  <div v-else>
    <div class="container mx-auto px-4">
      <p class="text-3xl font-bold py-12">Results</p>
      <p class="text-lg mb-12 text-gray-600">Down below you will see a list of every performed analysis, along with a small description and more information on what it is / how to fix it.</p>
    </div>
    <div v-for="(tests, category) in categories" :key="category">
      <Category :name="category" :tests="tests" />
    </div>
  </div>
</template>

<script>
import Category from './Category.vue'

export default {
  name: 'Results',
  components: { Category },
  props: {
    results: {
      type: Array,
      required: false
    },
    status: {
      type: String,
      required: false
    }
  },
  data () {
    return {
      bg: 'bg-gray-800',
      dots: 0
    }
  },
  computed: {
    categories () {
      if (!this.results) {
        return {}
      }

      const categories = {}
      for (const result of this.results) {
        if (!categories[result.category]) {
          categories[result.category] = []
        }

        categories[result.category].push(result)
      }

      return categories
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
