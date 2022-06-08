<template>
  <div>
    <div class="menu">
      <div style="display: flex;align-items: baseline;font-size: 49.5px;font-weight: 600;color: rgb(0 0 0);font-weight: initial;">
      <h1 class="pine">pine</h1><h1>Apple</h1></div>
    <div class="menuu"><RouterLink to="/">Home</RouterLink> <p style="color:#2c5592">|</p>
    <RouterLink to="/products">Products</RouterLink>
    </div></div>
    <RouterView />
    
  </div>
</template>

<script>
import { createClient, provideClient } from '@urql/vue';
export default {
  setup() {
    const client = createClient({
      url: "http://38.242.229.113:8055/graphql",
      fetchOptions: () => {
      const auth = 1
      const token = auth === 0 ? localStorage.getItem('token') : null
      return {
        headers: { authorization: token ? `Bearer ${token}` : '' }
      };
    },
    });

    provideClient(client);
  }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Varela+Round&display=swap');
.menu{ 
    background-color: #f6f6f6;;
    height: 0px;
    padding-top: 25px;
    display: flex;
    align-items: center;
    justify-content: space-around;
    /* box-shadow: rgb(44 85 146) 0px 19px 38px -29px inset; */
}
.menu h1{ 
      font-weight: initial;
      font-size: unset;
}
.menuu{ 
  display: flex;
  justify-content: flex-end;
  align-items: center;
}
a{
text-decoration: none;
color: #000000;
padding: 0px 10px 0px 10px;
font-size: unset;
text-transform: uppercase;
font-weight: bold;
}
.pine {
  color: #aac6de;
}
</style>