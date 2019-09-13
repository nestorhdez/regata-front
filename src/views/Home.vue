<template>
  <div class="home">
    <h1>Regatistas canarios federados</h1>
    <div class="profile">
      <img class="profile-image" src="../assets/profile.svg" alt="profile image">
      <div class="profile-info">
      <h2>Pedro Ramirez</h2>
        <span>21 años</span>
        <span>Ha participado en: 15 regatas</span>
        <span>La media de sus posiciones es: 8º</span>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'home',
  components: {
  }
}
</script>

<style scoped>
  .home {
    padding-top: 100px;
  }

  .profile {
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-wrap: wrap;
    padding: 20px;
    background-color: #3b506b;
    color: white;
    width: 500px;
    height: 200px;
    margin: 30px;
    border-radius: 4px;
    box-shadow: 2px 1px 8px 1px rgba(0, 0, 0, 0.58);
  }

  .profile-image {
    width: 50px;
    height: 50px;
    flex-basis: 20%;
  }

  .profile-info {
    flex-basis: 70%;
    text-align: left;
  }

  span {
    display: block;
  }
</style>