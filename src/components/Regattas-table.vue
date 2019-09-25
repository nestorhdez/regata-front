<template>
    <div id="regattas-table">
        <div id="title-container">
            <h2>Resultado de regatas</h2>
            <router-link to="/contact">Realizar una petición</router-link>
        </div>
        <div class="regatta-cells grid-cells">
            <span>Posición</span>
            <span>Regata</span>
            <span>Categoría</span>
        </div>
        <div class="grid-cells regattas-container" v-for="(regatta, i) in list" :key="i">
            <span>{{regatta.position}}</span>
            <span>{{regatta.regatta_title}}</span>
            <span>{{regatta.category}}</span>
        </div>
    </div>
</template>

<script>
export default {
    name: 'regattas-table',
    props:{
        list: Array
    }
}
</script>

<style scoped>

    #regattas-table {
        width: 100%;
        margin-top: 50px;
    }

    #title-container {
        display: flex;
        justify-content: space-between;
        align-items: center;
        flex-wrap: wrap;
        margin-bottom: 20px;
    }

    #title-container h2 {
        margin-bottom: 10px;
    }

    a{
        text-decoration: none;
        color: #2b3e50;
        text-decoration: underline;
        padding: 5px 0;
        border-radius: 4px;
        font-weight: 500;
    }

    .grid-cells {
        display: grid;
        grid-template-columns: 1fr 4fr 1fr;
        align-items: center;
    }

    .regatta-cells span {
        background-color: #3b506b;
        color: white;
        padding: 5px;
    }

    .regatta-cells span:not(:nth-child(1)) {
        border-left: 1px solid white;
    }

    .regattas-container {
        border-bottom: 1px solid #3b506b;
        border-left: 1px solid #3b506b;
        border-right: 1px solid #3b506b;
    }

    .regattas-container span {
        padding: 5px 10px;
    }

    .regattas-container span:nth-child(2) {
        font-size: .9rem;
    }

    @media (min-width: 458px) {
        #title-container h2 {
            margin-bottom: 0;
            margin-right: 30px;
        }
    }

</style>