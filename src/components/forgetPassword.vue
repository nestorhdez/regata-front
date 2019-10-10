<template>
    <div class="newKey">
        <p class="comment" v-if="!feedback.message">
        Si desea cambiar su contraseña introduzca su correo electronico, 
        recibirá un email para que confirme su petición y recibir la nueva contraseña</p>
        <span :class="this.feedback.error ? 'feedback error' : 'feedback'" 
        v-if="feedback.message">{{feedback.message}}</span>
        <input type="email" v-model="email" id="email" 
        placeholder="Introduzca su email">
        <button @click="newPassword">Solicitar</button>
    </div>
</template>

<script>
export default {
    name: 'logout-component',
    data() {
        return {
            email: '',
            url: 'http://38232cf0.ngrok.io/auth/forgot_password',
            feedback: {
                error: false,
                message: ''
            }
        }
    },
        
    methods: {
        newPassword(){
            this.$axios.post(this.url, {email: this.email})
            .then(response => {
                this.feedback.error= false
                this.feedback.message= response.data.message
            })
            .catch(() => {
                this.feedback.error = true
                this.feedback.message= 'Lo sentimos, ha ocurrido un error en la conexion'
            });
        }
    },
}
</script>

<style scoped>
    .newKey {
        padding-top: 20px;
        display: flex;
        flex-direction: column; 
        align-items: center
    }

    p{
        font-size: 14px;
        color: rgba(255, 255, 255, 0.842);
        text-align: justify;
        margin-bottom: 10px
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

    button {
        width: 150px;
        margin: 20px 0px 10px;
        padding: 5px;
        font-size: 16px;
        font-weight: 600;
        border-radius: 5px;
        align-self: center;
        color: #3b506b;
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

</style>