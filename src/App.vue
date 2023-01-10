<template>
  <section class="container">
    <div class="Wrapper">
      <h1 class="title">Nuxt 계산기</h1>
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

<script>
export default {
  data() {
    return {
      result: "",
      point: true,
      operation: true,
    };
  },
  methods: {
    getNumber(event) {
      this.result = this.result + event.target.value;
      this.operation = true;
    },
    getOperation(event) {
      if (this.operation) {
        this.result = this.result + event.target.value;
        this.operation = false;
      }
    },
    getPoint(event) {
      if (this.result.length === 0) {
        return;
      }
      if (this.point) {
        this.result = this.result + event.target.value;
        this.point = false;
      }
    },
    getResult() {
      const replace_str = this.result.replace(/×/gi, "*").replace(/÷/gi, "/");

      if ( isNaN(eval(replace_str)) ) {
        this.result = "";
      }
      else if ( eval(replace_str) == Infinity ) {
        alert("0으로 나눌수 없습니다.");
        this.result = "";
        return false;
      }
      else {
        this.result = eval(replace_str);
      }
    },
    Delete() {
      this.point = true;
      this.operation = true;
      const str = String(this.result).slice(0, -1);
      this.result = str;
    },
    allClear() {
      this.point = true;
      this.result = "";
    },
  },
};
</script>

<style>
.Wrapper {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  max-width: 500px;
  padding: 35px 0;
  border-radius: 10px;
  margin: 0 auto;
  margin-top: 5%;
  background-color: #111;
  overflow: hidden;
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
  width: 90px;
  height: 90px;
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
  .ButtonWrapper {
    max-width: 90%;
    margin: 0 auto;
  }
  .SearchBar {
    max-width: 98%;
    width: 90%;
  }
  button {
    width: 75px;
    height: 75px;
  }
  .ZeroButton {
    width: 175px;
  }
}
</style>

