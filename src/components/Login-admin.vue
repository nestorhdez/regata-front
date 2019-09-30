<template>
    <div class="login">
        <form>
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
            <button type="submit" @click="access">Iniciar sesión</button>
        </form>
    </div>
</template>

<script>
export default {
    data() {
        return{
            nameUser: '',
            passwordUser: '',
            validation: {
                name: 'paco',
                password: '1234'
            },
            denied: false,
        }
    },
    methods: {
        access() {
            this.nameUser == this.validation.name && this.passwordUser == this.validation.password ? this.$emit('approve') : this.denied=true
        }
    }
}
</script>

<style scoped>

    .login{
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