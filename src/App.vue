<template>
  <v-app id="inspire">
    <v-app-bar color="primary" app>
      <v-toolbar-title class="white--text"
        >Todo Condor - Daniel Morán</v-toolbar-title
      >
    </v-app-bar>

    <v-main>
      <v-container>
        <v-row>
          <v-col cols="12" md="6">
            <v-text-field
              label="Input Task Name"
              dense
              autocomplete="nope"
              v-model="input"
              outlined
              clearable
              @keyup.enter="handleInput"
            >
              <template v-slot:append>
                <v-icon
                  color="primary"
                  @click="handleInput"
                  :disabled="newTaskTitleInvalid"
                >
                  mdi-plus
                </v-icon>
              </template>
            </v-text-field>
          </v-col>
        </v-row>
        <v-divider></v-divider>
        <v-row>
          <v-col cols="12" md="6">
            <!-- {{ listOne }} -->
            <list-one
              :listOne="listOne"
              @emitTaskId="handleDoneListOne($event)"
            />
          </v-col>
        </v-row>
        <v-divider></v-divider>
        <v-row>
          <v-col cols="12" md="6">
            <!-- {{ listTwo }} -->
            <list-two
              :listTwo="listTwo"
              @emitTaskId="handleDoneListTwo($event)"
              @emitDelete="handleDeleteListTwo($event)"
            />
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import ListOne from "@/views/ListOne.vue";
import ListTwo from "@/views/ListTwo.vue";

export default {
  components: { ListOne, ListTwo },
  data() {
    return {
      counter: 4,
      input: "",
      listOne: [
        {
          id: 1,
          title: "Dormir",
          done: false,
        },
        {
          id: 2,
          title: "Comer",
          done: false,
        },
        {
          id: 3,
          title: "Caminar",
          done: false,
        },
      ],
      listTwo: [
        {
          id: 4,
          title: "Sentarse",
          done: true,
        },
      ],
    };
  },
  methods: {
    handleDoneListOne(id) {
      let resultTwo = this.listOne.find((task) => task.id === id);
      resultTwo.done = true;
      let resultOne = this.listOne.filter((task) => task.id !== id);
      this.listOne = resultOne;
      this.listTwo.push(resultTwo);
    },
    handleDoneListTwo(id) {
      let resultTwo = this.listTwo.find((task) => task.id === id);
      resultTwo.done = false;
      let resultOne = this.listTwo.filter((task) => task.id !== id);
      this.listTwo = resultOne;
      this.listOne.push(resultTwo);
    },
    handleInput() {
      let newEntry = {
        id: this.counter + 1,
        title: this.input,
        done: false,
      };
      this.listOne.push(newEntry);
      this.input = "";
    },
    handleDeleteListTwo(id) {
      alert(id);
    },
  },
  computed: {
    newTaskTitleInvalid() {
      return !this.input;
    },
  },
};
</script>
