<template>
  <div class='main'>
    <b-dropdown block variant="outline-light" v-bind:class="{ 'purple-top': this.purple, 'green-top': this.green, 'blue-top': this.blue }" class="hidden">
          <template #button-content>
                <b-icon icon="list" aria-hidden="true">Dropdown</b-icon>
        </template>
        <b-dropdown-group id="previous" class="small">
            <b-dropdown-item>
                <b-icon aria-hidden="true"></b-icon>{{this.thirdCalc}}
                <span icon="circle"> </span>
            </b-dropdown-item>
            <b-dropdown-item>
                <b-icon aria-hidden="true"></b-icon>{{this.secondCalc}}
                <span icon="circle"> </span>
            </b-dropdown-item>
            <b-dropdown-item>
                <b-icon aria-hidden="true"></b-icon>{{this.lastCalc}}
                <span icon="circle"> </span>
            </b-dropdown-item>
        </b-dropdown-group>
        <b-dropdown-divider></b-dropdown-divider>
        <b-dropdown-group id="themes" header="Themes" size="sm">
            <b-dropdown-item-button v-on:click="change('green')">
                <b-icon aria-hidden="true"></b-icon>Green
                <span icon="circle"> </span>
            </b-dropdown-item-button>
            <b-dropdown-item-button v-on:click="change('purple')">
                <b-icon aria-hidden="true"></b-icon>Purple
                <span icon="circle"> </span>
            </b-dropdown-item-button>
            <b-dropdown-item-button v-on:click="change('blue')">
                <b-icon aria-hidden="true"></b-icon>Blue
                <span icon="circle"> </span>
            </b-dropdown-item-button>
        </b-dropdown-group>
    </b-dropdown>
    <div class="landscape-ham">
        <div class="landscape-prev">
            <h3 class="l-header" style="color:white; font-size:17px;">{{this.thirdCalc}}</h3>
            <h3 class="l-header" style="color:white; font-size:17px;">{{this.secondCalc}}</h3>
            <h3 class="l-header" style="color:white; font-size:17px;">{{this.lastCalc}}</h3>
        </div>
        <div class="landscape">
            <b-button pill variant="outline-light" v-on:click="change('green')">Green</b-button>
            <b-button pill variant="outline-light" v-on:click="change('purple')">Purple</b-button>
            <b-button pill variant="outline-light" v-on:click="change('blue')">Blue</b-button>
        </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HamburgerMenu',
  data: function () {
    return {
    }
  },

  props: {
    lastCalc: {
      type: String,
      default: "0"
    },
    thirdCalc: {
      type: String,
      default: "0"
    },
    secondCalc: {
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
  },

  methods: {
    change: function (text) {
      this.$emit('change', text)
    }
  }
}
</script>

<style>
.purple-top {
    background-color: #645390;
    border-bottom: 5px solid #332550;
    padding-top: 20px;
}

.green-top {
    background-color: #73b504;
    border-bottom: 5px solid #2E4502;
    padding-top: 20px;
}

.blue-top {
    background-color: #267EA6;
    border-bottom: 5px solid #023047;
    padding-top: 20px;
}

.hidden {
    display:none;
}

.l-header {
    font: white;
}
.landscape-ham {
    display:flex;
    flex-direction: column;
    width: 200px;
}

.landscape {
    display:flex;
    flex-direction: column;
}

.landscape-prev {
    display:flex;
    flex-direction: column;
    height:110px;
}
</style>
