<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <div>
    <h4>xx 원룸</h4>
    <p>50 만원</p>
  </div>
  <div>
    <h4>xx 원룸</h4>
    <p>70 만원</p>
  </div>
</template>

<script>

export default {
  name: 'App',
  data(){ // 데이터 보관하는 곳. 일반 변수 뿐만 아니라 HTML 속성도 데이터 바인딩 가능
    return {
      products : ['역삼동원룸', '천호동원룸', '마포구원룸'],
    }
  },
  components: {
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
