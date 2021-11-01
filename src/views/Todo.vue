<template>
  <div class="home pa-2">
    

    <!-- ListTasksComponent -->
    <list-tasks v-if="$store.state.tasks.length" />

    <!-- NoTaskComponent -->
    <no-tasks v-else />
    <button-done-sorting v-if="$store.state.sorting" />
  </div>
</template>

<script>
import ButtonDoneSorting from "../components/Todo/ButtonDoneSorting.vue";
import ListTasks from "../components/Todo/ListTasks.vue";
import NoTasks from "../components/Todo/NoTasks.vue";
export default {
  components: {  ListTasks, NoTasks, ButtonDoneSorting },
  name: "Home",
};
</script>

