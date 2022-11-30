<template>
  <div class="menu">
    <a v-for="menu in menus" :key="menu">{{menu}}</a>
  </div>

  <div v-for="(product,index) in products" :key="index" class = 'card'>
    <h4>{{product.product}}</h4>
    <p>{{product.price}}만원</p>
    <button v-on:click="increase(index)" class="red-btn">허위매물신고</button> <span>신고수 : {{reportNum[index]}}</span>
  </div>

</template>

<script>


export default {
  name: 'App',
  data() {
    return {
      menus : ['Home','Products','About'],
      products : [{product : '역삼동원룸', price: 60, id : 0}, {product : '천호동원룸', price : 40, id : 1}, {product : '마포구원룸', price : 70, id :2}],
      reportNum : [0,0,0]
    }
  },  // data 보관함 ( 데이터 다 떄려 박기 ) vue 실시간 자동 렌더링을 위해 데이터 바인딩이 필요
  methods: {
    increase(index) {
      this.reportNum[index]++
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

.menu {
  background: darkorchid;
  padding:15px;
  border-radius: 5px;
}

.menu a{
  color : white;
  padding : 10px;
}

.red-btn {
  color : white;
  background-color: darkred;
  border-radius: 5px;
  border : 0px;
  height : 40px;
  width : 130px
}
</style>
