<template>
  <div>
    <v-menu bottom left>
      <template v-slot:activator="{ on, attrs }">
        <v-btn color="purple" icon v-bind="attrs" v-on="on">
          <v-icon>mdi-dots-vertical</v-icon>
        </v-btn>
      </template>

      <v-list>
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
          @click="handleClick(i)"
        >
          <v-list-item-icon>
            <v-icon v-text="item.icon"></v-icon>
          </v-list-item-icon>
          <v-list-item-title>{{ item.title }}</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-menu>
    <dialog-edit
      v-if="dialogs.edit"
      :task="task"
      @close="dialogs.edit = false"
    />
    <dialog-due-date
      v-if="dialogs.dueDate"
      :task="task"
      @close="dialogs.dueDate = false"
    />
    <dialog-delete
      v-if="dialogs.delete"
      :task="task"
      @close="dialogs.delete = false"
    />
  </div>
</template>

<script>
import DialogDelete from "./Dialogs/DialogDelete.vue";
import DialogDueDate from "./Dialogs/DialogDueDate.vue";
import DialogEdit from "./Dialogs/DialogEdit.vue";

export default {
  props: ["task"],
  data: () => ({
    dialogs: {
      edit: false,
      dueDate: false,
      delete: false,
      sorting: false,
    },
    items: [
      {
        title: "Edit",
        icon: "mdi-pencil",
        click() {
          this.dialogs.edit = true;
        },
      },
      {
        title: "Due Date",
        icon: "mdi-calendar",
        click() {
          this.dialogs.dueDate = true;
        },
      },
      {
        title: "Delete",
        icon: "mdi-delete",
        click() {
          this.dialogs.delete = true;
        },
      },
      {
        title: "Sort",
        icon: "mdi-drag-horizontal-variant",
        click() {
          if (!this.$store.state.search) {
            this.$store.commit("toogleSorting");
          } else {
            this.$store.commit(
              "showSnackbar",
              "Clear search bar before sorting!"
            );
          }
        },
      },
    ],
  }),
  methods: {
    handleClick(i) {
      this.items[i].click.call(this);
    },
  },
  components: { DialogDelete, DialogEdit, DialogDueDate },
};
</script>

<style>
</style>