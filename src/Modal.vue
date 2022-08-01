<template>
  <div class="black-bg" v-if="모달창열렸니 == true">
  <div class="white-bg">
    <h4 class="modalimg"><img :src="원룸들오리지널[누른거].image" style="width:100%"></h4>
    <h4>{{ 원룸들오리지널[누른거].title }}</h4>
    <h4>{{ 원룸들오리지널[누른거].content }}</h4>
    <input v-model.number="month">
    <p> {{ month }}개월 선택함 : {{ 원룸들오리지널[누른거].price *month}}원</p>
    <button @click="close">닫기</button>
  </div>
</div>
</template>

<script>
export default {
    name : 'Modal',
    data(){
      return{
        month : 1,
      }
    },
    watch : {
      month(a){
        if(a >= 13){
          alert('13이상 입력하지 마셈');
           this.month = 1;
        } else if(isNaN(a) == true){
        alert('문자입력하지마라');
          this.month = 1;
        } 
      },
    },
    props : {
        원룸들오리지널 : Array,
        누른거 : Number,
        모달창열렸니 : Boolean
    },
    methods : {
      close(){
        this.$emit('closeModal', this.원룸들)
      }
    },
     beforeUpdate(){
    if (this.month == 2){
      alert('2개월은 너무 적음.. 안팝니다')
      this.month = 3
    }
 }
}
</script>

<style>

</style>