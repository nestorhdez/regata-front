<template>
  <div class="formulary">
    
      <div class="field">
        <label>Nombre</label>
        <input class="info" type="text" v-model="firstName" placeholder="Introduzca nombre del regatista">
      </div>

      <div class="field">
        <label>Apellidos</label>
        <input class="info" type="text" v-model="lastName" placeholder="Introduzca apellidos del regatista">
      </div>

      <div class="field">
        <label>Correo electronico</label>
        <input class="info" type="text" v-model="email" placeholder="Introduzca un e-mail">
      </div>

      <div class="field">
        <label>Asunto</label>
        <input class="info" type="text" v-model="issue" placeholder="Introduzca el motivo de su esolicitud">
      </div>

      <div class="field">
        <label>Descripcion</label>
        <textarea class="info" v-model="description" placeholder="Exponga su solicitud"></textarea>
      </div>

      <div class="field advise">
         <p>Si desea adjuntar uno o más archivos pulse en "Verificar y enviar", 
          seleccione "Insertar" en la parte superior y elija "archivos"</p>
      </div>
      
      <div class="click">
        <a class="btn reset" @click="reset">Resetear</a>
        <a class="btn send" :href="mailto">Verificar y enviar</a>
      </div>
  </div>
</template>

<script>
export default {
  data() {
    return{
      firstName: '',
      lastName: '',
      email: '',
      issue: '',
      description: ''
    }
  },
  methods: {
    reset() {
        this.firstName= this.lastName= this.email= this.issue=  this.description= ''
    }
  },
  computed: {
    mailto() {
      return `mailto:ruben.altair91@gmail.com?subject=(Incidencia): ${this.issue}&body=Mensaje de ${this.firstName} ${this.lastName} <${this.email}>:%0A${this.description}`
    }
  }
}
</script>

<style scoped>
.formulary{
  max-width: 500px;
  margin: auto;
  border-radius: 5px;
  background-color: #3b506b;
  color: white;
}
.field{
  padding: 10px 30px 10px;
  text-align: left;
}
label {
  padding: 5px 0 15px;
  font-size: 16px;
  display: inline-block;
}
.advise{
  font-size: 14px;
  text-align: justify;
  color: rgba(94, 94, 90, 0.616);
  padding: 0px 30px 0px;
}
p{
  margin: 0px;
  color: white;
}
.info{
    width: 100%;
    padding: 5px;
    font-size: 14px;
    border: 0px;
    /* background-color: rgb(176, 230, 230); */
    border-radius: 5px;
}
.click{
  padding: 25px 30px 20px;
  text-align: right;
}
.btn{
  width: 180px;
  padding: 5px;
  font-size: 16px;
  border-radius: 5px;
  align-self: center;
  margin-left: 20px;
  text-decoration: none;
}
.reset{
  width: 100px;
  cursor: pointer;
}
.send{
  background-color: white;
  color: #3b506b;
  font-weight: bolder;
}
</style>