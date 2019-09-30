<template>
  <div class="admin">
    <h1>Welcome!</h1>
  </div>
</template>

<script>

export default {
  name: 'admin',
  data(){
    return {
      jwt: localStorage.getItem('auth-regata'),
      access: false
    }
  },
  methods: {
    accessApprove() {
      return this.access = true
    }
  },
  components: {
  },
  created(){
    if(!this.jwt){
      this.$router.replace('/login');
    }
  }
}
</script>

<style scoped>
    .admin{
        padding: 150px 10px 80px
    }
</style>