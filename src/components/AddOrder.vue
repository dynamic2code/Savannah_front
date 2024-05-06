<template>
    <div id="form_holder" >
        <form class="container" @submit.prevent="addOrder">
            <input type="text" id="item" v-model="item" placeholder="Your Item name" required />
            <input type="number" id="amount" v-model="amount" placeholder="The amount" required />
            <button  class="call_to_action" type="submit">Add order</button>
        </form>
    </div>
</template>

<script setup>
import { ref } from 'vue'
import config from '../config';
import { useUserStore } from '../stores/counter.js';
import router from '@/router';

const apiUrl = `${config.baseUrl}/orders`;
const userStore = useUserStore();
const token = userStore.token;
console.log(token);
const item = ref('');
const amount = ref('');
const customerId = useUserStore().user.user_id

const addOrder = async () => {
  try {
    const response = await fetch(apiUrl, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        'Authorization': `Bearer ${token}`,
      },
      body: JSON.stringify({
        item: item.value,
        amount: amount.value,
        customer_id: customerId,
      }),
    });
    if (response.ok) {
      router.push('/order');
    } else {
      console.error('Failed to fetch authentication token:', response.statusText);
    }
  } catch (error) {
    console.error('Error signing up:', error);
  }
};
</script>

<style scoped>
form{

  display: flex;
  flex-direction: column;
}
.icon{
  font-size: 1.5rem;
  display: flex;
  justify-content: center;
  margin-bottom: 3%;
  align-items: center;
}
.direction{
  font-size: 1.2rem;
  display: flex;
  justify-content: center;
  margin-bottom: 3%;
  align-items: center;
}
input{
  all: unset;
  width: 90%;
  height: 50px;
  margin: 2%;
  padding-left: 3%;
  /* background-color: aliceblue; */
  border-radius: 10px;
  border: 1px solid #000;
}
#form_holder{
    display: flex;
    justify-content: center;
    align-self: center;
    height: 80%;
    width: 100%;
}
button{
    background-color: white;
    color: black;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 70px;
    border-radius: 20px;
}
</style>