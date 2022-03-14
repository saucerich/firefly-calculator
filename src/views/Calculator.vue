<template>
  <div v-bind:class="{ 'purple': this.purple, 'green': this.green, 'blue': this.blue }">
    <div class="">
    <HamburgerMenu
    v-bind:lastCalc="this.lastCalc"
    v-bind:secondCalc="this.secondCalc"
    v-bind:thirdCalc="this.thirdCalc"
    v-on:change="themeChange($event)"
    v-bind:purple="this.purple"
    v-bind:green="this.green"
    v-bind:blue="this.blue"/>
    <div>
    <CalculatorOutput
    v-bind:displayText="this.displayText"
    v-bind:purple="this.purple"
    v-bind:green="this.green"
    v-bind:blue="this.blue"/>
    <CalculatorButtons
    v-on:numPress="append($event)"
    v-on:operation="append($event)"
    v-on:clear="clear()"
    v-on:eval="evaluate()"
    v-bind:purple="this.purple"
    v-bind:green="this.green"
    v-bind:blue="this.blue"/>
    </div>
    </div>
  </div>
</template>

<script>
import HamburgerMenu from '@/components/HamburgerMenu.vue'
import CalculatorOutput from '@/components/CalculatorOutput.vue'
import CalculatorButtons from '@/components/CalculatorButtons.vue'

export default {
  name: 'Calculator-r',
  components: {
    HamburgerMenu,
    CalculatorOutput,
    CalculatorButtons
  },


  data () {
    return {
      displayText: "0",
      lastCalc: "",
      secondCalc: "",
      thirdCalc: "",
      formula: "",
      theme: "purple",
      purple: true,
      green: false,
      blue: false,
      containsOp: false,
    }
  },

  methods: {
    /*
     * FUNCTION: evaluate()
     * PARAMETERS: none
     * FUNCTIONALITY: evaluate() was already written by instructors.
     */
    evaluate () {
      try {
        /* WARNING! Never use eval in production code. */
        // eslint-disable-next-line no-eval
        let result = eval(this.formula)
        this.formulaAlert = false
        result = ""+Math.round(result*100)/100
        if (result==="NaN") {
          this.clear()
        } else {
          this.push(this.displayText+"= "+result)
          this.displayText = ""+result
          this.formula = ""+result
          this.containsOp= false
        }
      } catch (exception) {
        this.clear()
      }
    },
    /*
     * FUNCTION: isOp()
     * PARAMETERS: value: any string value
     * FUNCTIONALITY: checks to see if value is "+", "-", "×", "÷", "/" or "*"
     * If so returns true, else false
     */
    isOp (value) {
      if (value === "÷" || value==="×" || value==="+" || value=== "-" || value==="/" || value==="*") {
        return true
      } else return false
    },

    /*
     * FUNCTION: formulize()
     * PARAMETERS: value: "+", "-", "×", "÷" or a number string
     * FUNCTIONALITY:
     * "+" returns "+"
     * "-" returns "-"
     * "×" returns "*"
     * "÷" returns "/"
     */
    formulize (value) {
      if (value==="+") return "+"
      if (value==="-") return "-"
      if (value==="×") return "*"
      if (value==="÷") return "/"
      else return value
    },

    /*
     * FUNCTION: append()
     * PARAMETERS: value: Value to be appended to end of string.
     * FUNCTIONALITY: append() first checks to see if this.formula has been set.
     * If not, then it just replaces the value. If it has been set, it adds the
     * user input string (the button pressed) to the end of this.formula.
     */
    append (value) {
      console.log("LENGTH: "+this.displayText.length)
      if (this.displayText.length >5){
        return
      }
      if (this.containsOp && this.isOp(value)) {
        // If value is op and last char is op replace last char
        let last = this.formula.charAt(this.formula.length -1)
        if (this.isOp(last)){
          this.backspace()
        }
        // If in format (num op num) evaluate and update display
        else {
          let result = eval(this.formula)
          result = Math.round(result*100)/100
          this.push(this.displayText+"= "+result)
          this.displayText = ""+result
          this.formula= ""+result
        }
      }
      //if there's not already an op and value is an op start contains op to true
      if (!this.containsOp && this.isOp(value)) this.containsOp=true

      // if it's displaying 0 replace it with a number
      if (this.displayText==="0" && !this.isOp(value)) {
        this.displayText=value
        this.formula=value
      } else {
        this.displayText=this.displayText+value
        this.formula=this.formula+this.formulize(value)
      }

    },

    /*
     * FUNCTION: clear()
     * PARAMETERS: NONE
     * FUNCTIONALITY: clears the calculator to default settings
     */
    clear () {
      this.displayText = "0"
      this.formula = ""
      this.containsOp = false
    },

    /*
     * FUNCTION: backspace()
     * PARAMETERS: none
     * FUNCTIONALITY: backspace() uses slice() to cut the last character off from
     * the string. It uses toString() to ensure that this.formula is a string
     * (otherwise this function would not work when deleting the last character
     * from a result).
     */
    backspace () {
      this.displayText= this.displayText.slice(0, (this.displayText.length -1))
      this.formula=this.formula.slice(0, (this.formula.length -1))
    },

    /*
     * FUNCTION: push()
     * PARAMETERS: text: to replace this.lastCalc
     * FUNCTIONALITY: changes thirdCalc to the value of secondCalc
     * changes secondCalc to the value of thirdCalc
     * and changes the value of this.lastCalc to text parameter
     */
    push (text) {
      this.thirdCalc = this.secondCalc
      this.secondCalc = this.lastCalc
      this.lastCalc = text
    },
    /*
      * FUNCTION: themeChange()
      * PARAMETERS: theme: the theme to be changed to
      * FUNCTIONALITY: changes the theme of the calculator depending on
      * theme variable
      */
      themeChange (theme) {
        if (theme==="green") {
          this.green=true
          this.blue = false
          this.purple= false
        } if (theme==="blue") {
          this.green=false
          this.blue = true
          this.purple= false
        } if (theme==="purple") {
          this.green=false
          this.blue = false
          this.purple= true
        }
    }
  }
}
</script>

<style>
.purple {
  background-color: #43326e;
}

.green {
  background-color: #538103;
}

.blue {
  background-color: #1A7B93;
}

.landscapemain {
  display: flex;
  flex-direction: row;
  margin-left:10px;
}

</style>
