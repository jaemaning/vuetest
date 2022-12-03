<template>
    <div class='card'>
        <img :src="product.image" class="room-img" @click="modal=true; productNumber = product.id">
        <h4 @click="(modal=true)">{{product.title}}</h4>
        <p @click="(modal=true)">{{product.price}}원</p>
        <!-- <button v-on:click="increase(index)" class="red-btn">허위매물신고</button> <span>신고수 : {{reportNum[index]}}</span> -->
    </div>
</template>

<script>
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