<template>
  <div>
    <v-list flat v-if="listOne.length > 0">
      <v-subheader>To-do List</v-subheader>

      <v-list-item v-for="task in listOne" :key="task.id">
        <template v-slot:default>
          <v-list-item-action>
            <v-checkbox
              :input-value="task.done"
              color="primary"
              @click="handleDone(task.id)"
            ></v-checkbox>
          </v-list-item-action>

          <v-list-item-content>
            <v-list-item-title
              >{{ task.title }} {{ task.id }}</v-list-item-title
            >
          </v-list-item-content>
          <v-btn icon color="primary" @click="handleEdit(task.id)">
            <v-icon>mdi-pencil</v-icon>
          </v-btn>
          <v-btn icon color="primary" @click="handleDelete(task.id)">
            <v-icon>mdi-delete</v-icon>
          </v-btn>
        </template>
      </v-list-item>
    </v-list>
    <v-list flat v-else>
      <v-subheader>There's nothing To Do!</v-subheader>
    </v-list>
  </div>
</template>
<script>
export default {
  props: {
    listOne: {
      type: [Array],
    },
  },
  data() {
    return {};
  },
  methods: {
    handleDone(id) {
      this.$emit("emitTaskId", id);
    },
    handleDelete(id) {
      this.$emit("emitDelete", id);
    },
    handleEdit(id) {
      this.$emit("emitEdit", id);
    },
  },
};
</script>
<style></style>
