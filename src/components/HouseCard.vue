<template>
    <div class="bg-white border border-dark rounded d-flex">
        <img class="img-fluid house-img rounded-start" :src="houseProp.imgUrl" alt="House">
        <div class="p-2">
            <h2>{{ houseProp.year }} {{ houseProp.bedrooms }} {{ houseProp.bathrooms }}</h2>
            <p>{{ houseProp.description }}</p>
            <h3>{{ houseProp.creator.name }} on {{ houseProp.createdAt.toLocaleDateString() }}</h3>
            <div class="p-3">
                <button v-if="account.id == houseProp.creatorId" class="btn btn-danger me-4" title="Delete this house" type="button">Remove Listing</button>

                <button v-if="account.id == houseProp.creatorId" class="btn btn-info" title="Edit house" type="button">Edit Listing</button>
            </div>
        </div>
    </div>
</template>


<script>
import { computed } from 'vue';
import { House } from '../models/House.js';
import { AppState } from '../AppState.js';

export default {
    props: {
        houseProp: {type: House, required: true}
    },
    setup(){

        return {
            account: computed(() => AppState.account)
        }

    }
}
</script>


<style lang="scss" scoped>

.house-img{
    width: 40%;
    object-fit: cover;
    object-position: center;
}


</style>