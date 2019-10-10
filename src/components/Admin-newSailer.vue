<template>
    <div class="newSailer">
        <h2>Agregar regatista</h2>
        <form>
            <div class="container side">
                <div class="field">
                    <label for="number">Numero de federación</label>
                    <input type="text" v-model="newSailer.affiliate_number" id="number" 
                    placeholder="Nº de afiliado">
                </div>
                <div class="field">
                    <label for="federation">Federación*</label>
                    <input type="text" v-model="newSailer.federation" id="federation" 
                    placeholder="federación a la que pertenece" required>
                </div>
                <div class="field">
                    <label for="club">Club*</label>
                    <input type="text" v-model="newSailer.club" id="club" 
                    placeholder="club al que pertenece" required>
                </div>
                <div class="field">
                    <label for="name">Nombre*</label>
                    <input type="text" v-model="newSailer.name" id="name" 
                    placeholder="nombre completo" required>
                </div>
                <div class="field">
                    <label for="firstSurname">Primer apellido*</label>
                    <input type="text" v-model="newSailer.first_surname" id="firstSurname" 
                    placeholder="Primer apellido" required>
                </div>
                <div class="field">
                    <label for="secondSurname">Segundo apellido*</label>
                    <input type="text" v-model="newSailer.second_surname" id="secondSurname" 
                    placeholder="Segundo apellido" required>
                </div>   
                <div class="field">
                    <label for="nif">NIF</label>
                    <input type="text" v-model="newSailer.NIF" id="nif" 
                    placeholder="Documento de identidad">
                </div>   
                <div class="field">
                    <label for="address">Dirección</label>
                    <input type="text" v-model="newSailer.address" id="address" 
                    placeholder="Dirección actual">
                </div>  
                <div class="field">
                    <label for="zipCode">Codigo postal</label>
                    <input type="text" v-model="newSailer.zip_code" id="zipCode" 
                    placeholder="Nº de codigo postal">
                </div>                
                <div class="field">
                    <label for="town">Ciudad</label>
                    <input type="text" v-model="newSailer.town" id="town" 
                    placeholder="Ciudad donde reside">
                </div> 
                <div class="field">
                    <label for="island">Isla</label>
                    <input type="text" v-model="newSailer.island" id="island" 
                    placeholder="Isla donde reside">
                </div>     
                <div class="field">
                    <label for="phoneNumber">Numero de telefono</label>
                    <input type="text" v-model="newSailer.phone_number" id="phoneNumber" 
                    placeholder="Numero de telefono">
                </div> 
            </div>
            <div class="container side">
                <div class="field">
                    <label for="phoneNumber2">Nº de telefono 2º</label>
                    <input type="text" v-model="newSailer.phone_number2" id="phoneNumber2" 
                    placeholder="numero de telefono auxiliar">
                </div>  
                <div class="field">
                    <label for="email">Correo electronico</label>
                    <input type="text" v-model="newSailer.email" id="email" 
                    placeholder="dirección de correo electronico">
                </div>
                <div class="field">
                    <label for="birthday">Fecha de nacimiento</label>
                    <input type="text" v-model="newSailer.birthday" id="birthday" 
                    placeholder="Fecha de nacimiento">
                </div>          
                <div class="field">
                    <label for="inscriptionDate">Fecha de inscripción</label>
                    <input type="text" v-model="newSailer.license_inscription_date" id="inscriptionDate" 
                    placeholder="Fecha de inscripción como regatista">
                </div>  
                <div class="field">
                    <label for="gender">Genero</label>
                    <input type="text" v-model="newSailer.gender" id="gender" 
                    placeholder="Genero">
                </div>
                <div class="field">
                    <label for="speciality">Especialidad</label>
                    <input type="text" v-model="newSailer.specialty" id="speciality" 
                    placeholder="Especialidad">
                </div>
                <div class="field">
                    <label for="boat">Barco*</label>
                    <input type="text" v-model="newSailer.boat" id="boat" 
                    placeholder="Tipo de embarcación">
                </div>
                <div class="field">
                    <label for="category">Categoria*</label>
                    <input type="text" v-model="newSailer.category" id="category" 
                    placeholder="Categoria" required>
                </div>
                <div class="field">
                    <label for="expirationDate">Fecha de expiración</label>
                    <input type="text" v-model="newSailer.expiration_date" id="expirationDate" 
                    placeholder="Expiración de la licencia">
                </div>
                <div class="field">
                    <label for="price">Precio</label>
                    <input type="number" v-model="newSailer.price" id="price" 
                    placeholder="Precio">
                </div>
                <div class="field">
                    <label for="status">Estatus*</label>
                    <input type="text" v-model="newSailer.status" id="status" 
                    placeholder="Activo o pendiente" required>
                </div>
                <div class="field bottom">
                    <p :class="this.feedback.error ? 'feedback error' : 'feedback'" 
                    v-if="feedback.message">{{feedback.message}}</p>
                    <p v-else>(*) Los campos señalados son obligatorios</p>
                    <button class="btn" @click="addOne">Añadir</button>
                </div>
            </div>
        </form>
    </div>
</template>

<script>
export default {
    data() {
        return {
            newSailer: {
                affiliate_number: '',
                federation: '',
                club: '',
                name: '',
                first_surname: '',
                second_surname: '',
                NIF: '',
                address: '',
                zip_code: '',
                town: '',
                Island: '',
                phone_number: '',
                phone_number2: '',
                email: '',
                birthday: '',
                license_inscription_date: '',
                gender: '',
                specialty: '',
                boat: '',
                category: '',
                expiration_date: '',
                price: '',
                status: ''
            },
            feedback: {
                error: false,
                message: ''
            }
        }
    },
    methods: {
        addOne() {
            this.feedback.error = false;

            if(this.newSailer.second_surname && this.newSailer.federation && this.newSailer.club && 
            this.newSailer.name && this.newSailer.first_surname && this.newSailer.category && 
            this.newSailer.status && this.newSailer.boat){
                
                this.$axios.post('https://web-ranking-back.herokuapp.com/regatistas', this.newSailer)
                    .then(() => this.feedback.message= 'Regatista añadido con éxito')
                    .catch(() => {
                        this.feedback.error = true;
                        this.feedback.message = 'No se ha podido añadir con éxito. Lo sentimos';
                    });
            }
        }
    }
}
</script>

<style scoped>

    form{
        display: flex;
        flex-wrap: wrap;
    }

    h2{
        color: rgba(245, 245, 220, 0.76);
        padding: 20px 0px 10px;
    }

    .side{
        width: 100%
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

    .bottom{
        width: 100%;
        text-align: right;
    }

    p{
        padding: 5px 0 5px;
        color: rgba(255, 255, 255, 0.692);
    }

    .feedback{
        color: #75f742;
        font-weight: 500;
        width: 100%;
        text-align: right;
    }

    .error{
        color: #f76742;
    }

    .btn{
        width: 150px;
        margin: 15px 0px 15px;
        padding: 5px;
        font-size: 14px;
        font-weight: 600;
        border-radius: 5px;
        align-self: flex-end;
        color: #3b506b;
    }

    @media(min-width: 600px) {
        .side{
            width: 50%;
        }
    }

</style>