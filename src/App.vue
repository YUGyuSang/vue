<template>

  <div class="black-bg" v-if="modalstate == true">
    <div class="white-bg">
      <h4>상세페이지임</h4>
      <p>상세페이지 내용임</p>
       <button @click="modalstate = false">닫기</button>
    </div>
  </div> 

  <div class="menu">
    <a v-for="(a,i) in menus" :key="i">{{a}}</a>
  </div>

  <div v-for="(product,i) in products" :key='i'>
    <img :src="oneroom[i].image" alt="" class="room-img">
    <h4 @click="modalstate = true">{{oneroom[i].title}}</h4>
    <p>{{oneroom[i].price}}만원</p>
    <button @click="increase(i)">허위매물신고</button> <span>신고수 : {{tlsrhtn[i]}}</span>
  </div>

  <h1>메서드 핸들러 인라인 핸들러</h1>
  <button @click="count++">카운트 버튼</button>
  <h1>{{count}}</h1>
  <button @click="changeName()">메서드 핸들러</button>
  <h1>{{name}}</h1>


  <h1>캐싱 기능</h1>
  <h1>{{text}}</h1>
  <h1>changeText 함수 호출 값:{{changeText()}}</h1>
  <h1>changeText 함수 호출 값:{{changeText()}}</h1>
  <h1>changeText 함수 호출 값:{{changeText()}}</h1>

  <h2>{{computedText}}</h2>
  <h2>{{computedText}}</h2>
  <h2>{{computedText}}</h2>

  <h1>Watch 기능 테스트</h1>
  <button @click="changeMessage()">{{message}}</button>
  {{watchMessage}}

  <h1>Props Emits</h1>
  <div>
    <!-- <ChildComponent v-bind:sendProps1="title" v-bind:sendProps2="createAt" :sendProps3="obj" /> -->
    <ChildComponent @send-event="parentEvent" :sendProps1="title" :sendProps2="createAt" :sendProps3="obj"/>
  </div>

  <h1>v-model</h1>
  <div>
    <input type="text" v-model="inputValue1">
    <span>즉각적으로 변함</span>
    <input type="text" :value="inputValue2" @input="inputValue2 = $event.target.value" />
  </div>
  <div>
    {{inputValue1}}
    {{inputValue2}}
  </div>

  <!-- <div>
    <h4>{{products[0]}}</h4>
    <p>50만원</p>
    <button @click="increase">허위매물신고</button> <span>신고수 : {{tlsrhtn}}</span>
  </div>
  <div>
    <h4>{{products[1]}}</h4>
    <p>가격은아무거나</p>
  </div>
    <div>
    <h4>{{products[2]}}</h4>
    <p>가격은아무거나</p>
  </div> -->


</template>

<script>

import data from './assets/oneroom.js'
import ChildComponent from './components/ChildComponent.vue'

// interface obj{
//   id:number,
//   name:string
// }

// const title = ref<string>('부모컴포넌트에서 선언된 데이터입니다.')
// const createAt = ref<number>(2024)
// const Object = reactive<obj>({
//   id: 2024,
//   name: 'yu'
// })

export default {
  components:{
    ChildComponent,
  },
  data(){
    return {
      oneroom : data,
      modalstate : false,
      tlsrhtn: [0,0,0],
      prices: [50, 45, 60],
      menus : ['home','shop','about'],
      products: ['역삼동원룸','천호동원룸','강남원룸'],
      name: 'Vue.js',
      count: 0,
      text:"coumputed 테스트 데이터 문구입니다.",
      message:'안녕하세요, vue.js watch 기능입니다.',
      watchMessage:'',
      title:'부모컴포넌트에서 선언된 데이터입니다.',
      createAt: 2024,
      obj:{
        id:2024,
        name:'yu'
      },
      inputValue1: '',
      inputValue2: '',
    }
  },
  // methods 부분에 선언된 함수와 동일한 로직일 때
  // 캐싱 기능이 없는 methods 호출될 때마다 console 값이 출력이 되었습니다.
  // 반면에, computed는 캐싱 기능이 있기 때문에 methods와 어떤 차이점이 있는지
  // 한 번 주의깊게 살펴보는 것이 포인트 입니다.
  computed: {
    computedText(){ // 함수 모형이지만 리턴이 있는 데이터이다
      console.log("computed 기능을 생성하였습니다.")
      return this.text.split("").reverse().join('')
    }
  },
  watch: { //변경 되면 그 함수가 실행이 되는 watch이다.
    // message: function(){}
    // 데이터 뿐만 아니라 computed로 계산된 형태의 데이터도 watch로 감지 할 수 있다.
    // 보통 게시판에서 한 컬럼을 선택하였을 때, 고유한 id 값이 바뀜을 감지하고
    // 이때, 그 id 값에 따른 상세 데이터를 호출할 때, 주로 사용한다.
    message() {
      //window.alert("message 변수에 담긴 데이터가 변경되었습니다.")
      this.watchMessage = "watch 동작"
    },
    id(){
      //해당 상세데이터를 조회하는 api호출
    }
  },
  methods : {
    increase(index){
      this.tlsrhtn[index] +=1;
    },
    changeName() {
      this.name = '변경된 텍스트 데이터 입니다'
    },
    changeText() {
      console.log("함수 호출");
      console.log(this.text);

      return this.text.split("").reverse().join('')
    },
    changeMessage() {
      console.log('M 함수 호출!');
      this.message = '변경된 message 데이터입니다.'
    },
    parentEvent(e){
      console.log(e);
    }
  },
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
.menu{
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}
.menu a{
  color: white;
  padding: 10px;
}
.room-img{
  margin-top: 40px;
  width: 100%;
}
body{
  margin: 0;
}
div{
  box-sizing: border-box;
}
.black-bg{
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed;
  padding: 20px;
}
.white-bg{
  width: 100%;
  background: white;
  border-radius: 6px;
  padding: 20px;
}
</style>
