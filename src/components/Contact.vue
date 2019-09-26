<template>
  <div class="formulary">
      <div class="field">
        <label for="firstName">Nombre*</label>
        <input class="info" type="text" v-model="firstName" id="firstName" 
        placeholder="Introduzca nombre del regatista">
      </div>
      <div class="field">
        <label for="surName">Apellidos*</label>
        <input class="info" type="text" v-model="surName" id="surName"
        placeholder="Introduzca apellidos del regatista">
      </div>
      <div class="field">
        <label for="email">Correo electronico*</label>
        <input class="info" type="email" v-model="email" id="email"
        placeholder="Introduzca un e-mail">
      </div>
      <div class="field">
        <label for="issue">Asunto*</label>
        <input class="info" type="text" v-model="issue" id="issue"
        placeholder="Introduzca el motivo de su solicitud">
      </div>
      <div class="field">
        <label for="description">Descripcion</label>
        <textarea class="info" v-model="description" id="description" 
        placeholder="Exponga su solicitud"></textarea>
      </div>
      <div class="field advise">
        <p>(*) Los campos señalados son obligatorios para el envio</p>
        <p>Si desea adjuntar uno o más archivos pulse en "Verificar y enviar", 
        seleccione "Insertar" en la parte superior y elija "archivos"</p>
      </div>
      <div class="click">
        <a class="btn reset" @click="reset">Resetear</a>
        <a v-if="required == true" class="btn send" :href="mailto">Verificar y enviar</a>
        <span v-else class="btn send disabled">Verificar y enviar</span>
      </div>
  </div>
</template>

<script>
export default {

  data() {
    return{
      firstName: '',
      surName: '',
      email: '',
      issue: '',
      description: '',
      emailTo: 'ruben.altair91@gmail.com'
    }
  },

  methods: {
    reset() {
        this.firstName= this.surName=  this.email=  this.issue=  this.description= ''
    }
  },
  computed: {
    mailto() {
      return `mailto:${this.emailTo}?subject=(RANKING): ${this.issue}&body=Mensaje de ${this.firstName} ${this.surName} <${this.email}>:%0A${this.description}`
    },
    required() {
      if(this.firstName && this.surName && this.email.includes("@" && ".") && this.issue){
        return true
      }else{
        return false
      }
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

  label{
    padding: 5px 0 15px;
    font-size: 16px;
    display: inline-block;
  }

  .info{
    width: 100%;
    padding: 5px;
    border: 0px;
    border-radius: 5px;
    font-size: 14px;
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
  }

  .advise{
    font-size: 14px;
    text-align: justify;
    color: rgba(94, 94, 90, 0.616);
    padding: 0px 30px 0px;
  }

  p{
    margin: 0px 0px 10px;
    color: white;
  }

  .click{
    padding: 20px 30px 20px;
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

  .disabled{
    opacity: 0.5;
  }

</style>