<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div class="calculator">
      <input v-model="display" :class="displayClass" readonlyS />
      <div class="buttons">
        <button @click="appendToDisplay('7')">7</button>
        <button @click="appendToDisplay('8')">8</button>
        <button @click="appendToDisplay('9')">9</button>
        <button @click="appendToDisplay('/')">/</button>

        <button @click="appendToDisplay('4')">4</button>
        <button @click="appendToDisplay('5')">5</button>
        <button @click="appendToDisplay('6')">6</button>
        <button @click="appendToDisplay('*')">*</button>

        <button @click="appendToDisplay('1')">1</button>
        <button @click="appendToDisplay('2')">2</button>
        <button @click="appendToDisplay('3')">3</button>
        <button @click="appendToDisplay('-')">-</button>

        <button @click="appendToDisplay('0')">0</button>
        <button @click="appendToDisplay('.')">.</button>
        <button @click="calculate()">=</button>
        <button @click="appendToDisplay('+')">+</button>
      </div>
      <button @click="clearDisplay" class="clear-btn">C</button>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";
const msg = ref("Calculator");
const display = ref("0");
const appendToDisplay = (value) => {
  if (display.value === "0" && value !== ".") {
    display.value = value;
  } else {
    display.value += value;
  }
};
const calculate = () => {
  try {
    display.value = eval(display.value).toString();
  } catch (error) {
    display.value = "error";
  }
};

// computed property for dynamic class binding
const displayClass = computed(() => {
  return display.value.length > 12 ? "small-text" : "";
});
const clearDisplay = () => {
  display.value = "0";
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
input {
  padding: 10px 20px;
  margin-bottom: 20px;
  border-radius: 8px;
}
.calculator {
  max-width: 300px;
  margin: 0 auto;
  padding: 20px;
  border: 4px solid #ccc;
  border-radius: 10px;
  background-color: #615efc;
  box-shadow: rgba(0, 0, 0, 0.25) 0px 54px 55px,
    rgba(0, 0, 0, 0.12) 0px -12px 30px, rgba(0, 0, 0, 0.12) 0px 4px 6px,
    rgba(0, 0, 0, 0.17) 0px 12px 13px, rgba(0, 0, 0, 0.09) 0px -3px 5px;
}
.display {
  width: 100%;
  margin-bottom: 10px;
  padding: 10px;
  font-size: 18px;
  text-align: right;
}
.buttons {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 10px;
}
button {
  width: 100%;
  padding: 10px;
  font-size: 18px;
  border-radius: 10px;
  outline: none;
  &:hover {
    background-color: #ccc;
  }
}
.clear-btn {
  width: 100%;
  margin-top: 10px;
}
.small-text {
  font-size: 14px;
}
</style>
