<template>
  <div class="h-screen flex items-center justify-center bg-white">
    <div class="container mx-auto px-4 sm:px-6 md:grid md:grid-cols-2 md:gap-8 lg:px-8">
      <div class="relative">
        <h1 class="font-litic text-green-600 text-4xl text-left md:text-6xl" data-aos="fade-down" data-aos-duration="600">Litic</h1>
        <p class="text-gray-600 text-xl text-left mt-8" data-aos="fade-up" data-aos-duration="600">
          Analyze your website and get insights about SEO, accesibility, security and best practices in less than a minute.
        </p>
        <form class="max-w-4xl mx-auto flex gap-8 mt-4" data-aos="fade-up" data-aos-duration="1000" action="#" method="POST" @submit.prevent="onSubmit">
          <label class="block text-sm font-semibold flex-1">
            URL
            <input type="text" placeholder="Your URL here" class="block w-full p-4 rounded-lg border border-gray-300 mt-2" v-model="url" autofocus>
          </label>
          <label class="block text-sm font-semibold flex-1">
            Keyword <small class="text-xs text-gray-600 pl-1">- Optional</small>
            <input type="text" placeholder="Search keyword" class="block w-full p-4 rounded-lg border border-gray-300 mt-2" v-model="keyword">
          </label>
          <div class="flex items-end">
            <button type="submit" class="w-full inline-flex justify-center items-center px-8 py-4 border border-transparent text-sm font-medium rounded-md shadow-sm text-white bg-green-600 hover:bg-green-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-green-500">
              Analyze
            </button>
          </div>
        </form>
        <div class="mt-16" data-aos="fade-up" data-aos-delay="300" data-aos-duration="1000">
          <p class="text-lg text-gray-600 text-center">You can also install it and use it locally</p>
          <pre class="max-w-md mx-auto mt-8 bg-gray-900 p-4 rounded-lg text-gray-100 text-center select-none cursor-pointer" @click="copyCommand">$ npm install litic -g</pre>
          <div class="text-center mt-8">
            <a href="https://github.com/RuliLG/Litic" target="_blank" rel="noopener noreferrer" class="inline-flex items-center px-6 py-3 rounded-lg border border-gray-300 text-gray-800 hover:bg-gray-100">
              View on GitHub
              <svg role="img" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 inline-block ml-2 flex-shrink-0"><path d="M12 .297c-6.63 0-12 5.373-12 12 0 5.303 3.438 9.8 8.205 11.385.6.113.82-.258.82-.577 0-.285-.01-1.04-.015-2.04-3.338.724-4.042-1.61-4.042-1.61C4.422 18.07 3.633 17.7 3.633 17.7c-1.087-.744.084-.729.084-.729 1.205.084 1.838 1.236 1.838 1.236 1.07 1.835 2.809 1.305 3.495.998.108-.776.417-1.305.76-1.605-2.665-.3-5.466-1.332-5.466-5.93 0-1.31.465-2.38 1.235-3.22-.135-.303-.54-1.523.105-3.176 0 0 1.005-.322 3.3 1.23.96-.267 1.98-.399 3-.405 1.02.006 2.04.138 3 .405 2.28-1.552 3.285-1.23 3.285-1.23.645 1.653.24 2.873.12 3.176.765.84 1.23 1.91 1.23 3.22 0 4.61-2.805 5.625-5.475 5.92.42.36.81 1.096.81 2.22 0 1.606-.015 2.896-.015 3.286 0 .315.21.69.825.57C20.565 22.092 24 17.592 24 12.297c0-6.627-5.373-12-12-12"/></svg>
            </a>
          </div>
        </div>
      </div>
      <div data-aos="fade-left" data-aos-duration="600" data-aos-delay="300">
        <img src="@/assets/app_development.svg" alt="Illustration of a laptop with some HTML code on it" class="block w-full max-w-lg mx-auto">
      </div>
    </div>
  </div>
</template>

<script>
import copy from 'copy-to-clipboard'

export default {
  name: 'Banner',
  data () {
    return {
      url: '',
      keyword: ''
    }
  },
  methods: {
    copyCommand () {
      copy('npm install litic -g')
      this.$emit('copy')
    },
    onSubmit () {
      this.$emit('analysis', this.url, this.keyword)
    }
  }
}
</script>
