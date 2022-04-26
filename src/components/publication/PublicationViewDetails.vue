<script setup>
import { publicationService } from '../../services/publicationService';
import PublicationView from './PublicationView.vue';


    const props = defineProps({
        publicationId: String
    })

    const {data, error, isFinished} = publicationService.useGetById(props.publicationId)

</script>

<template>

    <div v-if="error">Tapahtui virhe</div>
    <div v-else-if="!isFinished"></div>
    <div v-else-if="!data">
    
        <PublicationView :publication="data.publication"></PublicationView>
    </div>
</template>