<template>
  <div class="black-bg" v-if="모달창열렸니 == true">
    <div class="white-bg">
      <img :src="원룸들[누른거].image" style="width:100%">
      <h4>{{ 원룸들[누른거].title }}</h4> <!-- 참고로 데이터 바인딩은 아래에 있는 데이터만 사용 가능 -->
      <p>{{ 원룸들[누른거].content }}</p>
      <!-- <input @input="month = $event.target.value"> @input: 입력이 들어올 때 마다 실행, @change: 입력 후 커서를 다른데 찍으면 실행, $event.target.value는 input에 입력한 값임(js 문법) -->
      <input v-model.number="month"> <!-- 바로 위와 같은 기능. 아래 선언한 month 변수에 값을 저장. .number는 선택 사항이지만 저장할 데이터 타입 명시 효과 -->
      <p> {{ month }}개월 선택함 : {{ 원룸들[누른거].price * month}} 원</p>
      <botton @click="$emit('closeMoal')">닫기</botton>
    </div>
  </div>
</template>

<script>
export default {
    name : 'Modal',
    data() {
      return {
        month : 1, // 문자 입력 받을거면 초기값을 문자로 하셈
      }
    },
    watch : { // 데이터를 감시하기 위해서는 watcher를 사용
      month(a) { // 감시할 데이터명() -> method 생성, a는 변경 후 month 데이터임, a의 뒤에 오는 인자는 변경 전 month 데이터 
        // 사용자가 month를 글자로 입력하면 경고문
        if (a >= 13) {
          alert('13이상 입력하지 마셈')
        }
      },
    },
    props : { // props는 read-only여서, 받아온 거 수정하면 큰일남
      원룸들 : Array,
      누른거 : Number,
      모달창열렸니 : Boolean,
    }
}
</script>

<style>

</style>