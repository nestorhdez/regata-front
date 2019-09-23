<template>
  <div class="contact">
    <Contact/>
  </div>
</template>

<script>
import Contact from '@/components/Contact.vue'

export default {
  name: 'contact',
  components: {
    Contact
  }
}
</script>

<style scoped>
  .contact {
    padding: 120px 20px 60px; 
  }
</style>
