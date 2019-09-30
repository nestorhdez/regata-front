<template>
  <div class="admin">
    <AdminPage v-if="access"/>
    <Login v-else @approve='accessApprove'/>
  </div>
</template>

<script>
import Login from '@/components/Login-admin.vue'
import AdminPage from '@/components/Page-admin.vue'

export default {
  name: 'admin',
  data(){
    return{
      access: false
    }
  },
  methods: {
    accessApprove() {
      return this.access = true
    }
  },
  components: {
    Login,
    AdminPage
  }
}
</script>

<style scoped>
    .admin{
        padding: 150px 10px 80px
    }
</style>