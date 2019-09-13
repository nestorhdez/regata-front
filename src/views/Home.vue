<template>
  <div class="home">
    <h1>Regatistas canarios federados</h1>
    <h2 id="error" v-if="error.status">{{error.message}}</h2>
    <div id="cards-container">
      <Card :profile="profile" v-for="(profile, i) in profiles" :key="i"/>
    </div>
  </div>
</template>

<script>
import Card from '../components/Profile-card';

export default {
  name: 'home',
  data() {
    return {
      profiles: [],
      error: {
        status: false,
        message: ''
      }
    }
  },
  methods: {
    getProfiles() {
      this.error.status = false;

      this.$axios.get('http://localhost:3000/response')
        .then(res => {
          this.profiles = res.data;
          if(res.data.length == 0){
            this.error.status = true;
            this.error.message = 'No hemos encontrado regatistas'
          }
        })
        .catch(() => {
          this.error.status = true;
          this.error.message = 'Sorry, something wrong happend'
        });
    }
  },
  created() {
    this.getProfiles();
  },
  components: {
    Card
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
    margin: 40px auto;
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
  @media(min-width: 1500px) {
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