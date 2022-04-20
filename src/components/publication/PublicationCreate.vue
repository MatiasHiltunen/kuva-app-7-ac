<script setup>
import { computed, reactive } from 'vue'


const publicationData = reactive({
    title: '',
    description: '',
    url: '',
    visibility: 2, // Julkinen postaus
    tags: []
})


const isDataValid = computed(()=>{
    return !!(publicationData.title && publicationData.description && publicationData.url)
})


const createNewPublication = ()=>{

    publicationData.title = ''
    publicationData.description = ''
    publicationData.url = ''

}


</script>

<template>

    <div>
        <label>Otsikko</label>
        <input v-model="publicationData.title" type="text">

        <label>Kuvaus</label>
        <input v-model="publicationData.description" type="text">

        <label>URL</label>
        <input v-model="publicationData.url" type="text">

        <button :disabled="!isDataValid" @click="createNewPublication">Lähetä</button>

    </div>

  

</template>