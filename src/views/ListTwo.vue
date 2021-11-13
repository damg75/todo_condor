<template>
  <div>
    <v-list flat v-if="listTwo.length > 0">
      <v-subheader>Completed <v-icon class="ml-2">mdi-check-all</v-icon> </v-subheader>

      <v-list-item v-for="task in listTwo" :key="task.id">
        <template v-slot:default>
          <v-list-item-action>
            <v-checkbox
              :input-value="task.done"
              color="primary"
              @click="handleNotDone(task.id)"
            ></v-checkbox>
          </v-list-item-action>

          <v-list-item-content >
            <v-list-item-title
              ><span class="hover" @click="handleNotDone(task.id)"
                >{{ task.title }}
              </span></v-list-item-title
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
    listTwo: {
      type: [Array],
    },
    searching: {
      type: [Boolean],
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
<style>
.hover:hover{
  cursor: pointer !important;
}
</style>
