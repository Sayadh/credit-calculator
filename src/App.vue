<template>
  <div>
    <header>
      <img src="@/assets/Masrik.png" alt="">
      <div style="display: flex; flex-direction: column; align-items: start">
        <p><b>Դասարան `</b> 7/ա</p>
        <p><b>ՈՒսուցչուհուի `</b> Սիրան Դավթյան</p>
      </div>
    </header>
    <CreditCalculator />
  </div>
</template>

<script>
import CreditCalculator from './components/CreditCalculator.vue'

export default {
  name: 'App',
  components: {
    CreditCalculator
  }
}
</script>

<style>
header {
  position: fixed;
  display: flex;
  align-items: center;
  justify-content: center;
  column-gap: 20px;
  top: 0;
  width: 100%;
  background-color: #333;
  color: white;
  text-align: center;
  padding: 10px 0;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
  z-index: 1000;

  img  {
    width: 60px;
    height: 60px;
  }
}
* {
  margin: 0;
  padding: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 90px;
}
</style>
