<template>
    <div>
        <h2>¿Desea cerrar sesión?</h2>
        <button @click="logout">Cerrar sesión</button>
    </div>
</template>

<script>
export default {
    name: 'logout-component',
    methods: {
        logout() {
            localStorage.removeItem('auth-regata');
            this.$router.replace('/');
        }
    }
}
</script>

<style scoped>
    div {
        padding: 20px;
    }
    h2 {
        color: rgba(245, 245, 220, 0.76);
        padding: 20px 0px 10px;
    }
    button {
        padding: 10px;
        border-radius: 4px;
        outline: none;
        font-size: 14px;
        font-weight: 600;
        border-radius: 5px;
        color: #3b506b;
    }
</style>