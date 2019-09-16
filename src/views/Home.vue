<template>
  <div class="home">
    <h1>Regatistas canarios federados</h1>
    <h2 id="error" v-if="error.status">{{error.message}}</h2>
    <div id="cards-container">
      <Card :profile="profile" v-for="(profile, i) in response.profiles" :key="i"/>
    </div>
    <Pagination @page="setPage" :limitOfSet="5" :limitOfPage="10" :total="response.total"/>
  </div>
</template>

<script>
import Card from '../components/Profile-card';
import Pagination from '../components/Pagination';

export default {
  name: 'home',
  data() {
    return {
      response: {
        profiles: [],
        total: 0,
      },
      error: {
        status: false,
        message: ''
      },
      url: {
        urlBase: 'http://localhost:3000/response',
        page: ''
      }
    }
  },
  watch: {
    url: {
      handler(){
        this.getProfiles();
      },
      deep: true
    }
  },
  methods: {
    getProfiles() {
      this.error.status = false;

      this.$axios.get(`${this.url.urlBase}${this.url.page ? `/${this.url.page}` : ''}`)
        .then(res => {
          this.response.total = res.data.total;
          this.response.profiles = res.data.array;
          if(res.data.length == 0){
            this.error.status = true;
            this.error.message = 'No hemos encontrado regatistas'
          }
        })
        .catch(() => {
          this.error.status = true;
          this.error.message = 'Sorry, something wrong happend'
        });
    },
     setPage(page) {
      this.url.page = page;
    },
  },
  created() {
    this.getProfiles();
  },
  components: {
    Card,
    Pagination
  }
}
</script>

<style scoped>
  .home {
    padding-top: 100px;
  }

  #cards-container {
    display: grid;
    grid-template-columns: 1fr;
    justify-items: center;
    grid-gap: 30px;
    width: 90%;
    margin: 40px auto 60px;
  }
  
  #error {
    font-size: 2rem;
    margin-top: calc(50vh - 144px);
    color: #f76742;
  }

  @media(min-width: 900px) {
    #cards-container {
      grid-template-columns: repeat(2, 1fr);
    }
  }
  @media(min-width: 1350px) {
    #cards-container {
      grid-template-columns: repeat(3, 1fr);
    }
  }
  @media(min-width: 2000px) {
    #cards-container {
      grid-template-columns: repeat(4, 1fr);
    }
  }
</style>