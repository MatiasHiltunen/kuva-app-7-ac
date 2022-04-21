<script setup>
import { computed, reactive } from 'vue'


const publicationData = reactive({
    title: '',
    description: '',
    url: '',
    visibility: 2, // Julkinen postaus
    tags: []
})


const isDataValid = computed(() => {

    const urlValidation = publicationData.url.includes('https://')
    const descriptionValidation = publicationData.description.length < 1000
    const titleValidation = publicationData.title.length > 2

    return {
        urlValidation: urlValidation ? 'OK' : 'Vain https osoitteet ovat sallittu',
        descriptionValidation: descriptionValidation ? 'OK' : 'Kuvauksen teksti on liian pitkä',
        titleValidation: titleValidation ? 'OK' : 'Otsikon täytyy olla ainakin kolme merkkiä pitkä',
        isAllValid: urlValidation && descriptionValidation && titleValidation
    }
})


const createNewPublication = () => {

    if (!isDataValid.value.isAllValid) return

    publicationData.title = ''
    publicationData.description = ''
    publicationData.url = ''

}


</script>

<template>

    <div>
        <label>Otsikko</label>
        <small>{{ isDataValid.titleValidation }}</small>
        <input v-model="publicationData.title" type="text">

        <small>{{ isDataValid.descriptionValidation }}</small>
        <label>Kuvaus</label>
        <input v-model="publicationData.description" type="text">

        <small>{{ isDataValid.urlValidation }}</small>
        <label>URL</label>
        <input v-model="publicationData.url" type="text">

        <button :disabled="!isDataValid.isAllValid" @click="createNewPublication">Lähetä</button>
    </div>



</template>