<template>

    <div>
        <span id="hide" @click="$emit('hide')">Cerrar</span>

        <h2>Editar regatas de {{`${profile.name} ${profile.first_surname} ${profile.second_surname}`}}</h2>
        <span class="msg" :class="msg.error ? 'error' : ''" v-if="msg.status">{{msg.text}}</span>

        <div id="btn-container">
            <button @click="addRegata" class="btn">Añadir regata</button>
            <button @click="save" class="btn save">Guardar</button>
        </div>

        <div class="formulary" v-for="(regatta, i) in regattas" :key="i">

            <div class="field">
                <div class="basis-15">
                    <label :for="`category-${i}`">Categoría</label>
                    <input class="info" type="text" v-model="regatta.category" :id="`category-${i}`" placeholder="Categoría" required>
                </div>
                <div class="basis-70">
                    <label :for="`regata-${i}`">Regata</label>
                    <input class="info" type="text" v-model="regatta.regatta_title" :id="`regata-${i}`" placeholder="Regata" required>
                </div>
                <div class="basis-10">
                    <label :for="`position-${i}`">Posición</label>
                    <input class="info" type="number" v-model="regatta.position" :id="`position-${i}`" placeholder="Posición" required>
                </div>
                <div class="basis-15">
                    <label :for="`vela-${i}`">vela</label>
                    <input class="info" type="text" v-model="regatta.vela" :id="`vela-${i}`" placeholder="vela" required>
                </div>
                <div class="basis-70">
                    <label :for="`club-${i}`">Club</label>
                    <input class="info" type="text" v-model="regatta.club" :id="`club-${i}`" placeholder="Club" required>
                </div>
                <div class="basis-15">
                    <label :for="`net_points-${i}`">Puntos netos</label>
                    <input class="info" type="number" v-model="regatta.net_points" :id="`net_points-${i}`" placeholder="Puntos netos" required>
                </div>
                <div class="basis-15">
                    <label :for="`total_points-${i}`">Puntos totales</label>
                    <input class="info" type="number" v-model="regatta.total_points" :id="`total_points-${i}`" placeholder="Puntos totales" required>
                </div>
                <button :id="i" @click="remove" class="btn remove">Eliminar</button>
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
            regattas: this.profile.list_of_regattas.reverse().map(user => ( {...user} ) ),
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
        addRegata(){
            this.regattas.unshift( {
                category: "",
                club: "",
                net_points: "",
                position: "",
                regatta_title: "",
                total_points: "",
                vela: ""
            });
        },
        remove(e){
            let index = e.target.id;
            this.regattas.splice(index, 1);
        },
        checkObjEqual(obj1, obj2){
            return Object.keys(obj1).reduce( (prev, current) => prev && obj1[current] == obj2[current], true );
        },
        checkArrsEqual(arr1, arr2){
            return arr1.reduce( (prev, current, i) =>  prev && this.checkObjEqual(current, arr2[i]), true );
        },
        save() {
            this.msg.status = false;
            this.msg.error = false;
            let regattasReverse = this.regattas.reverse();


            if( this.profile.list_of_regattas.length !== regattasReverse.length || !this.checkArrsEqual( this.profile.list_of_regattas, regattasReverse ) ){
                this.patchProfile();
            }
        },
        patchProfile(){
            
            const update = {
                list_of_regattas: this.regattas.reverse()
            }

            const id = window.location.hash.split('/').slice(-1)[0];
            this.$axios.patch(`https://web-ranking-back.herokuapp.com/regatista/${id}`, update)
                .then(() => {
                    this.msg.status = true;
                    this.msg.text = 'Regatas actualizadas correctamente.'
                })
                .catch(() => {
                    this.msg.status = true;
                    this.msg.error = true;
                    this.msg.text = 'No se ha podido actualizar, lo sentimos.';
                });
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
        padding: 25px;
        border-radius: 5px;
        background-color: #3b506b;
        color: white;
    }

    .field{
        text-align: left;
        flex-basis: 100%;
        display: flex;
        flex-wrap: wrap;
    }

    .field div{
        margin-right: 10px;
    }

    .basis-10{
        flex-basis: 10%;
    }

    .basis-70{
        flex-basis: 70%;
    }

    .basis-15{
        flex-basis: 15%;
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

    #btn-container{
        display: flex;
        margin: 30px 0px 40px;
    }

    #btn-container .btn:first-child{
        margin-left: auto;
    }

    .btn-edit{
        margin-top: 30px;
        text-align: right;
    }

    .btn{
        padding: 5px;
        font-size: 16px;
        border-radius: 5px;
        align-self: center;
        margin-left: 20px;
        text-decoration: none;
        background-color: white;
        color: #3b506b;
        font-weight: bolder;
        outline: none;
    }

    .save{
        background-color: #377d37;
        color: white;
    }

    .remove {
        align-self: flex-end;
        margin-left: auto;
        background-color: #bf310c;
        color: white;
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