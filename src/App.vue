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

export default {
  name: 'App',
  data(){
    return {
      oneroom : data,
      modalstate : false,
      tlsrhtn: [0,0,0],
      prices: [50, 45, 60],
      menus : ['home','shop','about'],
      products: ['역삼동원룸','천호동원룸','강남원룸']
    }
  },
  methods : {
    increase(index){
      this.tlsrhtn[index] +=1;
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
