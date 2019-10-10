<template>
    <div class="searchContainer">
        <input type="text" class="search search__input" @keyup.enter ="getOne()" 
        v-model= "sailer" placeholder="Introduzca regatista">
        <button class="search search__btn" @click="getOne()">Buscar</button>
    </div>
</template>

<script>
export default {
    data() {
        return{
            sailer: ''
        }
    },
    methods: {
        getOne() {
            this.$emit('fetch', this.sailer)
        }
    }
}
</script>

<style scoped>

    .searchContainer {
        padding: 10px;
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
    }

    .search{
        min-width: 250px;
        padding: 5px 10px 5px;
        margin: 10px;
    }

    .search__input{
        font-size: 14px;
        background-color: rgb(207, 200, 200);
        border-radius: 5px;
        color: black;
        border: 0px;
    }

    .search__btn {
        font-size: 16px;
        background-color: #3b506b;
        border-radius: 5px;
        align-self: center;
        color: white;
    }

</style>