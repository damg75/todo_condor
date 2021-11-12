<template>
  <div>
    <v-list flat>
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
            <v-list-item-title>{{ task.title }} {{task.id}}</v-list-item-title>
          </v-list-item-content>
        </template>
      </v-list-item>
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
  },
};
</script>
<style></style>
