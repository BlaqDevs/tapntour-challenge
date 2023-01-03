<template>
  <div class="divide-y divide-slate-100 pt-5 cursor-pointer">
    <NavView>
      <NavItem href="" v-on:click:active="true" isActive>New Release</NavItem>
      <NavItem href="" v-on:click:active="true">Top Rated</NavItem>
      <NavItem href="" v-on:click:active="true">England</NavItem>
    </NavView>
    <ListView>
      <p v-if="loading">Loading tours...</p>
      <p v-if="error">{{ error.message }}</p>
      <pre>

      {{ tours }}
      </pre>
      <li v-for="tour in tours" :key="tour.id">
        <span @click="viewDetails(tour.id)">
          {{ tour.name }}
        </span>
        <button @click="viewDetails(tour.id)" class="btn">
          View Tour Details
        </button>
      </li>
      
    </ListView>
  </div>
</template>

<script setup>
// import
import { useRouter } from "vue-router";
import { storeToRefs } from "pinia";
import { useTourStore } from "@/stores/tour";
import TourItem from "@/menu/tour/TourItem.vue";
import ListView from "@/components/ListView.vue";
import NavView from "@/components/NavView.vue";
import NavItem from "@/components/NavItem.vue";
 

const { tours, loading, error } = storeToRefs(useTourStore());
const { fetchTours } = useTourStore();
fetchTours();

const router = useRouter()

const viewDetails = (tourId) =>{
router.push(`/TourDetail/${tourId}`)
}
</script>
