<template>
  <v-footer >
    <v-row dense>
      <v-col class="text-center" cols="12" color="primary">
        {{ currentYear }} — <strong>Daniel Morán</strong>
      </v-col>
      <v-col class="text-center" cols="12" color="primary">
        <div class="d-flex flex-row justify-center align-baseline">
          <v-icon small>mdi-clock</v-icon>
          <div>{{ hours }}</div>
          <div>{{ minutes }}</div>
          <div>{{ seconds }}</div>
          <div></div>
        </div>
      </v-col>
    </v-row>
  </v-footer>
</template>
<script>
export default {
  props: {
    color: {
      type: String,
      default: "red",
    },
  },
  data() {
    return {
      hours: '',
      minutes: '',
      seconds: '',
    };
  },
  methods: {
    setTime() {
      setInterval(() => {
        const date = new Date();
        this.hours = date.getHours() + `:`;
        this.minutes = this.checkSingleDigit(date.getMinutes()) + `:`;
        this.seconds = this.checkSingleDigit(date.getSeconds());
      }, 1000);
    },
    checkSingleDigit(digit) {
      return ("0" + digit).slice(-2);
    },
  },
  created() {
    this.setTime();
  },
  computed: {
    currentYear() {
      return new Date().getFullYear()
    }
  }
};
</script>
<style lang=""></style>
