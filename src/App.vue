<template>
  <v-app id="inspire">
    <v-app-bar color="primary" app>
      <v-toolbar-title class="white--text"
        >Todo Condor - Daniel Morán</v-toolbar-title
      >
    </v-app-bar>

    <v-main>
      <v-container>
        {{ listOne }}
        <list-one :listOne="listOne" @emitTaskId="handleDoneListOne($event)" />
        <v-divider></v-divider>
        {{ listTwo }}
        <list-two :listTwo="listTwo" @emitTaskId="handleDoneListTwo($event)" />
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
      listOne: [
        {
          id: 1,
          title: "ListOne",
          done: false,
        },
        {
          id: 2,
          title: "ListTwo",
          done: false,
        },
        {
          id: 3,
          title: "ListThree",
          done: false,
        },
      ],
      listTwo: [
        {
          id: 4,
          title: "ListDone",
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
      // let resultTwo = this.listOne.find((task) => task.id === id);
      // resultTwo.done = true;
      // let resultOne = this.listOne.filter((task) => task.id !== id);
      // this.listOne = resultOne;
      // this.listTwo.push(resultTwo);
      alert(id)
    },
  },
};
</script>
