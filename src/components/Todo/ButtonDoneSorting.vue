<template>
  <v-btn
    class="button-done-sorting text-white"
    color="purple"

    @click="$store.commit('toogleSorting')"
  >
    Done Sorting
  </v-btn>
</template>

<script>
export default {};
</script>

<style lang="sass">
.button-done-sorting
    position: fixed
    bottom: 20px
    left: 50%
    transform: translateX(-50%)
</style>

