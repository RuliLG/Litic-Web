<template>
  <div>
    <transition name="fade">
      <Notification title="Copied!" text="Command has successfully been copied to your clipboard." v-if="shouldDisplayNotification" />
    </transition>
    <Banner @copy="displayNotification" @analysis="analyse" />
  </div>
</template>

<script>
import Banner from './components/Banner.vue'
import Notification from './components/Notification.vue'

export default {
  name: 'app',
  components: {
    Banner,
    Notification
  },
  data () {
    return {
      shouldDisplayNotification: false
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
          console.log(json)
        })
        .catch(error => {
          console.log(error)
        })
    }
  }
}
</script>
