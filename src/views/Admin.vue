<template>
  <div class="admin">
    <div class="selector">
      <!-- <button :class="[this.choice == 'edit' ? 'btn btn-active' : 'btn']" 
      @click="choice = 'edit'">Editar cuenta</button> -->
      <button :class="[this.choice == 'newAdmin' ? 'btn btn-active' : 'btn']" 
      @click="choice = 'newAdmin'">Agregar administrador</button>
      <button :class="[this.choice == 'newSailer' ? 'btn btn-active' : 'btn']" 
      @click="choice = 'newSailer'">Agregar regatista</button>
      <!-- <button :class="[this.choice == 'newSailer' ? 'btn btn-active' : 'btn']" 
      @click="choice = 'newSailer'">Contraseña olvidada</button> -->
      <button :class="[this.choice == 'logout' ? 'btn btn-active' : 'btn']" 
      @click="choice = 'logout'">Cerrar sesión</button>
    </div>
    <div class="collection">
      <!-- <Edit class="component" v-if="choice == 'edit'"/> -->
      <NewAdmin class="component" v-if="choice == 'newAdmin'"/>
      <NewSailer class="component" v-if="choice == 'newSailer'"/>
      <Logout class="component" v-if="choice == 'logout'"/>

    </div>
  </div>
</template>

<script>
// import Edit from '@/components/Admin-edit.vue'
import NewAdmin from '@/components/Admin-newAdmin.vue'
import NewSailer from '@/components/Admin-newSailer.vue'
import Logout from '@/components/Logout.vue'

export default {
  name: 'admin',
  data(){
    return{
      choice: 'newAdmin',
      jwt: localStorage.getItem('auth-regata')
    }
  },
  created() {
    if(!this.jwt){
      this.$router.replace('/login');
    }
  },
  components: {
    // Edit,
    NewAdmin,
    NewSailer,
    Logout
  }
}
</script>

<style scoped>

  .admin {
    padding: 85px 10px 10px;
  }

  .selector{
    max-width: 740px;
    margin: auto;
    padding: 10px 0px 0px;
    display: flex;
    justify-content: space-around;
  }

  .collection{
    max-width: 750px;
    margin: auto;
    border-radius: 5px;
    border: 0px;
    background-color: #3b506b;
  }

  .btn{
    width: 200px;
    margin: 10px 5px 0px;
    padding: 5px;
    border-bottom: 0px;
    font-size: 16px;
    border-top-left-radius: 5px;
    border-top-right-radius: 5px;
    color: #3b506b; 
    outline: none;
  }

  .btn:active{
    opacity: 0.5;
  }

  .btn-active{
    background-color: #3b506b;
    color: beige;
  }

   @media (max-width: 500px) {
    .btn{
      font-size: 14px;
    }
    .collection{
      border-radius: 0px;
    }
    .admin {
      padding: 85px 0px 10px;
    }
  }

</style>