<template>
    <div class="black-bg" v-if="(modal==true)">
        <div class="white-bg">
            <img :src="products[productNumber].image" class="modal-img">
            <h4>{{products[productNumber].title}}</h4>
            <p>{{products[productNumber].content}}</p>
            <p>{{products[productNumber].price}} 원</p><br/>
            <p @click="(modal=false)" class="close-btn">닫기</p>
        </div>
    </div>
</template>


<!-- props 받아야함 -->
<script>
import { numberLiteralTypeAnnotation } from '@babel/types';

export default {
    name : 'Modal',
    props : {
        products:Object,
        modal:Boolean,
        productNumber:Number
    } 
}
</script>

<style>

</style>