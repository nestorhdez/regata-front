<template>
    <div class="profile-card">
      <img class="profile-image" src="../assets/profile.svg" alt="profile image">
      <div class="profile-info">
      <h2>{{`${profile.name} ${profile.surName}`}}</h2>
        <span>Fecha de nacimiento: {{profile.birthdate}}</span>
        <span>Ha participado en: {{profile.noRegattas}} regatas</span>
        <span>Pertenece al club: {{profile.club}}</span>
      </div>
    </div>
</template>

<script>
export default {
    name: "profile-card",
    props: {
        profile: {
            _id: String,
            imagen: String,
            name: String,
            surName: String,
            birthdate: String,
            noRegattas: Number,
            club: String
        }
    }
}
</script>

<style scoped>
    .profile-card {
        display: flex;
        align-items: center;
        justify-content: space-between;
        flex-wrap: wrap;
        padding: 20px;
        background-color: #3b506b;
        color: white;
        width: 100%;
        height: 200px;
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