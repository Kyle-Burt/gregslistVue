<template>
    <div class="container-fluid">
        <div class="row">
            <div class="col-12 mb-2">
                <h1>Houses Page!</h1>
                <button v-if="account.id" >Create House Listing</button>
            </div>
        </div>
        <div class="row">
            <div v-for="house in houses" :key="house.id" class="col-md-10 m-auto mb-2">
                <HouseCard :houseProp="house" />
            </div>
        </div>
    </div>
</template>


<script>
import HouseCard from '../components/HouseCard.vue';
import { computed, onMounted } from 'vue';
import { housesService } from '../services/HousesService.js';
import Pop from '../utils/Pop.js';
import { AppState } from '../AppState.js';

export default {
    setup() {
        async function getHouses() {
            try {
                await housesService.getHouses();
            }
            catch (error) {
                Pop.error(error.message);
            }
        }
        onMounted(() => {
            getHouses();
        });
        return {
            houses: computed(() => AppState.houses),
            account: computed(() => AppState.account)
        };
    },
    components: { HouseCard }
}
</script>


<style lang="scss" scoped>

</style>