<template>
  <div class="holder">
    <form class="container" @submit.prevent="signup">
      <input type="email" id="email" v-model="email" placeholder="Your email" required />
      <input type="password" id="password" v-model="password" placeholder="Your password" required />
      <button  class="call_to_action" type="submit">log in</button>
    </form>
    <span>Or</span>
    <button>
      <span>Log in with google</span>
    </button>

  </div>
</template>

<script setup>
import { ref } from 'vue'
import config from '../config';
import { useUserStore } from '../stores/counter.js';
import { useRouter } from 'vue-router';

const router = useRouter();

const apiUrl = `${config.baseUrl}/customers/log_in`;

const email = ref('');
const password = ref('');

const signup = async () => {
  try {
    const response = await fetch(apiUrl, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify({
        email: email.value,
        password: password.value,
      }),
    });
    if (response.ok) {
      const responseData = await response.json();

      useUserStore().setUser( responseData.user);
      useUserStore().setTokens(responseData.token); 
      useUserStore().setAuth()
      router.push('/order');
    } else {
      console.error('Failed to fetch authentication token:', response.statusText);
      // Handle the failure scenario, e.g., display an error message
    }
  } catch (error) {
    console.error('Error signing up:', error);
  }
};
</script>

<style scoped>
.holder{
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
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
button{
    background-color: white;
    color: black;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 50px;
    border-radius: 20px;
}
</style>