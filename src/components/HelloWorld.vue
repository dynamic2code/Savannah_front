<script setup>

</script>

<template>
  <div class="holder">
    <div class="container">
      <div>
        <span>Savannah</span>
      </div>
      <div id="link_holder">
        <RouterLink class="button" to="/log_in">
          <span>log in</span>
        </RouterLink>

        <RouterLink class="button" to="/sign_up">
          <span>sign up</span>
        </RouterLink>        
      </div>


    </div>
  </div>
</template>

<style scoped>
.container{
  justify-content: space-between;
  align-items: center;
  height: 70px;
  /* background-color: aqua; */
}
#link_holder{
  display: flex;
  padding: 2%;
  height: 100%;
  /* background-color: blue; */
}
.button{
  height: 70%;
}
</style>
