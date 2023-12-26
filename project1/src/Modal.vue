<template>
  <div class="black-bg" v-if="모달창열렸니 == true">
    <div class="white-bg">
      <img :src="원룸들[누른거].image" style="width:100%">
      <h4>{{ 원룸들[누른거].title }}</h4> <!-- 참고로 데이터 바인딩은 아래에 있는 데이터만 사용 가능 -->
      <p>{{ 원룸들[누른거].content }}</p>
      <p>{{ 원룸들[누른거].price }} 원</p>
      <!-- <botton @click="모달창열렸니 = false">닫기</botton> -->
    </div>
  </div>
</template>

<script>
export default {
    name : 'Modal',
    props : { // props는 read-only여서, 받아온 거 수정하면 큰일남
      원룸들 : Array,
      누른거 : Number,
      모달창열렸니 : Boolean,
    }
}
</script>

<style>

</style>