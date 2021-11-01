<template>
  <v-list flat class="pt-0">
    <draggable  v-model="tasks"  handle=".handle">
        <task
          v-for="task in $store.getters.tasksFiltered"
          :key="task.id"
          :task="task"
        />
    </draggable>
  </v-list>
</template>

<script>
import Task from "./Task.vue";
import draggable from "vuedraggable";
export default {
  components: { Task, draggable },
  computed:{
    tasks:{
      get(){
        return this.$store.getters.taskFiltered
      },
      set(value){
        this.$store.dispatch('setTasks',value)
      }
    }
  }
};
</script>
