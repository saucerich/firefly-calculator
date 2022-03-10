<template>
  <div class='buttons' v-bind:class="{ 'purple': this.purple, 'green': this.green, 'blue': this.blue }">
    <b-container class="portrait">
      <b-row class="gx-1">
        <b-col cols=3><b-button pill variant="outline-warning" v-on:click="clear()" class="circle">C</b-button></b-col>
        <b-col offset=3 cols=3><b-button pill variant="warning" v-on:click="operation('÷')" class="circle">÷</b-button></b-col>
        <b-col cols=3><b-button pill variant="warning" v-on:click="operation('×')" class="circle">×</b-button></b-col>
      </b-row>
      <b-row class="gx-1">
        <b-col><b-button pill variant="outline-light" v-on:click="pressNum('7')" class="circle">7</b-button></b-col>
        <b-col><b-button pill variant="outline-light" v-on:click="pressNum('8')" class="circle">8</b-button></b-col>
        <b-col><b-button pill variant="outline-light" v-on:click="pressNum('9')" class="circle">9</b-button></b-col>
        <b-col><b-button pill variant="warning" v-on:click="operation('-')" class="circle">-</b-button></b-col>
      </b-row>
      <b-row class="gx-1">
        <b-col><b-button pill variant="outline-light" v-on:click="pressNum('4')" class="circle">4</b-button></b-col>
        <b-col><b-button pill variant="outline-light" v-on:click="pressNum('5')" class="circle">5</b-button></b-col>
        <b-col><b-button pill variant="outline-light" v-on:click="pressNum('6')" class="circle">6</b-button></b-col>
        <b-col><b-button pill variant="warning" v-on:click="operation('+')" class="circle">+</b-button></b-col>
      </b-row>
      <b-row class="gx-1">
        <b-col cols=9>
          <b-row class="gx-1">
            <b-col><b-button pill variant="outline-light" v-on:click="pressNum('1')" class="circle">1</b-button></b-col>
            <b-col><b-button pill variant="outline-light" v-on:click="pressNum('2')" class="circle">2</b-button></b-col>
            <b-col><b-button pill variant="outline-light" v-on:click="pressNum('3')" class="circle">3</b-button></b-col>
          </b-row>
          <b-row class="gx-1">
            <b-col cols=8 ><b-button pill variant="outline-light" class="zero" v-on:click="pressNum('0')">0</b-button></b-col>
            <b-col cols=3><b-button pill variant="outline-light" v-on:click="pressNum('.')" class="circle">.</b-button></b-col>
          </b-row>
        </b-col>
        <b-col cols=3 >
          <b-button pill variant="warning" class="pt-4 pb-4 equal" v-on:click="eval()">=</b-button>
        </b-col>
      </b-row>
    </b-container>
    <b-container class="landscape hidden">
      <b-row class="gx-1">
        <b-col cols=10>
          <b-row class="gx-1">
            <b-col><b-button pill variant="outline-light" v-on:click="pressNum('7')" class="circle">7</b-button></b-col>
            <b-col><b-button pill variant="outline-light" v-on:click="pressNum('8')" class="circle">8</b-button></b-col>
            <b-col><b-button pill variant="outline-light" v-on:click="pressNum('9')" class="circle">9</b-button></b-col>
            <b-col cols=3><b-button pill variant="warning" v-on:click="operation('÷')" class="circle">÷</b-button></b-col>
          </b-row>
          <b-row class="gx-1">
            <b-col><b-button pill variant="outline-light" v-on:click="pressNum('4')" class="circle">4</b-button></b-col>
            <b-col><b-button pill variant="outline-light" v-on:click="pressNum('5')" class="circle">5</b-button></b-col>
            <b-col><b-button pill variant="outline-light" v-on:click="pressNum('6')" class="circle">6</b-button></b-col>
            <b-col cols=3><b-button pill variant="warning" v-on:click="operation('×')" class="circle">×</b-button></b-col>
          </b-row>
          </b-col>
        <b-col cols=2 >
          <b-col cols=3><b-button pill variant="outline-warning" v-on:click="clear()" class="pt-4 pb-4 equal">C</b-button></b-col>
        </b-col>
      </b-row>
      <b-row class="gx-1">
        <b-col cols=10>
          <b-row class="gx-1">
            <b-col><b-button pill variant="outline-light" v-on:click="pressNum('1')" class="circle">1</b-button></b-col>
            <b-col><b-button pill variant="outline-light" v-on:click="pressNum('2')" class="circle">2</b-button></b-col>
            <b-col><b-button pill variant="outline-light" v-on:click="pressNum('3')" class="circle">3</b-button></b-col>
            <b-col cols=3><b-button pill variant="warning" v-on:click="operation('-')" class="circle">-</b-button></b-col>
          </b-row>
          <b-row class="gx-1">
            <b-col cols=6 ><b-button pill variant="outline-light" class="zero" v-on:click="pressNum('0')">0</b-button></b-col>
            <b-col cols=3><b-button pill variant="outline-light" v-on:click="pressNum('.')" class="circle">.</b-button></b-col>
            <b-col cols=3><b-button pill variant="warning" v-on:click="operation('+')" class="circle">+</b-button></b-col>
          </b-row>
        </b-col>
        <b-col cols=2 >
          <b-button pill variant="warning" class="pt-4 pb-4 equal" v-on:click="eval()">=</b-button>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
export default {
  name: 'CalculatorButtons',
  data: function () {
    return {
      announcementText: ""
    }
  },
  props: {
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
  },

  methods: {
    pressNum: function (num) {
      this.$emit('numPress', num)
    },

    operation: function (op) {
      this.$emit('operation', op)
    },

    clear: function () {
      this.$emit('clear')
    },

    eval () {
      this.$emit('eval')
    }
  }
}
</script>

<style>
.buttons {
  background-color: #43326e;
  margin-top: 8px;
  margin-bottom: 10px;
}

.circle {
  width: 37px;
  height: 37px;
  margin-top: 3px;
}

.zero {
  width:78px;
  height:37px;
  margin-top: 3px;
}

.equal {
  margin-top: 3px;
  height: 78px;
}

.hidden {
  display: none;
}

</style>
