<script setup>
import { ref, computed } from "vue";

const titulo = "VUE 3 Counter";
let inicial = ref(0);

const incrementar = () => {
  inicial.value += 1;
};

const decrementar = () => {
  inicial.value -= 1;
};

const reset = () => {
  inicial.value = 0;
  favNumbers.value = [];
};

const classCounter = computed(() => {
  if (inicial.value === 0) {
    return "zero";
  }
  if (inicial.value > 0) {
    return "green";
  }
  if (inicial.value < 0) {
    return "red";
  }
});

const favNumbers = ref([]);

const addFav = () => {
  favNumbers.value.push(inicial.value);
  console.log(alreadyAdd.value);
};

let alreadyAdd = computed(() => {
  const exists = favNumbers.value.includes(inicial.value);

  if (exists) {
    return true;
  } else {
    return false;
  }
});
</script>

<template>
  <div class="container">
    <div>
      <h1>{{ titulo }}</h1>
    </div>
    <div class="fav-n">
      <h4>Fav numbers:</h4>
      <p v-for="numbers in favNumbers">{{ numbers }},</p>
    </div>
    <div class="counter">
      <button @click="decrementar()">-</button>
      <h2 :class="classCounter">{{ inicial }}</h2>
      <button @click="incrementar()">+</button>
    </div>
    <div class="btns">
      <button
        :class="alreadyAdd === true ? 'gray' : 'normal'"
        :disabled="alreadyAdd"
        @click="addFav()"
      >
        Add ⭐
      </button>
      <button class="reset" @click="reset()">Reset</button>
    </div>
  </div>
</template>

<style>
.container {
  display: flex;
  flex-direction: column;
  margin: 0 auto;
  min-width: 240px;
}
.counter {
  display: flex;
  margin-top: 20px;
  border: 1px solid wheat;
  padding: 10px 20px;
  align-items: center;
}
h1 {
  color: pink;
  margin-bottom: 10px;
  text-align: center;
}

.fav-n {
  display: flex;
  gap: 10px;
  border: 1px solid wheat;
  padding: 10px 20px;
}

.gray {
  color: gray;
}

p {
  overflow-wrap: break-word;
  word-wrap: break-word;
  hyphens: auto;
}

.btns {
  display: flex;
  justify-content: space-between;
}

.green {
  color: green;
}

.red {
  color: red;
}

.zero {
  color: darkgoldenrod;
}
button {
  border-radius: 3px;
  padding: 15px 15px;
  border: 0;
  margin: 0 auto;
  cursor: pointer;
  background-color: rgba(245, 222, 179, 0);
  color: wheat;
  font-size: 21px;
}
</style>
