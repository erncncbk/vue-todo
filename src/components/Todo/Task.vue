<template>
  <div>
    <v-list-item
      :ripple="false"
      @click="doneTask(task.id)"
      :class="{ 'grey lighten-3': task.done }"
      class="white"
    >
      <template v-slot:default>
        <v-list-item-action>
          <v-checkbox :input-value="task.done"></v-checkbox>
        </v-list-item-action>

        <v-list-item-content>
          <v-list-item-title
            :class="{ 'text-decoration-line-through': task.done }"
          >
            {{ task.title }}
          </v-list-item-title>
        </v-list-item-content>
        <div v-if="task.dueDate">
          <v-icon small>mdi-calendar</v-icon>
          <v-list-item-action-text class="text-caption">
            {{ task.dueDate | niceDate }}
          </v-list-item-action-text>
        </div>

        <v-list-item-action v-if="!$store.state.sorting">
          <task-menu :task="task" />
        </v-list-item-action>

        <v-list-item-action v-if="$store.state.sorting">
          <v-btn color="purple" class="handle" icon>
            <v-icon>mdi-drag-horizontal-variant</v-icon>
          </v-btn>
        </v-list-item-action>
      </template>
    </v-list-item>
    <v-divider></v-divider>
  </div>
</template>

<script>
import TaskMenu from "./TaskMenu.vue";
import { format } from "date-fns";
export default {
  components: { TaskMenu },
  props: ["task"],
  filters: {
    niceDate(value) {
      return format(new Date(value), "MMM d");
    },
  },
  methods: {
    doneTask(id) {
      this.$store.dispatch("doneTask", id);
    },
  },
};
</script>

<style lang="sass">
.sortable-ghost
  opacity: 0
.sortable-drag
 box-shadow:0 0 10px rgba(0,0,0,0.3)
</style>