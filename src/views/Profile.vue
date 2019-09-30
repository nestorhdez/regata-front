<template>
    <div v-if="profile" id="profile-view">
        <div id="loading" v-if="loading">
            <span>Cargando...</span>
        </div>
        <div v-else id="profile-container">
            <img id="profile-image" src="../assets/profile.svg" alt="profile image">
            <div id="profile-info">
                <h1 id="profile-name" v-if="profile.name">{{`${profile.name} ${profile.first_surname} ${profile.second_surname}`}}</h1>
                <p>Categoría: <span v-if="profile.category">{{profile.category}}</span></p>
                <p>Club: <span v-if="profile.club">{{profile.club}}</span></p>
                <p>Embarcación: <span v-if="profile.boat">{{profile.boat}}</span></p>
                <p>Federación: <span v-if="profile.federation">{{profile.federation}}</span></p>
                <p>Estado: <span v-if="profile.status">{{profile.status}}</span></p>
            </div>
            <RegattasTable :list="profile.list_of_regattas" v-if="profile.list_of_regattas && profile.list_of_regattas.length > 0" id="regattas-table" />
            <div id="not-regattas-container" v-else>
                <h2 class="loading" id="not-regattas">No consta su participación en ninguna regata</h2>
                <router-link to="/contact">Realizar una petición</router-link>
            </div>
        </div>
    </div>
</template>

<script>

import RegattasTable from '../components/Regattas-table';

export default {
    name: 'profile',
    data() {
        return {
            profile: {},
            id: '',
            url: 'http://c316658e.ngrok.io/regatistas',
            loading: true
        }
    },
    computed: {
        urlToUse() {
            return `${this.url}/${this.id}`;
        }
    },
    methods: {
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
        RegattasTable
    }
}
</script>

<style scoped>

    *{
        box-sizing: border-box;
        text-decoration: none;
    }

    #profile-view {
        padding: 100px 20px 50px;
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


    @media(min-width: 700px) {

        #profile-view {
            padding: 120px 40px 50px;
        }

        #profile-container {
            display: flex;
            align-items: center;
            flex-wrap: wrap;
        }

        #profile-image {
            flex-basis: 50%;
            margin-bottom: 0;
        }

        #profile-info {
            flex-basis: 50%;
        }

        .regattas-container span:nth-child(2) {
            font-size: 1rem;
        }

        #not-regattas {
            margin: 100px auto 30px;
        }
    }
</style>