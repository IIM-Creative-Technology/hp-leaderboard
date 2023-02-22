<template>
  <!-- <Tutorial /> -->
  <!-- <SignUp/> -->
  <SelectHouse v-if="!houseId" :houseId="houseId" @select="houseId = $event"/>
  <SignUp v-else :houseId="houseId" @select="houseId = $event"/>
</template>

<script>
import SelectHouse from '../components/SelectHouse.vue';

export default {
    name: "IndexPage",
    data() {
        return {
            houseId: null,
        }
    },
}
</script>
