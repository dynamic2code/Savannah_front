<template>
    <div class="holder">
        <div class="container">
        <div>
            <span>Savannah</span>
        </div>

        <div>
            <button id="open" @click="openPortal">
            <img src="@/assets/images/add.png" alt="">
            </button>                
        </div>

        </div>
        <div v-if="isPortalOpen" id="add_portal">
            <div>
                <button id="close" @click="closePortal">
                <img src="@/assets/images/close.png" alt="">
                </button>
            </div>
            <div>
                <AddOrder/>
            </div>
        </div>
    </div>
</template>

<script setup>
import AddOrder from '@/components/AddOrder.vue'
import { ref } from 'vue';

const isPortalOpen = ref(false);

const openPortal = () => {
    isPortalOpen.value = true;
};

const closePortal = () => {
    isPortalOpen.value = false;
};
</script>

<style scoped>
.holder{
    width: 100%;
    /* background-color: blueviolet; */
    /* height: auto; */
    flex-direction: column;
    justify-content: center;
    align-items: center;
}
.container{
  justify-content: space-between;
  align-items: center;
  height: 70px;
  /* background-color: aqua; */
}
button{
    background-color: white;
}
#add_portal{
    position: fixed;
    display: flex;
    flex-direction: column;
    top: 0;
    width: 100vw;
    height: 100vh;
    background-color: #181818;
}

</style>