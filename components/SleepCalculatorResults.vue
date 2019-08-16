<template>
  <div>
      <div class="py-2">
        <button class="bg-white text-blue border-solid border py-2 px-4 rounded-full" @click="reset">
          CALCULATE AGAIN
        </button>
      </div>
      <div class="info text-black">
      <p>It takes the average human about 15 minutes to fall asleep. <br>
        If you go to sleep right now, you should try to wake up at one of the following times:</p>
      <div class="calculator-results">
          <go-to-bed-results
            v-if="config.mode == 'go-to-bed'"
            v-bind:time="time" />
          <wake-up-results
            v-else
            v-bind:time="time" />
      </div>  <div class="calculator-results"></div>
      </div>
  </div>
</template>

<script>
import GoToBedResults from "~/components/SleepCalculatorGoToBedResults.vue"
import WakeUpResults from "~/components/SleepCalculatorWakeUpResults.vue"

export default {
  name: "CalculatorResults",
  components: {
    GoToBedResults,
    WakeUpResults
  },
  props: [
    "config"
  ],
  computed: {
    time: function() {
      if (this.config.mode == "go-to-bed") {
        return this.$moment({hour: this.config.hh, minute: this.config.mm})
      } else {
        return this.$moment()
      }
    }
  },
  methods: {
    reset: function() {
      this.$emit("reset")
    }
  }
}
</script>
