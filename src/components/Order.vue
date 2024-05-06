<template>

    <div class="order">
        <div class="image">
            <img src="@/assets/images/deliver.jpg" alt="">
        </div>
        <div class="details">
            <span>{{order.item}}</span>
            <span>{{order.amount}}</span>
            <span>{{order.time}}</span>
        </div>
    </div>
</template>

<script setup>
defineProps({
    order: Object
})
</script>

<style scoped>
.order{
    display: flex;
    height: auto;
    width: 100%;
    background-color: white;
}
.image{
    padding: 2%;
    width: 40%;
}
.image img {
    display: block;
    width: 100%;
    height: 96%;
    border-radius: 20px;
}
.details{
    padding: 4%;
    display: flex;
    flex-direction: column;
    color: black;
}
</style>