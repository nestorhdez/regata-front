<template>
  <div class="home">
    <div id="loading" v-if="loading">
      <span>Cargando...</span>
    </div>
    <div v-else>
      <Search @fetch="searchSailer"/>
      <h1 v-if="!error.status">Regatistas canarios federados</h1>
      <h2 id="error" v-if="error.status">{{error.message}}</h2>
      <div id="cards-container">
        <Card :profile="profile" v-for="(profile, i) in result.profiles" :key="i"/>
      </div>
    </div>
    <Pagination @page="setPage" :limitOfSet="5" :limitOfPage="10" :total="result.total" v-if="!error.status"/>
  </div>
  
</template>

<script>

import Card from '../components/Profile-card';
import Pagination from '../components/Pagination';
import Search from '../components/Search';
import eventBus from '../main';

export default {
  name: 'home',
  data() {
    return {
      loading: false,
      result: {
        profiles: [],
        total: 0,
      },
      error: {
        status: false,
        message: ''
      },
      url: {
        urlBase: 'http://38232cf0.ngrok.io/regatista',
        page: 0,
        search: ''
      }
    }
  },
  computed: {
    urlToUse() {
      if(this.url.search){
        return `${this.url.urlBase}?name=${this.url.search}${this.url.page ? `&offset=${this.url.page}` : ''}`
      }else{
        return `${this.url.urlBase}s${this.url.page ? `?offset=${this.url.page}` : ''}`
      }
    }
  },
  methods: {
    getProfiles() {
      this.loading = true;
      this.error.status = false;
      this.$axios.get(this.urlToUse)
        .then(response => {
          this.loading = false;
          this.result.total = response.data.total;
          this.result.profiles = response.data.res;
          if(response.data.res.length == 0){
            this.error.status = true;
            this.error.message = 'No hemos encontrado regatistas';
          }
        })
        .catch(() => {
          this.loading = false;
          this.result.profiles = [];
          this.error.status = true;
          this.error.message = 'Lo sentimos, ha ocurrido un error';
        });
    },
    setPage(page) {
      this.url.page = page;
      this.getProfiles();
    },
    searchSailer(fetch) {
      this.url.search = fetch;
      this.url.page = 0;
      this.getProfiles();
    },

  },
  created() {
    this.getProfiles();
    //When the logo of the navbar is clicked trigger the refresh event
    this.$emit('url', this.urlToUse);
    eventBus.$on('refresh', () => {
      this.result.total = 0;
      this.url.page = 0;
      this.getProfiles();
    });
  },
  components: {
    Card,
    Pagination,
    Search
  }
}

</script>

<style scoped>

  .home {
    padding-top: 70px;
  }

  #cards-container {
    display: grid;
    grid-template-columns: 1fr;
    justify-items: center;
    grid-gap: 30px;
    width: 90%;
    margin: 40px auto 90px;
  }

  #error {
    font-size: 2rem;
    margin-top: calc(50vh - 144px);
    color: #f76742;
  }

  #loading {
      width: 100vw;
    }

  #loading span {
    margin: calc(50vh - 52px) auto;
    font-size: 1.5rem;
    font-weight: 500;
    display: block;
  }

  @media(min-width: 900px) {
    #cards-container {
      grid-template-columns: repeat(2, 1fr);
    }
  }

  @media(min-width: 1700px) {
    #cards-container {
      grid-template-columns: repeat(4, 1fr);
    }
  }

</style>