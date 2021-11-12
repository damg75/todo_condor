<template>
  <v-app id="inspire">
    <v-app-bar color="primary" app class="d-flex flex-column align-center">
      <v-toolbar-title class="white--text"
        >Todo Condor - Daniel Morán</v-toolbar-title
      >
    </v-app-bar>

    <v-main class="mt-10">
      <v-container>
        <v-row class="d-flex flex-column align-center">
          <v-col cols="12" md="6">
            <v-text-field
              label="Input Task Name"
              dense
              autocomplete="nope"
              v-model="input"
              outlined
              clearable
              @keyup.enter="handleInput"
              @keyup.esc="input = null"
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
        <v-row class="d-flex flex-column align-center">
          <v-col cols="12" md="6">
            <!-- {{ listOne }} -->
            <list-one
              :listOne="listOne"
              @emitTaskId="handleDoneListOne($event)"
              @emitDelete="handleDeleteOne($event)"
              @emitEdit="handleEdit($event)"
            />
          </v-col>
        </v-row>
        <v-divider></v-divider>
        <v-row class="d-flex flex-column align-center">
          <v-col cols="12" md="6">
            <!-- {{ listTwo }} -->
            <list-two
              :listTwo="listTwo"
              @emitTaskId="handleDoneListTwo($event)"
              @emitDelete="handleDelete($event)"
            />
          </v-col>
        </v-row>
      </v-container>
    </v-main>
    <!-- dialogs -->
    <template>
      <v-row justify="center">
        <v-dialog v-model="dialogDelete" persistent max-width="290">
          <v-card>
            <v-card-title class="text-h5">
              Do you want to delete the task?
            </v-card-title>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="red darken-1" text @click="dialog('second', false)">
                Disagree
              </v-btn>
              <v-btn
                color="primary darken-1"
                text
                @click="dialog('second', true)"
              >
                Agree
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-row>
    </template>
    <template>
      <v-row justify="center">
        <v-dialog v-model="dialogDeleteOne" persistent max-width="290">
          <v-card>
            <v-card-title class="text-h5">
              Do you want to delete the task?
            </v-card-title>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="red darken-1" text @click="dialog('first', false)">
                Disagree
              </v-btn>
              <v-btn
                color="primary darken-1"
                text
                @click="dialog('first', true)"
              >
                Agree
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-row>
    </template>
    <template>
      <v-row justify="center">
        <v-dialog v-model="dialogEdit" persistent max-width="380">
          <v-card>
            <v-card-title class="text-h5">
              Do you want to edit the task?
            </v-card-title>
            <v-card-text class="mt-4">
              <v-text-field
                label="Input Task Name"
                dense
                autocomplete="nope"
                v-model="currentTask"
                outlined
                @keyup.enter="currentTask && handleDialogEdit(true)"
              >
              </v-text-field
            ></v-card-text>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="red darken-1" text @click="handleDialogEdit(false)">
                Disagree
              </v-btn>
              <v-btn
                color="primary darken-1"
                text
                @click="handleDialogEdit(true)"
                :disabled="!currentTask && true"
              >
                Agree
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-row>
    </template>
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
      dialogDelete: false,
      dialogDeleteOne: false,
      currentId: 0,
      dialogEdit: false,
      currentTask: "",
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
    handleDelete(id) {
      true;
      this.currentId = id;
      this.dialogDelete = true;
    },
    handleDeleteOne(id) {
      this.currentId = id;
      this.dialogDeleteOne = true;
    },
    dialog(list, option) {
      if (list === "second") {
        if (option) {
          let resultOne = this.listTwo.filter(
            (task) => task.id !== this.currentId
          );
          this.listTwo = resultOne;
        }
        this.dialogDelete = false;
      }
      if (list === "first") {
        if (option) {
          let resultOne = this.listOne.filter(
            (task) => task.id !== this.currentId
          );
          this.listOne = resultOne;
        }
        this.dialogDeleteOne = false;
      }
    },
    handleEdit(id) {
      this.currentId = id;
      let currentTask = this.listOne.find((task) => task.id === id);
      this.currentTask = currentTask.title;
      this.dialogEdit = true;
    },
    handleDialogEdit(option) {
      if (option) {
        let objIndexEdit = this.listOne.findIndex(
          (obj) => obj.id === this.currentId
        );
        this.listOne[objIndexEdit].title = this.currentTask;
      }
      this.dialogEdit = false;
    },
  },
  computed: {
    newTaskTitleInvalid() {
      return !this.input;
    },
  },
};
</script>
