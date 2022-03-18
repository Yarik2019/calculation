<template>
  <div id="app">
    <div class="calculate">
      <div class="grid">
        <input type="text" v-model="result" placeholder="0" />
        <button
          @click="input(number)"
          class="cell num"
          v-for="number in numbers"
          :key="number"
        >
          {{ number }}
        </button>
        <button
          @click="input(operation)"
          class="cell op"
          v-for="operation in operations"
          :key="operation"
        >
          {{ operation }}
        </button>
        <button @click="reset" class="cell op">R</button>
        <button @click="calc" class="cell op">=</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      result: "",
      numbers: [1, 2, 3, 4, 5, 6, 7, 8, 9, 0],
      operations: ["+", "-", "*", "/", '%'],
    };
  },
  created() {
    let calc = JSON.parse(window.localStorage.getItem(
      "calculation"
    ));
    this.result = calc;
  },
  methods: {
    input(char) {
      this.result = this.result.toString();
      this.result += char;
    },
    reset() {
      this.result = "";
    },
    calc() {
      this.result = eval(this.result);
    },
  },
  watch: {
    result() {
      window.localStorage.setItem("calculation", JSON.stringify(this.result));
    },
  },
};
</script>

<style>
* {
  font-family: "Gilroy", sans-serif;
  transition: 0.3s all;
  font-weight: 600;
}
#app {
  width: 100%;
  height: 90vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
.calculate {
  max-width: 200px;
  box-shadow: 0 3px 15px grey;
}
input[type="text"] {
  width: 200px;
  border: 0;
  color: #243849;
  font-size: 18px;
  padding: 5px 5px;
  text-align: right;
}
.grid {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  width: 100%;
}
.cell {
  flex: 33%;
  height: 50px;
  font-size: 18px;
  border: none;
}
.num {
  background-color: #243849;
  color: #fff;
  font-weight: 400;
}
.cell:hover {
  background-color: #182530;
}
.op {
  background-color: #ff9900;
  color: #243849;
}
</style>
