<template>
  <div>
    <transition name="fade">
      <Notification title="Copied!" text="Command has successfully been copied to your clipboard." v-if="shouldDisplayNotification" />
    </transition>
    <Banner @copy="displayNotification" />
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
    }
  }
}
</script>
