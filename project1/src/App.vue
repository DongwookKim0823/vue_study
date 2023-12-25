<template>

  <!-- 조건문 사용하기
  <div v-if="1 == 3">
    안녕하세요3
  </div>
  <div v-else-if="1 == 2">
    안녕하세요2
  </div>
  <div v-else>
    안녕하세요1
  </div> -->

  <div class="black-bg" v-if="모달창열렸니 == true">
    <div class="white-bg">
      <h4>{{ 원룸들[누른거].title }}</h4>
      <p>{{ 원룸들[누른거].content }}</p>
      <botton @click="모달창열렸니 = false">닫기</botton>
    </div>
  </div>

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

  <div v-for="(작명,i) in 원룸들" :key="i"> <!-- HTML 태그안의 속성 데이터바인딩은 :어쩌구, HTML 태그안의 내용 데이터바인딩은 {{ 어쩌구 }} -->
    <img :src="원룸들[i].image" class="room-img"> <!-- 이미지는 src/assets 디렉토리에 저장하자 -->
    <h4 @click="모달창열렸니 = true; 누른거 = i">{{ 원룸들[i].title }}</h4> <!-- @click == v-on:click -->
    <p>{{ 원룸들[i].price }}원</p>
  </div>
  <!-- <div>
    <img src="./assets/room1.jpg" class="room-img">
    <h4>{{products[1]}}</h4>
    <p>60 만원</p>
    <button @click="신고수[1]++">허위매물신고</button>
    <span>신고수: {{신고수[1]}}</span> 
  </div>
  <div>
    <img src="./assets/room2.jpg" class="room-img">
    <h4>{{products[2]}}</h4>
    <p>70 만원</p>
    <button @click="신고수[2]++">허위매물신고</button>
    <span>신고수: {{신고수[2]}}</span>
  </div> -->
</template>

<script>
import data from './assets/oneroom.js' // import/export 문법 쓰는 법 1) export default 변수명 or {변수명1, 변수명2, ...} 2) import 변수명 or {변수명1, 변수명2, ...} from 그 파일경로 ,참고로 변수 선언하고 사용 안하면 에러

export default {
  name: 'App',
  data(){ // 데이터 보관하는 곳. 일반 변수 뿐만 아니라 HTML 속성도 데이터 바인딩 가능
    return {
      누른거: 0,
      원룸들: data,
      // 동적 UI 만드는 법. 1 UI의 현재 상태를 데이터로 저장해둠 2 데이터에 따라 UI가 어떻게 보일지 작성
      모달창열렸니: false, // 1 UI의 현재 상태를 데이터로 저장해둠
      신고수 : [0,0,0],
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
body {
  margin: 0
}
div {
  box-sizing: border-box;
}
.black-bg {
  width: 100%; height: 100%;
  background: rgba(0,0,0,0.5);
  position: fixed; padding: 20px;
}
.white-bg {
  width: 100%; background: white;
  border-radius: 8px;
  padding: 20px;
}


.room-img {
  width: 100%;
  margin-top: 40px;
}

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
