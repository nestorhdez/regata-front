<template>

    <router-link :to="`/profile/${profile._id}`" class="profile-card">
      <img class="profile-image" src="../assets/profile.svg" alt="profile image">
      <div class="profile-info">
        <h2>{{`${profile.name} ${profile.first_surname} ${profile.second_surname}`}}</h2>
        <span v-if="profile.club">Pertenece al club: {{profile.club}}</span>
        <span v-if="profile.category">Categoría: {{profile.category}}</span>
        <span v-if="profile.boat">Bote: {{profile.boat}}</span>
      </div>
    </router-link>

</template>

<script>

export default {
    name: "profile-card",
    props: {
        profile: {
            _id: String,
            name: String,
            first_surname: String,
            second_surname: String,
            club: String,
            affiliate_number: Number,
            federation: String,
            specialty: String,
            boat: String,
            category: String,
            status: String
        }
    }
}

</script>

<style scoped>

    a {
        text-decoration: none;
    }

    .profile-card {
        display: flex;
        align-items: center;
        justify-content: space-between;
        flex-wrap: wrap;
        padding: 20px;
        background-color: #3b506b;
        color: white;
        width: 100%;
        height: 280px;
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
        margin-top: 3px;
    }

    @media (min-width: 450px) {
        .profile-card {
            height: 230px;
        }
    }
    
</style>