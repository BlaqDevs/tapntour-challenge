<template>
  <div class="divide-y divide-slate-100 pt-5 cursor-pointer">
    <NavView>
      <NavItem href="" @click.prevent="layout = 'all'" :isActive="active1"
        >New Release</NavItem
      >
      <NavItem
        href=""
        v-on:click:active="true"
        :isActive="active2"
        @click.prevent="layout = 'highRated'"
        >Top Rated</NavItem
      >
      <NavItem
        href=""
        v-on:click:active="true"
        :isActive="active3"
        @click.prevent="layout = 'england'"
        >England</NavItem
      >
    </NavView>

    <ListView class="mb-5">
      <p v-if="loading">Loading tours...</p>
      <p v-if="error">{{ error.message }}</p>
      <div v-if="layout === 'all'">
        <li
          class="mx-auto list-none hover:list-disc"
          v-for="tour in tours"
          :key="tour.id"
        >
          <div class="mx-auto w-2/4">
            <TourItem :item="tour" />
          </div>
        </li>
      </div>
      <div v-if="layout === 'england'">
        <li
          class="mx-auto list-none hover:list-disc"
          v-for="tour in englandTour"
          :key="tour.id"
        >
          <div class="mx-auto w-2/4">
            <TourItem :item="tour" />
          </div>
        </li>
      </div>
      <div v-if="layout === 'highRated'">
        <li
          class="mx-auto list-none hover:list-disc"
          v-for="tour in highRated"
          :key="tour.id"
        >
          <div class="mx-auto w-2/4">
            <TourItem :item="tour" />
          </div>
        </li>
      </div>
    </ListView>
  </div>
</template>

<script setup>
// import
import { onMounted, ref, computed, watch } from "vue";
import { useRouter } from "vue-router";
import { storeToRefs } from "pinia";
import { useTourStore } from "@/stores/tour";
import ListView from "@/components/ListView.vue";
import NavView from "@/components/NavView.vue";
import TourItem from "@/menu/tour/TourItem.vue";

import NavItem from "@/components/NavItem.vue";

const englandTour = computed(() => {
  return tours.value.filter((tour) => tour.country === "England");
});
const highRated = computed(() => {
  return tours.value.filter((tour) => tour.rating > 5);
});
const layout = ref("all");
const active1 = ref(false);
const active2 = ref(false);
const active3 = ref(false);
onMounted(() => {
  active1.value = true;
});
watch(layout, (newVal) => {
  if (newVal === "all") {
    active1.value = true;
    active2.value = false;
    active3.value = false;
  } else if (newVal === "highRated") {
    active2.value = true;
    active1.value = false;
    active3.value = false;
  } else if (newVal === "england") {
    active3.value = true;
    active2.value = false;
    active1.value = false;
  }
});

const { tours, tour, loading, error } = storeToRefs(useTourStore());

const { fetchTours } = useTourStore();

onMounted(() => {
  fetchTours();
});

const router = useRouter();

const viewDetails = (tourId) => {
  router.push(`/TourDetail/${tourId}`);
};
</script>
