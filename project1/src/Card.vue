<template> 
    <div>
        <img :src="원룸.image" class="room-img">
        <h4 @click="send">{{ 원룸.title }}</h4> <!-- 자식이 부모 데이터 수정하려면 custom event 문법 사용(부모에게 메세지를 보내는 기능) 사용해야 함. 그리고 부모는 메세지를 받기를 해야함. App.vue 참고. @click="$emit('작명', 데이터)" 형식으로 보냄. 내용이 길면 함수화 해도 됌 -->
        <p>{{ 원룸.price }}원</p>
    </div>
</template>

<script>
export default {
    props : {
        원룸 : Object,
    },
    methods : {
        send(){
            this.$emit('openModal', this.원룸.id)
        }
    }
}
</script>

<style>

</style>