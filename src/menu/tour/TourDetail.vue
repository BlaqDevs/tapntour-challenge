<template>
    <div>

    <div class=" grid grid-cols-2 gap-2 top-10 mx-auto text-lg pt-10 w-full h-full" v-for="tour in tourDetails" :key="tour">
        <div class="mx-auto w-10/12">

      <img :src="tour.image" alt="">
        </div>
      <div class="mx-auto w-10/12">
<div class="text-5xl  text-center">{{ tour.name }}</div>
<p class="text-center text-4xl text-lime-500">{{ tour.city }}</p>
<p class="mt-5">{{ tour.desc }}</p>
        <FeatureItem :item="tour"></FeatureItem>
      </div>
        
    </div>
      <div class="text-center mt-5">

       <router-link to="/tours" class=" pa-5" > &#8592; Back </router-link>
      </div>
    </div>

</template>

<script setup>
import TourItem from "@/menu/tour/TourItem.vue";
  import FeatureItem from '@/components/FeatureItem.vue'

import { onMounted, computed } from 'vue';
import { storeToRefs } from 'pinia';
import { useRoute } from 'vue-router';
import { useTourStore } from '@/stores/tour';

const {fetchTours} = useTourStore()
const {tours}= storeToRefs(useTourStore())
const route = useRoute()
const tourDetails = computed(()=>{
   return tours.value.filter((tour)=>tour.id == route.params.id)
}) 
 onMounted(()=>{
     fetchTours()
 })
</script>