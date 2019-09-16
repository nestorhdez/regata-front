<template>
    
</template>

<script>
export default {
    name: 'profile-view',
    data() {
        return {
            profile: ''
        }
    },
    methods: {
        getProfile() {
            this.$axios.get()
        }
    }
}
</script>