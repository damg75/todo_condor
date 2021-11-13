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
            <v-list-item-title>{{ task.title }}</v-list-item-title>
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
      <v-subheader v-if="searching">There's no match with the search input</v-subheader>
      <v-subheader v-else >There's nothing To Do!</v-subheader>
    </v-list>
    <v-row class="d-flex flex-row justify-center">
      <v-col cols="6">
        <v-text-field
          label="Search Task Name"
          v-model="select"
          dense
          autocomplete="nope"
          outlined
          clearable
          append-icon="mdi-magnify"
          persistent-hint
          @input="emitSearchValue"
          @keydown.esc="emitSearchValueESC"
        >
        </v-text-field>
      </v-col>
    </v-row>
  </div>
</template>
<script>
export default {
  props: {
    listOne: {
      type: [Array],
    },
    searching: {
      type: [Boolean],
    }
  },
  data() {
    return {
      select: "",
    };
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
    emitSearchValue() {
      this.$emit("emitSearchValue", this.select);
    },
    emitSearchValueESC() {
      this.select = null;
      this.$emit("emitSearchValue", this.select);
    },
  },
};
</script>
<style></style>
