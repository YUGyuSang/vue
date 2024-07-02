<template>
    <div>{{sendProps1}}</div>
    <div>{{sendProps2}}</div>
    <div>{{sendProps3.id}}</div>
    <div>{{sendProps3.name}}</div>

    <button @click="sendEvent">자식컴포넌트에서 만든 버튼</button>
</template>

<script>
export default {
    props: {
        sendProps1 : String,
        sendProps2 : Number,
        sendProps3 : Object
    },
    data(){
        return{
            text:'자식컴포넌트에서 선언된 데이터입니다.'
        }
    },
    methods: {
        sendEvent(){
            this.$emit('send-event',this.text)
        }
    },
}
//1. 컴포지션API에서 타입스크립트를 활용하는 방법
//1-1 Prop 받은 데이터 형식에 맞게 타입을 지정해준다.

// Prop 받은 데이터 이름 자체에 미리 선언해둔 타입을 설정해준다.
// defineProps toRefs 내장함수를 통해 Prop 받은 데이터를 활용하여 템플릿 부분에 호출하여 사용한다.
</script>

<style lang="scss" scoped>

</style>