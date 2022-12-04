<template>
    <div class="black-bg" v-if="(modal==true)">
        <div class="white-bg">
            <img :src="products[productNumber].image" class="modal-img">
            <h4>{{products[productNumber].title}}</h4>
            <p>{{products[productNumber].content}}</p>
            <input v-model="month"> <!-- v-model 로 input 값을 쉽게 받을 수 있음 (기존 문법의 경우 @input = "month=e.target.value")-->
            <p> {{month}} 개월 선택 됨 : {{(products[productNumber].price*month)}} 원</p>
            <p @click="$emit('closeModal')" class="close-btn">닫기</p>
        </div>
    </div>
</template>


<!-- props 받아야함 -->
<script>
import { numberLiteralTypeAnnotation } from '@babel/types';

export default {
    name : 'Modal',
    data() {
        return{
            month:1,
        }
    },
    // watcher 로 데이터 인풋값을 감시 할 수 있음. => 데이터가 변할떄마다 함수 실행
    watch : {
        month(a,b) { // a == 변경 후 데이터, b == 변경 전 데이터
            if (isNaN(a)) {
                alert('숫자만 입력하세요');
                this.month = 1;
            }
        }
    },
    props : {
        products:Object,
        modal:Boolean,
        productNumber:Number
    }
}
</script>

<style>

</style>