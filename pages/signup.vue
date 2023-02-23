<template>
  <SelectHouse v-if="!houseId" :houseId="houseId" @select="houseId = $event"/>
  <SignUp v-else :houseId="houseId" @select="houseId = $event"/>
</template>

<script>
export default {
    name: "SignupPage",
    data() {
        return {
            houseId: null,
        }
    },
}
</script>

<style>
:root {
  --color-dark: #111212;
  --color-light: #242424;
  --color-gray: #8A8A8A;
  --radius: 30px;
  --shadow-normal: 0 1px 3px 0 rgba(0, 0, 0, 0.1),
  	0 1px 2px 0 rgba(0, 0, 0, 0.06);
  --shadow-medium: 0 4px 6px -1px rgba(0, 0, 0, 0.1),
  	0 2px 4px -1px rgba(0, 0, 0, 0.06);
  --shadow-large: 0 10px 15px -3px rgba(0, 0, 0, 0.1),
  	0 4px 6px -2px rgba(0, 0, 0, 0.05);
}

*,
*::before,
*::after {
	padding: 0;
	margin: 0;
}
</style>
