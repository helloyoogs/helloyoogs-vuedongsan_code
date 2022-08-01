<template>


  <div class="menu">
    <a v-for="a in 메뉴들" :key="a"> {{ a }} </a>
  </div>

  <Discount :amount="amount"/>

  <button @click="lowpriceSort">가격낮은순정렬</button>
  <button @click="toppriceSort">가격높은순정렬</button>
  <button @click="kpriceSort">상품명가나다순정렬</button>
  <button @click="sortBack">되돌리기</button>

  <transition name="fade">
  <Modal @closeModal="모달창열렸니 = false"
  :원룸들오리지널="원룸들오리지널"  :모달창열렸니="모달창열렸니" :누른거= "누른거"/>
  </transition>

<!-- <div v-for="(a,i) in 원룸들" :key="i">
  <img :src="a.image" class="room-img">
   <h4 @click="모달창열렸니 = true; 누른거 = i">{{ a.title }}</h4>
    <p>{{ a.price }}원</p>
    <button @click="신고수[i]++">허위매물신고</button> <span>신고수 : {{신고수[i]}}</span>
 </div> -->

<Card @openModal="모달창열렸니 = true; 누른거=$event"
 :원룸="원룸들[i]" v-for="(원룸,i) in 원룸들" :key="원룸"/>

</template>

<script>
import data from './assets/oneroom.js';
import Discount from './Discount.vue';
import Modal from './Modal.vue';
import Card from './Card.vue';

export default {
  name: 'App',
  data(){
    return{
      amount: 30,
      showDiscount : true,
      원룸들오리지널: [...data],
      누른거: 0, 
      원룸들 : data,
      모달창열렸니 : false,
      신고수 : [0, 0, 0, 0, 0, 0],
      메뉴들 : ['Home', 'Shop', 'About'],
      products : ['역삼동원룸', '천호동원룸', '마포구원룸'],
    }
  },
  methods : {
    increase(){
      this.신고수 += 1;
    },
    lowpriceSort(){
      this.원룸들.sort(function(a,b){
        return a.price - b.price
      })
    },
    toppriceSort(){
      this.원룸들.sort(function(a,b){
        return b.price - a.price
      })
    },
    kpriceSort(){
      this.원룸들.sort(function(a,b){
        return ( a.title < b.title ) ? -1 : ( a.title == b.title ) ? 0 : 1; 
      })
    },
    sortBack(){
      this.원룸들 = [...this.원룸들오리지널];
    }
  },

  mounted(){
    setInterval(() => {
      if(this.amount < 1){
        clearInterval();
      } else{
        this.amount -= 1;
      }
    }, 1000);
  },

  components: {
    Discount: Discount,
    Modal: Modal,
    Card : Card
}
}
</script>

<style>
.fade-leave-from{
  opacity: 1;
}
.fade-leave-active{
  transition: all 1s;
}
.fade-leave-to{
  opacity: 0;
}

.fade-enter-from{
  transform: translateY(-1000px);
}
.fade-enter-active{
  transition: all 1s;
}
.fade-enter-to{
  transform: translateY(0px);
}
body{
  margin: 0;
}
div{
  box-sizing: border-box;
}


.black-bg{
  width: 100%; height: 100%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed; padding: 20px;
  top: 0;
}
.white-bg{
  width: 100%; background: white;
  border-radius: 8px;
  padding: 20px;
}
.modalimg{
  width: 50%;
  margin-left: 25%;
}
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
  width: 50%;
  margin-top: 40px;
}

@media screen and (max-width: 800px){
  .room-img{
  width: 80%;
}
.modalimg{
  width: 100%;
  margin-left: 0;
}
}
</style>
