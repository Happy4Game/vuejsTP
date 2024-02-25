<template>
    <div>
        <v-text-field v-model="search" clearable label="Recherche"></v-text-field>
        {{ search }}
    </div>
</template>
<script>
export default {
    name: 'movieSearch',
    data(){
        return {
            search: ''
        }
    },
    watch: {
        search(newData, oldData){
            this.$emit('setMovieSearch', newData)
        }
    },
    
}
</script>