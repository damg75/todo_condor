<template>
  <div>
    <v-list flat v-if="listTwo.length > 0">
      <v-subheader>Completed</v-subheader>

      <v-list-item v-for="task in listTwo" :key="task.id">
        <template v-slot:default>
          <v-list-item-action>
            <v-checkbox
              :input-value="task.done"
              color="primary"
              @click="handleNotDone(task.id)"
            ></v-checkbox>
          </v-list-item-action>

          <v-list-item-content>
            <v-list-item-title
              >{{ task.title }} {{ task.id }}</v-list-item-title
            >
          </v-list-item-content>
          <v-btn icon color="primary" disabled>
            <v-icon>mdi-pencil</v-icon>
          </v-btn>
          <v-btn icon color="primary" @click="handleDelete(task.id)">
            <v-icon>mdi-delete</v-icon>
          </v-btn>
        </template>
      </v-list-item>
    </v-list>
    <v-list flat v-else>
      <v-subheader>There are no Completed Tasks!</v-subheader>
    </v-list>
  </div>
</template>
<script>
export default {
  props: {
    listTwo: {
      type: [Array],
    },
  },
  data() {
    return {};
  },
  methods: {
    handleNotDone(id) {
      this.$emit("emitTaskId", id);
    },
    handleDelete(id) {
      this.$emit("emitDelete", id);
    },
  },
};
</script>
<style></style>
