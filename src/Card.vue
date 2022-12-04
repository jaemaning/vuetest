<template>
    <div class='card cursor-point' @click="$emit('openModal', product.id)">
        <img :src="product.image" class="room-img">
        <h4>{{product.title}}</h4>
        <p>{{product.price}}원</p>
        <!-- <button v-on:click="increase(index)" class="red-btn">허위매물신고</button> <span>신고수 : {{reportNum[index]}}</span> -->
    </div>
</template>

<script>
// props 로 보낸 데이터는 read-only 수정 불가. app.vue 데이터 수정하고 싶으면 custom event 해야함 - $emit
export default {
    name : 'Card',
    props : {
        product : Object,
        productNumber : Number,
        modal : Boolean
    }
}
</script>

<style>

</style>