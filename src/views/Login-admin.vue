<template>
    <div class="login">
        <div class="form">
            <h2>Acceso de administrador</h2>
            <span class="denied" v-if="denied">
                El nombre y/o la contraseña no son validos</span>
            <div class="form-content">
                <label for="Name">Nombre</label>
                <input type="text" v-model="nameUser" id="Name" 
                placeholder="Introduzca su nombre de usuario" required>
            </div>
            <div class="form-content">
                <label for="Password">Contraseña</label>
                <input type="password" v-model="passwordUser" id="Password"
                placeholder="Introduzca su contraseña" required>
            </div>
            <button @click="access">Iniciar sesión</button>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return{
            nameUser: '',
            passwordUser: '',
            denied: false,
            jwt: localStorage.getItem('auth-regata')
        }
    },
    methods: {
        access() {
            this.denied = false;
            this.$axios.post('http://c316658e.ngrok.io/auth/login', {name: this.nameUser, password: this.passwordUser})
                .then(res => {
                    localStorage.setItem('auth-regata', JSON.stringify(res.data));
                    this.$router.replace('/admin');
                })
                .catch( () => this.denied = true)
        }
    },
    created(){
        if(this.jwt) {
            this.$router.replace('/admin');
        }
    }
}
</script>

<style scoped>

    .login {
        padding: 150px 10px 80px
    }

    .form{
        max-width: 500px;
        margin: auto;
        border-radius: 5px;
        background-color: #3b506b;
        color: white;
        padding: 20px
    }

    .form-content{
        padding: 10px;
        text-align: left;
    }

    h2{
        margin: 10px
    }

    .denied{
        color: rgba(255, 0, 0, 0.787);
        font-weight: 700
    }

    label{
        padding: 15px 0 15px;
        font-size: 16px;
        display: inline-block;
    }

    input{
        width: 100%;
        padding: 5px;
        border: 0px;
        border-radius: 5px;
        font-size: 14px;
    }

    button{
        width: 150px;
        margin: 20px 0px 10px;
        padding: 5px;
        font-size: 16px;
        font-weight: 600;
        border-radius: 5px;
        align-self: center;
        color: #3b506b;
    }

</style>