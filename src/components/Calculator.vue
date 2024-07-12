<template>
  <div class="p-3" style="width: 400px; margin: 50px auto; background: #234">
    <!-- result -->
    <div
      class="rounded my-2 py-3 px-1 text-right lead font-weight-bold text-white bg-vue-dark"
    >
      {{ calcValue || 0 }}
    </div>
    <!-- Buttons -->
    <div class="row">
      <div class="col-3 px-1" v-for="n in calcElements" :key="n">
        <div
          class="lead text-white text-center m-1 py-3 bg-vue-dark rounded hover-class"
          :class="{
            'bg-vue-green': ['c', '+', '-', '=', '%', '*', '/'].includes(n),
          }"
          @click="action(n)"
        >
          {{ n }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Cal-culator",
  props: {
    msg: String,
  },
  data() {
    return {
      calcValue: "",
      calcElements: [
        "c",
        "*",
        "/",
        "-",
        7,
        8,
        9,
        "+",
        4,
        5,
        6,
        "%",
        1,
        2,
        3,
        "=",
        0,
        ".",
      ],
      operator: "",
      previousCalculatorValue: "",
    };
  },
  methods: {
    action(n) {
      /* Append value */
      if (!isNaN(n) || n === ".") {
        this.calcValue += n + "";
      }

      /* Clear value */
      if (n === "c") {
        this.calcValue = "";
      }

      /* Percentage */
      if (n === "%") {
        this.calcValue = this.calcValue / 100 + "";
      }

      /* Operators */
      if (["/", "*", "-", "+"].includes(n)) {
        this.operator = n;
        this.previousCalculatorValue = this.calcValue;
        this.calcValue = "";
      }

      /* Calculate result using the eval function */
      if (n === "=") {
        this.calcValue = eval(
          this.previousCalculatorValue + this.operator + this.calcValue
        );
        this.previousCalculatorValue = "";
        this.operator = "";
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.bg-vue-dark {
  background-color: #31475e;
}
.hover-class {
  cursor: pointer;
  background-color: #3d5875;
}
.bg-vue-green {
  background-color: #f0bd48;
}
</style>
