<template>

    <div>
        <span id="hide" @click="$emit('hide')">Cerrar</span>

        <h2>Editar deportista</h2>
        <span class="msg" :class="msg.error ? 'error' : ''" v-if="msg.status">{{msg.text}}</span>
        <div class="formulary">

            <div class="field">
                <label for="name">Nombre</label>
                <input class="info" type="text" v-model="copy.name" id="name" placeholder="Nombre">
            </div>
            <div class="field">
                <label for="first-surname">Primer apellido</label>
                <input class="info" type="text" v-model="copy.first_surname" id="first-surname" placeholder="Primer apellido">
            </div>
            <div class="field">
                <label for="second-surname">Segundo apellido</label>
                <input class="info" type="text" v-model="copy.second_surname" id="second-surname" placeholder="Segundo apellido">
            </div>
            <div class="field">
                    <label for="category">Categoría</label>
                    <input v-model="copy.category" type="text" id="category">
            </div>
            <div class="field">
                    <label for="club">Club</label>
                    <input v-model="copy.club" type="text" id="club">
            </div>
            <div class="field">
                    <label for="boat">Clase</label>
                    <input v-model="copy.boat" type="text" id="boat">
            </div>
            <div class="field">
                    <label for="federation">Federación</label>
                    <input v-model="copy.federation" type="text" id="federation">
            </div>
            <div class="field">
                    <label for="status">Estado</label>
                    <select id="status" @change="setSelect">
                        <option value="ACTIVO" :checked="copy.status === 'ACTIVO'">Activo</option>
                        <option value="PENDIENTE" :checked="copy.status === 'PENDIENTE'">Pendiente</option>
                    </select>
            </div>
            <div class="btn-edit">
                <button @click="editUser" class="btn send">Editar</button>
            </div>

        </div>


    </div>
</template>

<script>
export default {
    name: 'edit-profile-modal',
    props: {
        profile: Object
    },
    data() {
        return {
            copy: {...this.profile},
            msg: {
                status: false,
                error: false,
                text: ''
            }
        }
    },
    methods: {
        setSelect(){
            this.copy.status = document.querySelector('#status').value;
        },
        checkObjEqual(obj1, obj2){
            return Object.keys(obj1).reduce( (prev, current) => prev && obj1[current] == obj2[current], true );
        },
        editUser() {
            this.msg.status = false;
            this.msg.error = false;
            const update = {
                name: this.copy.name,
                first_surname: this.copy.first_surname,
                second_surname: this.copy.second_surname,
                category: this.copy.category,
                club: this.copy.club,
                boat: this.copy.boat,
                federation: this.copy.federation
            }
            if(!this.checkObjEqual(this.profile, this.copy)){
                const id = window.location.hash.split('/').slice(-1)[0];
                this.$axios.patch(`https://web-ranking-back.herokuapp.com/regatista/${id}`, update)
                    .then(() => {
                        this.msg.status = true;
                        this.msg.text = 'Perfil actualizado correctamente.'
                    })
                    .catch(() => {
                        this.msg.status = true;
                        this.msg.error = true;
                        this.msg.text = 'No se ha podido actualizar, lo sentimos.';
                    });
            }
        }
    }
}
</script>

<style scoped>

    #hide {
        position: absolute;
        top: 90px;
        left: 30px;
        cursor: pointer;
        font-weight: 500;
    }

    .formulary{
        margin: 20px auto;
        border-radius: 5px;
        background-color: #3b506b;
        color: white;
    }

    .field{
        padding: 10px 30px 10px;
        text-align: left;
        flex-basis: 50%;
    }

    label{
        padding: 5px 0 15px;
        font-size: 16px;
        display: inline-block;
    }

    input, select{
        width: 100%;
        padding: 5px;
        border: 0px;
        border-radius: 5px;
        font-size: 14px;
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
    }

    p{
        margin: 0px 0px 10px;
        color: white;
    }

    .btn-edit{
        padding: 20px 30px 20px;
        text-align: right;
    }

    .btn{
        padding: 5px;
        font-size: 16px;
        border-radius: 5px;
        align-self: center;
        margin-left: 20px;
        text-decoration: none;
    }

    .send{
        background-color: white;
        color: #3b506b;
        font-weight: bolder;
    }

    .msg {
        color: green;
        font-size: 1.1rem;
        font-weight: 500;
        margin-top: 10px;
        display: inline-block;
    }

    .error {
        color: #f76742;
    }

  @media (min-width: 780px) {
      .formulary {
            display: flex;
            flex-wrap: wrap;
            max-width: 70%;
      }

      .btn-edit {
          margin-left: auto;
      }
  }

</style>