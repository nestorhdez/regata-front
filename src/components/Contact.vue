<template>
  <div class="formulary">
    
      <div class="field">
        <h2>Nombre</h2>
        <input class="info" type="text" v-model="firstName" placeholder="Introduzca nombre del regatista">
      </div>

      <div class="field">
        <h2>Apellidos</h2>
        <input class="info" type="text" v-model="lastName" placeholder="Introduzca apellidos del regatista">
      </div>

      <div class="field">
        <h2>Correo electronico</h2>
        <input class="info" type="text" v-model="email" placeholder="Introduzca un e-mail">
      </div>

      <div class="field">
        <h2>Asunto</h2>
        <input class="info" type="text" v-model="issue" placeholder="Introduzca el motivo de su esolicitud">
      </div>

      <div class="field">
        <h2>Descripcion</h2>
        <textarea class="info" v-model="description" placeholder="Exponga su solicitud"></textarea>
      </div>

      <div class="click">
        <button class="btn attach" :click="attach">Adjuntar</button>
        <button class="btn send" :click="send">Enviar</button>
      </div>
  </div>
</template>

<style scoped>
.formulary{
  max-width: 500px;
  margin: auto;
  border-radius: 5px;
  background-color: white;
}
.field{
  padding: 10px 30px 10px;
  text-align: left;
}
h2 {
  margin: 5px 0 15px;
  font-size: 16px;
}
.info{
   width: 100%;
    padding: 5px;
    font-size: 14px;
    border: 0px;
    background-color: rgb(176, 230, 230);
    border-radius: 5px;
    color: rgb(0, 0, 0);
}
.click{
  padding: 20px 30px 20px;
  text-align: right;
}
.btn{
  width: 120px;
  padding: 5px;
  font-size: 16px;
  border-radius: 5px;
  align-self: center;
  color: rgb(255, 255, 255);
  margin-left: 20px
}
.attach{
  background-color: rgb(206, 27, 27)
}
.send{
  background-color: #3b506b
}

</style>