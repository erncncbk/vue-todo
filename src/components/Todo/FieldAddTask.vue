<template>
  <v-text-field
    flat
    v-model="newTaskTitle"
    @click:append="addTask"
    @keyup.enter="addTask"
    class="field-add-task pa-2"
    outlined
    placeholder="Add Task"
    hide-details
    clearable
    color="white"
  >
    <template v-slot:append>
      <v-icon @click="addTask" color="white" :disabled="newTaskTitleInvalid"
        >mdi-plus</v-icon
      >
    </template>
  </v-text-field>
</template>

<script>
export default {
  data() {
    return {
      newTaskTitle: "",
      tasks: [],
    };
  },
  computed: {
    newTaskTitleInvalid() {
      return !this.newTaskTitle;
    },
  },
  methods: {
    addTask() {
      if (!this.newTaskTitleInvalid) {
        this.$store.dispatch("addTask", this.newTaskTitle);
        this.newTaskTitle = "";
      }
    },
  },
};
</script>
<style lang="sass">
.field-add-task.v-input--is-focused
  .v-input__slot
    background: rgba(108,36,162,0.3) !important
.field-add-task.v-text-field--outlined
  border-radius: 15px !important
</style>
