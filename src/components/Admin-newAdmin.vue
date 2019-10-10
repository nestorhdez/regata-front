<template>
    <div class="newAdmin">
        <h2>Agregar administrador</h2>
        <div class="field">
            <label for="name">Nombre</label>
            <input type="text" v-model="name" id="name" 
            placeholder="Nombre de usuario">
        </div>
        <div class="field">
            <label for="email">Correo electronico</label>
            <input type="text" v-model="email" id="email" 
            placeholder="Nombre de usuario">
        </div>
        <div class="field">
            <label for="password">Contraseña</label>
            <input type="password" v-model="password" id="password" 
            placeholder="introduzca la contraseña del usuario">
        </div>
        <div class="field advise">
            <p>Debe completar todos los campos. Cuando confirme su solicitud se le abrira 
            un correo para poder notificar al nuevo administrador de su nombre de usuario 
            y claves de acceso</p>
        </div>
        <div class="click">
            <span :class="this.feedback.error ? 'feedback error' : 'feedback'" 
            v-if="feedback.message">{{feedback.message}}</span>
            <a v-if="required" class="btn" :href="mailto" @click="addAdmin">
            Confirmar y enviar</a>
            <span v-else class="btn disabled">Confirmar y enviar</span>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            name: '',
            email: '',
            password: '',
            message: {
                issue: 'Ha sido dado de alta como administrador en web de regatistas canarios',
                address: 'www.webderegatistas.com',
                boddy1: 'Bienvenido, se le ha otorgado una cuenta como administrador de la web',
                boddy2: '.Sus datos son los siguientes:%0A%0Anombre de usuario:'
            },
            feedback: {
                error: false,
                message: ''
            },
            url: 'http://38232cf0.ngrok.io/auth/signup'
        }
    },
    methods: {
        addAdmin(){
            this.$axios.post(this.url, {name: this.name, email: this.email, password: this.password})
            .then(() => {
                this.feedback.error= false
                this.feedback.message= 'Nuevo administrador creado con éxito'
            })
            .catch(() => {
                this.feedback.error = true
                this.feedback.message= 'Lo sentimos, ha ocurrido un error en el servidor'
            });
        }
    },
    computed: {
        mailto() {
            return `mailto:${this.email}?subject=${this.message.issue}&body=${this.message.boddy1} ${this.message.address}${this.message.boddy2} ${this.name}%0Acontraseña: ${this.password}`
        },
        required() {
            if(this.name && this.email.includes("@" && ".") && this.password){
                return true
            }else{
                return false
            }
        }
    }
}
</script>

<style scoped>

    h2{
        color: rgba(245, 245, 220, 0.76);
        padding: 20px 0px 10px;
    }

    .field{
        padding: 10px 30px 10px;
        text-align: left;
    }

    label{
        padding: 5px 0 5px;
        font-size: 16px;
        display: inline-block;
        color: white
    }

    input{
        width: 100%;
        padding: 5px;
        margin: 15px 0px 15px;
        border: 0px;
        border-radius: 5px;
        font-size: 14px;
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
    }

    .click{
        display: flex;
        flex-direction: column;
        padding: 20px 30px 20px;
        text-align: right;
    }

    p{
        color: rgba(255, 255, 255, 0.692);
        text-align: justify
    }

    .feedback{
        color: #75f742;
        font-weight: 500;
        width: 100%;
        text-align: justify;
        margin-bottom: 10px
    }

    .error{
        color: #f76742;
    }

    .btn{
        width: 150px;
        margin: 10px 0px 10px;
        padding: 5px 10px 5px;
        font-size: 14px;
        border-radius: 5px;
        align-self: flex-end;
        color: #3b506b;
        background-color: rgb(221, 221, 221);
        font-weight: bolder;
        text-decoration: none;
    }

    .disabled{
        opacity: 0.5;
    }

    @media(min-width: 600px) {
        .feedback{
            text-align: right;
        }
    }
   
</style>