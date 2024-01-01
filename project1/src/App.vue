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

  <!-- <div class="start" :class="{ end : 모달창열렸니 }"> :class="{ end : 모달창열렸니 }"는 조건부로 클래스를 데이터바인딩하는 유용한 방법
    <Modal @closeMoal="모달창열렸니 = false" v-bind:원룸들="원룸들" :누른거="누른거" v-bind:모달창열렸니="모달창열렸니" /> 
  </div> -->
  <transition name="fade"> <!-- 위 방법은 js로 애니메이션 주는 방법, 지금 방법은 vue로 애니메이션 주는 방법. 이후는 style 참고-->
    <Modal @closeMoal="모달창열렸니 = false" v-bind:원룸들="원룸들" :누른거="누른거" v-bind:모달창열렸니="모달창열렸니" /> <!--자식 컴포넌트가 부모가 갖고 있는 데이터를 쓰려면 props로 데이터를 전송해야함. 밑에 있는 데이터 보내고(v-bind 생략 가능)>등록하고>가져다 쓰셈. props로 다양한 자료형 입력 가능. 문자를 전송할 때 ':' 생략 가능 -->
    <!-- @closeMoal는 부모 데이터한테 신호를 받고 값을 변경 -->
  </transition>

  <div class="menu">
    <a v-for="a in 메뉴들" :key="a">{{ a }}</a> <!-- 반복문 형식: <태그 v-for="작명 in 횟수/데이터(array, object) :key="작명"> -->
  </div>

  <Discount v-if="showDiscount == true"/> <!--UI만드는법 1) UI현재 상태 만들어두고 2) 그거에 따라 보이는지 안보이는지-->

  <button @click="priceSort">가격순정렬</button> <!--생js로 정렬 기능 1)원룸들 데이터 정렬하고 2)HTML에 반영. Vue라면 원룸들 데이터를 정렬하면 끝-->
  <button @click="sortBack">되돌리기</button>

  <!--
  아래와 같은 방법을 반복문으로 해결
  <div v-for="(a,i) in products" :key="i"> a에는 아이템, i에는 인덱스
    <h4>{{a}}</h4>
    <p>50만원</p>
  </div>
  -->

  <Card @openModal="모달창열렸니 = true; 누른거 = $event" :원룸="원룸들[i]" v-for="(작명,i) in 원룸들" :key="i" /> <!-- 부모가 메세지 수신할 때는 <자식컴포넌트 @작명한거="">, $event는 자식이 보낸 데이터를 담는 변수 -->
  <!-- <Card :원룸="원룸들[1]" />
  <Card :원룸="원룸들[2]" />
  <Card :원룸="원룸들[3]" />
  <Card :원룸="원룸들[4]" />
  <Card :원룸="원룸들[5]" /> -->

  <!-- <div v-for="(작명,i) in 원룸들" :key="i"> HTML 태그안의 속성 데이터바인딩은 :어쩌구, HTML 태그안의 내용 데이터바인딩은 {{ 어쩌구 }}
    <img :src="원룸들[i].image" class="room-img"> 이미지는 src/assets 디렉토리에 저장하자
    <h4 @click="모달창열렸니 = true; 누른거 = i">{{ 원룸들[i].title }}</h4> @click == v-on:click
    <p>{{ 원룸들[i].price }}원</p>
  </div> -->
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
import Discount from './Discount.vue'; // 생성한 컴포넌트 사용하기 1) import 하기 2) components {}에 등록 3) <Discount/> 처럼 가져다가 사용하기
import Modal from './Modal.vue';
import Card from './Card.vue';

export default {
  name: 'App',
  data(){ // 데이터 보관하는 곳. 일반 변수 뿐만 아니라 HTML 속성도 데이터 바인딩 가능
    return {
      showDiscount : true,
      원룸들오리지널: [...data],
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
    },
    sortBack(){
      //this.원룸들 = this.원룸들오리지널; // 주의) 등호로 array를 집어넣으면 왼쪽 오른쪽 값 공유해주세요임
      this.원룸들 = [...this.원룸들오리지널]; // array/object 데이터의 각각 별개의 사본을 만들려면 [...array자료]
    },
    priceSort() {
      this.원룸들.sort(function(a,b){
        return a.price - b.price
      })
    }
  },
  mounted() { // 라이프사이클 부분 숙지하고 훅 부분 알아둬야 쓰기 가능할듯
    setTimeout(()=>{ //function이 아니라 arrow function 사용해야함. 장점은 밖깥의 this를 잘 가져다 쓸 수 있음. 함수 내부에서 this를 쓸일 있으면 arrow function 사용하기
      this.showDiscount = false;
    }, 2000);
  },
  components: {
    Discount : Discount, // 왼쪽이 위에서 import한 것, 또한 생략도 가능
    Modal : Modal,
    Card : Card,
  }
}
</script>

<style>
/* transition으로 애니메이션 주려면 아래 세개 다 만들어야 함. enter-from는 도입 애니메니션임. 퇴증 애니메이션은 -leave- */
.fade-enter-from { /* 시작 시 스타일 */
  opacity: 0;
}
.fade-enter-active { /* 애니메이션 */
  transition: all 1s;
}
.fade-enter-to { /* 끝날 시 스타일 */
  opacity: 1;
}
.fade-leave-from { /* 시작 시 스타일 */
  opacity: 1;
}
.fade-leave-active { /* 애니메이션 */
  transition: all 1s;
}
.fade-leave-to { /* 끝날 시 스타일 */
  opacity: 0;
}

.start {
  opacity: 0;
  transition: all 1s;
}
.end {
  opacity: 1;
}


body {
  margin: 0
}
div {
  box-sizing: border-box;
}
.discount {
  background: #eee;
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
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
