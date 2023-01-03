<template>
  <div class="divide-y divide-slate-100 pt-5 cursor-pointer">
    <NavView>
      <NavItem href="" v-on:click:active=true  isActive>New Guide</NavItem>
      <NavItem href="" v-on:click:active=true >Top Guide</NavItem>
    </NavView>
    <ListView>
  {{ guideStore.guides }}
    </ListView>
  </div>
</template>

<script setup> 
  import { } from "vue"
  import { storeToRefs } from 'pinia'
  import { useGuideStore } from '@/stores/guide'
  import NavView       from '@/components/NavView.vue'
  import NavItem       from '@/components/NavItem.vue'
  import ListView      from '@/components/ListView.vue'
  import GuideItem     from '@/menu/guide/GuideItem.vue'

  const guideStore = useGuideStore()
const { guides, loading, error }  = storeToRefs(useGuideStore())
      // const { fetchGuides }             = useGuideStore()
console.log(guideStore)
      guideStore.fetchGuides()
</script>
