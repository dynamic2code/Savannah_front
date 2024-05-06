<template>
    <Header></Header>  
    <div class="holder">
  
        <div class="container">
            <Order/>
            <!-- <Order v-for="order in orders"  :order="order"></Order> -->
        </div>
    </div>
</template>
<script setup>
import Header from '@/components/Header.vue'
import Order from '@/components/Order.vue'
import { ref, onMounted } from 'vue'
import config from '../config';

const apiUrl = `${config.baseUrl}/orders`;


const orders = ref([])

const fetchOrders = async () => {
  try {
    const response = await fetch(apiUrl, {
      headers: {
        'Content-Type': 'application/json',
      },
    });
    if (response.ok) {
      const responseData = await response.json();

      // Check if the 'data' property exists in the response
      if ('data' in responseData) {
        const { data } = responseData;

        // Update the spots ref with the processed spot data
        orders.value = data;

      } else {
        console.error('Invalid API response: Missing "data" property');
      }
    } else {
      console.error('Request failed:', response.statusText);
    }
  } catch (error) {
    // ... error handling
  }
};

// console.log(products);

onMounted(() => {
    fetchOrders();
});
</script>

<style scoped> 
</style>