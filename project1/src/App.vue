<template>

  <div class="menu">
    <a v-for="a in 메뉴들" :key="a">{{ a }}</a> <!-- 반복문 형식: <태그 v-for="작명 in 횟수/데이터(array, object) :key="작명"> -->
  </div>

  <!--
  아래와 같은 방법을 반복문으로 해결
  <div v-for="(a,i) in products" :key="i"> a에는 아이템, i에는 인덱스
    <h4>{{a}}</h4>
    <p>50만원</p>
  </div>
  -->

  <div>
    <h4>{{products[0]}}</h4>
    <p>50 만원</p>
    <button @click="increase">허위매물신고</button> <span>신고수: {{신고수}}</span> <!-- @click == v-on:click -->
  </div>
  <div>
    <h4>{{products[1]}}</h4>
    <p>60 만원</p>
  </div>
  <div>
    <h4>{{products[2]}}</h4>
    <p>70 만원</p>
  </div>
</template>

<script>

export default {
  name: 'App',
  data(){ // 데이터 보관하는 곳. 일반 변수 뿐만 아니라 HTML 속성도 데이터 바인딩 가능
    return {
      신고수 : 0,
      메뉴들 : ['Home', 'Shop', 'About'],
      products : ['역삼동원룸', '천호동원룸', '마포구원룸'],
    }
  },
  methods: { // 자바스크립트 함수는 여기 위치에 작성해야 함.
    increase() {
      this.신고수 += 1; // 내부의 변수를 사용할 때는 this 키워드 잊지 말자
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
