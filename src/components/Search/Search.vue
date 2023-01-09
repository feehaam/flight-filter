<template>
    <Results :flightData="flightData" />
</template>

<script>
import JsonFileData from '../../assets/data.json'
import Results from '../Display/Results.vue'

export default {
    name: 'Search',
    data(){
        return {
            flightData: JsonFileData.flightOffer,
        }
    },
    components: {
        Results,
    }
}
</script>
