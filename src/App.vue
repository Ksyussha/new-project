<template>
  <div>
    <div class="menu">
      <div style="display:flex; width: 981px; align-items: baseline; font-size: 49.5px; font-weight: 600; color: #2c5592;">
      <p class="pine">pine</p>Apple</div>
    <div class="menuu"><RouterLink to="/">Home</RouterLink> <p style="color:#2c5592">|</p>
    <RouterLink to="/products">Products</RouterLink>
    </div></div>
    <RouterView />
    
  </div>
</template>

<script>
export default {
  setup() {

  }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Varela+Round&display=swap');
.menu{ 
  background-color: #dee6e8;
  height: 66px;
  display: flex;
  justify-content: flex-end;
  align-items: center;
  box-shadow: rgb(44 85 146) 0px 19px 38px -29px inset;
  
}
.menu h1{ 
  color: #2c5592;
}
.menuu{ 
  display: flex;
  justify-content: flex-end;
  align-items: center;
}
a{
  text-decoration: none;
  color:#2c5592;
  padding: 0px 10px 0px 10px;
  font-size: unset;
  text-transform: uppercase;
  font-weight: bold;
}
.pine {
  color: #aac6de;
}
</style>