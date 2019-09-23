<template>
    <div id="regattas-table">
        <h2>Resultado de regatas</h2>
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

    #regattas-table h2 {
        margin-bottom: 15px;
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

</style>