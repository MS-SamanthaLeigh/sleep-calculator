<template>
  <div class="calculator-setup">
    <p class="">Sleep Calculator</p>
      <br>
<!-- SWITCH FOR 'WHEN SHOULD I GO TO BED' VIEW -->
    <h2 class="calc-title py-2 ">
      If I want to wake up at...
    </h2>
    <div class="setup-controls flex">
      <time-control class="w-1/2"
        v-bind:items="hours"
        v-bind:selected="hh"
        v-on:set-value="setHour" />
      <time-control class="w-1/2"
        v-bind:items="minutes"
        v-bind:selected="mm"
        v-on:set-value="setMinute" />
    </div>
    <div class="calc-actions py-2">
      <button class="mv-btn--secondary bg-white text-blue border-solid border py-2 px-4 rounded-full hover:bg-blue-100 text-blue-500 font-bold py-2 px-4" @click="finish('wake-up')">
        When should I go to bed?
      </button>
    </div>


<!-- SWITCH FOR 'WHEN SHOULD I GET UP' VIEW -->
    <!-- <h2 class="calc-title py-2">
      If I go to sleep now...
    </h2>
    <div class="calc-actions py-2">
      <button class="bg-white text-blue border-solid border py-2 px-4 rounded-full hover:bg-blue-100 text-blue-500 font-bold py-2 px-4" @click="finish('wake-up')">
        When should I get up?
      </button>
    </div> -->

  </div>
</template>

<script>
import TimeControl from "~/components/SleepCalculatorTimeControl.vue"

export default {
  name: "CalculatorSetup",
  components: {
    TimeControl
  },
  data: function () {
    return {
      hours: this._.range(0, 24),
      minutes: this._.range(0, 60, 5),
      hh: 0,
      mm: 0
    }
  },
  methods: {
    finish: function(mode) {
      this.$emit("setup-completed", {
        mode,
        hh: this.hh,
        mm: this.mm
      })
    },
    setHour: function(value) {
      this.hh = value
    },
    setMinute: function(value) {
      this.mm = value
    },
  }
}
</script>

<style scoped>
  .calculator-setup,
  .calculator-setup .setup-controls {
    margin: 10px 0 15px;
  }
</style>