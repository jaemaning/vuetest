<template>

  <Transition name="fade">
    <Modal :products="products" :modal="modal" :productNumber="productNumber" @closeModal="(modal=false)"/> <!--props μ μ‘ v-bind -->
  </Transition>


  <div class="menu">
    <a v-for="menu in menus" :key="menu">{{menu}}</a>
  </div>


  <Discount v-if="showDiscount" />

  <button @click="titleSort" class="tap-button">ABC π½</button>
  <button @click="priceSortDown" class="tap-button"> κ°κ²© π½ </button>
  <button @click="priceSortUp" class="tap-button"> κ°κ²© πΌ </button>
  <button @click="sortBack" class="tap-button"> λλλ¦¬κΈ° </button>

  <Card @openModal="(modal=true, productNumber = $event)" v-for="(product,index) in products" :key="index" :product="product" :modal="modal" />


</template>

<script>
import productsData from './assets/data.js';
import Discount from './Discount.vue';
import Modal from './Modal.vue';
import Card from './Card.vue';

export default {
  name: 'App',
  data() {
    return {  // data λ³΄κ΄ν¨ ( λ°μ΄ν° λ€ λλ € λ°κΈ° ) vue μ€μκ° μλ λ λλ§μ μν΄ λ°μ΄ν° λ°μΈλ©μ΄ νμ
      menus : ['Home','Products','About'],
      products : productsData,
      productsOriginal : [...productsData],
      productNumber : 0,
      reportNum : [0,0,0],
      modal : false,
      showDiscount : true
    }
  }, 
  methods: { // ν¨μ λ³΄κ΄ν¨
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
      }) // sort() : μνλ³κ²½ // map(), filter() : μνλ³΄μ‘΄
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
  mounted(){ // life cycle hook μ€μ mounted : λ§μ΄νΈ λ λ μ€ν
    setTimeout(()=>{ // thisλ₯Ό μ¬μ©ν λ arrow(=>) functionμ μ¬μ©μ©
      this.showDiscount = false;
    },2000);
  },
  components: { // components λ³΄κ΄ν¨
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
}   /* animation μμ */
.fade-enter-active{
  transition: all 0.5s;
}   /* animation transition μλ ₯ */
.fade-enter-to{
  opacity: 1;
}   /* animation λ */

.tap-button{
  margin-right: 10px;
  padding : 5px;
  color: white;
  background-color: #2c3e50;
  border: solid 3px #2c3e50 ;
  border-radius: 5px;
  cursor: pointer;
  margin-top : 10px;
}

/* ν΄μ₯ animation μ enter => leaveλ‘ λ³κ²½ */
</style>
