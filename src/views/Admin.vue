<template>
  <div class="admin">
    <Login/>
  </div>
</template>

<script>
import Login from '@/components/Login-admin.vue'

export default {
  name: 'login',
  components: {
    Login
  }
}
</script>

<style scoped>
    .admin{
        padding: 150px 10px 80px
    }
</style>