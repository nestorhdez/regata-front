<template>
    <div v-if="profile" id="profile-view">
        <div id="loading" v-if="loading">
            <span>Cargando...</span>
        </div>
        <EditProfile @hide="edited" :profile="profile" v-else-if="!loading && editProfile"/>
        <EditRegattas @hide="edited" :profile="profile" v-else-if="!loading && editRegattas"/>
        <div v-else id="profile-container">
            <img id="profile-image" src="../assets/profile.svg" alt="profile image">
            <div id="profile-info">
                <h1 id="profile-name" v-if="profile.name">{{`${profile.name} ${profile.first_surname} ${profile.second_surname}`}}</h1>
                <p>Categoría: <span v-if="profile.category">{{profile.category}}</span></p>
                <p>Club: <span v-if="profile.club">{{profile.club}}</span></p>
                <p>Clase: <span v-if="profile.boat">{{profile.boat}}</span></p>
                <p>Federación: <span v-if="profile.federation">{{profile.federation}}</span></p>
                <p>Estado: <span v-if="profile.status">{{profile.status}}</span></p>
            </div>
            <div id="edit-btn-container">
                <button @click="editProfile = true" v-if="jwt" class="edit-btn">Editar deportista</button>
                <button @click="editRegattas = true" v-if="jwt" class="edit-btn">Editar regatas</button>
            </div>
            <RegattasTable :list="profile.list_of_regattas" v-if="profile.list_of_regattas && profile.list_of_regattas.length > 0" id="regattas-table" />
            <div id="not-regattas-container" v-else>
                <h2 class="loading" id="not-regattas">No consta su participación en ninguna regata</h2>
                <router-link v-if="!jwt" to="/contact">Realizar una petición</router-link>
            </div>
        </div>
    </div>
</template>

<script>

import EditProfile from '../components/EditProfile';
import EditRegattas from '../components/EditRegattas';
import RegattasTable from '../components/Regattas-table';

export default {
    name: 'profile',
    data() {
        return {
            profile: {},
            id: '',
            url: 'https://web-ranking-back.herokuapp.com/regatistas',
            loading: true,
            jwt: localStorage.getItem('auth-regata'),
            editProfile: false,
            editRegattas: false
        }
    },
    computed: {
        urlToUse() {
            return `${this.url}/${this.id}`;
        }
    },
    methods: {
        edited(){
            this.editProfile = false;
            this.editRegattas = false;
            this.getProfile();
        },
        getProfile() {
            this.loading = true;
            this.$axios.get(this.urlToUse)
                .then(res => {
                    this.profile = res.data[0];
                    this.loading = false;
                })
                .catch(() => {
                    this.$router.replace('/');
                });
        }
    },
    created(){
        this.id = window.location.hash.split('/').slice(-1)[0];
        this.getProfile();
    },
    components: {
        EditProfile,
        EditRegattas,
        RegattasTable
    }
}
</script>

<style scoped>

    *{
        box-sizing: border-box;
        text-decoration: none;
    }

    #profile-container {
        display: flex;
        flex-direction: column;
        align-items: center;
        flex-wrap: wrap;
    }

    #profile-view {
        padding: 130px 20px 50px;
    }

    #profile-name {
        margin-bottom: 10px;
    }

    #profile-info {
        text-align: left;
    }

    p {
        font-weight: bold;
        margin-bottom: 7px;
    }

    p span {
        font-weight: normal;
    }

    #profile-image{
        width: 100px;
        height: 100px;
        margin-bottom: 30px;
    }

    #not-regattas {
        margin: 60px auto 30px;
        font-size: 1.5rem;
        color: #f76742;
    }

    #not-regattas-container {
        width: 100%;
    }

    #not-regattas-container a{
        text-decoration: none;
        color: white;
        background-color: #2b3e50;
        padding: 10px;
        border-radius: 4px;
        font-weight: 500;
    }

    #loading {
        width: 100vw;
    }

    #loading span {
        margin: calc(50vh - 120px) auto;
        font-size: 1.5rem;
        font-weight: 500;
        display: block;
    }

    #edit-btn-container {
        margin-top: 20px;
        margin-right: auto;
    }

    .edit-btn {
        padding: 5px 10px;
        border-radius: 4px;
        outline: none;
        color: #3b506b;
        background-color: white;
        font-weight: bold;
        font-size: 0.8rem;
        border-width: 1.4px;
    }

    .edit-btn:nth-child(2){
        margin-left: 10px;
    }

    @media(min-width: 700px) {

        #profile-view {
            padding: 120px 40px 50px;
        }

        #profile-container {
            flex-direction: row;
        }

        #profile-image {
            flex-basis: 40%;
            margin-bottom: 0;
        }

        #profile-info {
            flex-basis: 60%;
        }

        #edit-btn-container {
            margin-right: 0;
            margin-left: auto;
        }

        .regattas-container span:nth-child(2) {
            font-size: 1rem;
        }

        #not-regattas {
            margin: 60px auto 30px;
        }
    }
</style>