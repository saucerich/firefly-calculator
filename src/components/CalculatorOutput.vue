<template>
  <div v-bind:class="{ 'purple': this.purple, 'green': this.green, 'blue': this.blue }">
      <div class='output'>
        <h2 class='output-text'> {{this.displayText}} </h2>
      </div>
  </div>
</template>

<script>
export default {
  name: 'CalculatorOutput',
  data: function () {
    return {
    }
  },

  props: {
    displayText: {
      type: String,
      default: "0"
    },
    purple: {
      type: Boolean,
      default: true,
    },
    green: {
      type: Boolean,
      default: false,
    },
    blue: {
      type: Boolean,
      default: false,
    },
  }
}
</script>

<style>

.output {
  border-bottom: 1px solid white;
  display: flex;
  justify-content: flex-end;
  padding-top: 40px;
  margin-right: 5px;
  margin-left: 5px;
}

.landscape {
  padding-top: 0px;
}

.output-text {
  color: white;
  font-size: 40px;
}

</style>
