<template>

  <Transition name="fade">
    <Modal :products="products" :modal="modal" :productNumber="productNumber" @closeModal="(modal=false)"/> <!--props 전송 v-bind -->
  </Transition>


  <div class="menu">
    <a v-for="menu in menus" :key="menu">{{menu}}</a>
  </div>


  <Discount></Discount>

  <button @click="titleSort" class="tap-button">ABC 🔽</button>
  <button @click="priceSortDown" class="tap-button"> 가격 🔽 </button>
  <button @click="priceSortUp" class="tap-button"> 가격 🔼 </button>
  <button @click="sortBack" class="tap-button"> 되돌리기 </button>

  <Card @openModal="(modal=true, productNumber = $event)" v-for="(product,index) in products" :key="index" :product="product" :productNumber="productNumber" :modal="modal" />


</template>

<script>
import productsData from './assets/data.js';
import Discount from './Discount.vue';
import Modal from './Modal.vue';
import Card from './Card.vue';

export default {
  name: 'App',
  data() {
    return {  // data 보관함 ( 데이터 다 떄려 박기 ) vue 실시간 자동 렌더링을 위해 데이터 바인딩이 필요
      menus : ['Home','Products','About'],
      products : productsData,
      productsOriginal : [...productsData],
      productNumber : 0,
      reportNum : [0,0,0],
      modal : false
    }
  }, 
  methods: { // 함수 보관함
    increase(index) {
      this.reportNum[index]++
    },
    sortBack(){
      this.products = [...this.productsOriginal]
    },
    priceSortUp(){
      let array = [...this.products]
      array.sort(function(a,b){
        return a.price-b.price
      }) // sort() : 원형변경 // map(), filter() : 원형보존
      this.products = array
    },
    priceSortDown(){
      let array2 = [...this.products]
      array2.sort(function(a,b){
        return b.price-a.price
      })
      this.products = array2
    },
    titleSort(){
      let array3 = [...this.products]
      array3.sort(function(a,b){
        const titleA = a.title[0]
        const titleB = b.title[0]
        if (titleA<titleB) {
          return -1;
        } else if (titleA>titleB) {
          return 1;
        } else {
          return 0 ;
        }
      })
      this.products = array3
    }
  },
  components: { // components 보관함
    Discount : Discount,
    Modal : Modal,
    Card:Card
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

body {
  margin : 0;
}
div {
  box-sizing: border-box;
}
.black-bg {
  width: 100%; 
  height:100%;
  background: rgba(0,0,0,0.5);
  position: fixed; 
  padding-top: 70px;
  padding-left: auto;
  padding-right: auto;
}
.white-bg {
  width: 700px;
  height : 550px;
  background: white;
  margin-left: auto;
  margin-right: auto;
  border-radius: 8px;
  padding: 20px;
}

.modal-img {
  width: 600px;
}

.menu {
  background: darkorchid;
  padding:15px;
}

.menu a{
  color : white;
  padding : 10px;
  cursor: pointer;
}

.red-btn {
  color : white;
  background-color: darkred;
  border-radius: 5px;
  border : 0px;
  height : 40px;
  width : 130px;
  cursor: pointer;
}

.room-img {
  margin-top : 40px;
  width : 40%;
}

.cursor-point{
  cursor: pointer;
}

.close-btn {
  background-color: #2c3e50;
  width : 30%;
  margin-left: auto;
  margin-right: auto;
  height : 30px;
  line-height: 30px;
  text-align: center;
  border-radius: 5px;
  color:white;
  cursor: pointer;
}
.card {
  border: 1rem solid;
  border-color: white;
  background-color: whitesmoke;
  border-radius: 5px;
}

.fade-enter-from{
  opacity: 0;
}   /* animation 시작 */
.fade-enter-active{
  transition: all 0.5s;
}   /* animation transition 입력 */
.fade-enter-to{
  opacity: 1;
}   /* animation 끝 */

.tap-button{
  margin-right: 10px;
  padding : 5px;
  color: white;
  background-color: #2c3e50;
  border: solid 3px #2c3e50 ;
  border-radius: 5px;
  cursor: pointer;
}

/* 퇴장 animation 은 enter => leave로 변경 */
</style>
