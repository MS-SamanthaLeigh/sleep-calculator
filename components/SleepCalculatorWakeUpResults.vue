<template>
  <div class="wake-up-results">
    <h2 class="font-bold py-2">
      WAKE UP TIMES
    </h2>
    <div class="flex flex-wrap justify-center py-5">
      <div v-for="time in results" class="text-black bg-white border border-solid border-blue-500 rounded mx-1 my-2 px-1">
        {{ time | moment("HH:mm") }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "WakeUpResults",
  props: [
    "time"
  ],
  computed: {
    results: function() {
      let time = this.$moment(this.time).add({minute: 15})
      let times = []

      for (let i = 0; i < 6; i++) {
        time = this.$moment(time).add({minute: 90})
        times.push(time)
      }

      return times

    }
  }
}
</script>
