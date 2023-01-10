<template>
  <section class="container">
    <div class="Wrapper">
      <h1 class="title">Vue 계산기</h1>
      <input class="SearchBar" readOnly v-model="result" />
      <div class="ButtonWrapper">
        <button class="TopButton" @click="allClear">AC</button>
        <button class="TopButton" @click="Delete">DEL</button>
        <button class="TopButton" value="%" @click="getOperation">%</button>
        <button class="CalButton" value="÷" @click="getOperation">÷</button>
        <button value="7" @click="getNumber">7</button>
        <button value="8" @click="getNumber">8</button>
        <button value="9" @click="getNumber">9</button>
        <button class="CalButton" value="×" @click="getOperation">×</button>
        <button value="4" @click="getNumber">4</button>
        <button value="5" @click="getNumber">5</button>
        <button value="6" @click="getNumber">6</button>
        <button class="CalButton" value="-" @click="getOperation">-</button>
        <button value="1" @click="getNumber">1</button>
        <button value="2" @click="getNumber">2</button>
        <button value="3" @click="getNumber">3</button>
        <button class="CalButton" value="+" @click="getOperation">+</button>
        <button class="ZeroButton" value="0" @click="getNumber">0</button>
        <button value="." @click="getPoint">.</button>
        <button class="CalButton" @click="getResult">=</button>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from "vue";

const result = ref("");
const point = ref(true);
const operation = ref(true);

const getNumber = (event) => {
  result.value = result.value + event.target.value;
  operation.value = true;
};

const getOperation = (event) => {
  if (operation.value) {
    result.value = result.value + event.target.value;
    operation.value = false;
  }
};

const getPoint = (event) => {
  if (result.value.length === 0) {
    return;
  }
  if (point.value) {
    result.value = result.value + event.target.value;
    point.value = false;
  }
};

const getResult = () => {
  const replace_str = result.value.replace(/×/gi, "*").replace(/÷/gi, "/");

  if (isNaN(eval(replace_str))) {
    result.value = "";
  } else if (eval(replace_str) == Infinity) {
    alert("0으로 나눌수 없습니다.");
    result.value = "";
    return false;
  } else {
    result.value = eval(replace_str);
  }
};

const Delete = () => {
  point.value = true;
  operation.value = true;
  const str = String(result.value).slice(0, -1);
  result.value = str;
};

const allClear = () => {
  point.value = true;
  result.value = "";
};

</script>

<style>
.Wrapper {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  max-width: 500px;
  width: 100%;
  padding: 35px 0;
  border-radius: 10px;
  margin: 0 auto;
  margin-top: 5%;
  background-color: #111;
}

.title {
  font-size: 2.75rem;
  line-height: 1.1;
  margin-bottom: 35px;
  color: #fff;
}

.SearchBar {
  max-width: 475px;
  height: 65px;
  margin-bottom: 25px;
  border-radius: 10px;
  font-size: 32px;
  border: none;
  text-align: right;
  padding-right: 20px;
}

.SearchBar:focus {
  outline: none;
}

.ButtonWrapper {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-gap: 10px;
}

button {
  background-color: #333;
  border: none;
  color: #fff;
  font-size: 1.5rem;
  border-radius: 10%;
  /* width: 90px;
  height: 90px; */
  padding: 25px 0;
  cursor: pointer;
  transition: 0.5s;
}

button:hover {
  background-image: linear-gradient(135deg, #f83600 0%, #f9d423 100%);
}

button:active {
  margin-left: 2px;
  margin-top: 2px;
  box-shadow: none;
}

.TopButton {
  background-color: #a6a6a6;
  font-size: 1.25rem;
}

.CalButton {
  background-color: #f98000;
}

.ZeroButton {
  grid-column: 1/3;
  width: 200px;
  border-radius: 7.5%;
}

@media screen and (max-width: 1024px) {
  .SearchBar {
    width: 380px;
  }

  .ButtonWrapper {
    max-width: 400px;
    width: 100%;
    margin: 0 auto;
  }
}

@media screen and (max-width: 640px) {
  .ButtonWrapper {
    width: 98%;
    height: 50%;
  }
}

@media screen and (max-width: 480px) {
  .SearchBar {
    max-width: 98%;
    width: 90%;
  }
  button {
    padding: 15px 0;
  }
  /* button {
    width: 100%;
    height: 100%;
    padding: 25px 0;
  }
  .ZeroButton {
    max-width: 100%;
  } */
}
</style>

