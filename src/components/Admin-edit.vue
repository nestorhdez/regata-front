<template>
    <div class="edit">
        <h2>Editar perfil</h2>
        <form class="field">
            <label for="name">Cambiar nombre: {{admin.name}}</label>
            <input class="new" type="text" v-model="newName" id="name" 
            placeholder="Nuevo nombre" required>
            <button class="btn" @click="changeName">Modificar</button>
        </form>
        <form class="field">
            <label for="email">Cambiar email: {{admin.email}}</label>
            <input class="new" type="email" v-model="newEmail" id="email" 
            placeholder="Nuevo email" required>
            <button class="btn" @click="changeEmail">Modificar</button>
        </form>
        <form class="field">
            <label for="password">Cambiar contraseña</label>
            <span class="error" v-if="error.field == 'password'">{{error.message}}</span>
            <input class="new" type="password" v-model="newPassword" id="password" 
            placeholder="Nueva contraseña" required>
            <input class="new" type="password" v-model="verifiedPassword"
            placeholder="repita la nueva contraseña" required>
            <button class="btn" @click="changePassword">Modificar</button>
        </form>
    </div>
</template>

<script>
export default {
    data() {
        return{
            admin: {
                name: 'Tipo de Incognito',
                email: 'prueba@gmail.com',
                password: '12345'
            },
            newName: '',
            newPassword: '',
            newEmail: '',
            verifiedPassword: '',
            error: {
                field: '',
                message: ''
            }
        }
    },
    methods: {
        changeName() {
            if(this.newName){
                this.admin.name = this.newName
                console.log(this.admin.name)
            }
        },
        changeEmail() {
            if(this.newEmail.includes("@" && ".")){
                this.admin.email = this.newEmail
                console.log(this.admin.email)
            }
        },
        changePassword() {
            if(this.newPassword && this.newPassword === this.verifiedPassword){
                this.error.field = ''
                this.admin.password = this.newPassword
                console.log(this.admin.password)
            }else{
                this.error.field = 'password'
                this.error.message = 'La contraseña no coincide'
            }
        }
    },
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
        border-top: solid;
        display: flex;
        justify-content: space-between;
        flex-wrap: wrap;
    }

    label{
        width: 100%;
        padding: 5px 0 5px;
        font-size: 16px;
        display: inline-block;
        color: white
    }

    .new{
        width: 100%;
        padding: 5px;
        margin: 15px 0px 15px;
        border: 0px;
        border-radius: 5px;
        font-size: 14px;
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
    }

    p{
        margin: 0px 0px 10px;
        color: white;
    }

    .btn{
        width: 150px;
        margin: 10px auto 10px;
        padding: 5px;
        font-size: 14px;
        font-weight: 600;
        border-radius: 5px;
        color: #3b506b;
    }

    .error{
        color: #f76742;
        font-weight: 700;
        width: 100%;
    }

    @media(min-width: 600px) {
        .new{
            width: 400px;
        }

        .btn{
            margin: 15px 0px 15px;
        }
    }

    @media(min-width: 800px) {
        .new{
            width: 500px;
        }
    }

</style>