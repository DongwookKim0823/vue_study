<template>

  <div class="menu">
    <a v-for="a in 메뉴들" :key="a"> {{ a }} </a> <!-- 반복문 형식: <태그 v-for="작명 in 횟수/데이터(array, object) :key="작명"> -->
  </div>

  <div>
    <h4>{{products[0]}}</h4>
    <p>50 만원</p>
  </div>
  <div>
    <h4>{{products[1]}}</h4>
    <p>50 만원</p>
  </div>
  <div>
    <h4>{{products[2]}}</h4>
    <p>50 만원</p>
  </div>
</template>

<script>

export default {
  name: 'App',
  data(){ // 데이터 보관하는 곳. 일반 변수 뿐만 아니라 HTML 속성도 데이터 바인딩 가능
    return {
      메뉴들 : ['Home', 'Shop', 'About'],
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
}

.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}

.menu a {
  color: white;
  padding: 10px;
}

</style>
