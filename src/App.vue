<template>
  <div>
    <transition name="fade">
      <Notification title="Copied!" text="Command has successfully been copied to your clipboard." v-if="shouldDisplayNotification" />
    </transition>
    <Banner @copy="displayNotification" @analysis="analyse" />
    <Results :results="results" :loading="loading" ref="results" />
  </div>
</template>

<script>
import Banner from './components/Banner.vue'
import Notification from './components/Notification.vue'
import Results from './components/Results.vue'

export default {
  name: 'app',
  components: {
    Banner,
    Notification,
    Results
  },
  data () {
    return {
      shouldDisplayNotification: false,
      loading: false,
      results: null
    }
  },
  methods: {
    displayNotification () {
      this.shouldDisplayNotification = true
      setTimeout(() => {
        this.shouldDisplayNotification = false
      }, 2000)
    },
    analyse (url, keyword) {
      if (this.loading) {
        return
      }

      this.results = null
      this.loading = true
      setTimeout(() => {
        this.$refs.results.$el.scrollIntoView({ behavior: 'smooth' })
      }, 200)

      fetch('https://litic.herokuapp.com/invoke', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
          'Accept': 'application/json'
        },
        body: JSON.stringify({
          url,
          keyword: keyword.length > 0 ? keyword : undefined
        })
      })
        .then(response => response.json())
        .then(json => {
          this.results = json.results
        })
        .catch(error => {
          // console.log(error)
        })
    }
  }
}
</script>
