<template>
  <div>
    <div class="cont" style="width: 1465px; margin:0 auto; background-color: #dee6e8; padding-bottom: 10%;">
    <div class="backgroundin" >
    <div class="background">
      <div class="h1"><h1>Products</h1></div>
      </div>
  </div>

    <div class="flx">
      <input type="text" v-model="search" placeholder="search..." />
    </div>
    <div v-if="fetching">Loading...</div>
    <div v-else-if="error">Oh no... {{ error }}</div>
    <div v-else>
      <div v-if="data">
        <div class="flex">
          <div
            v-for="p in data.products"
            :key="p.id"
            @click="move(p.id)"
            class="product_card"
          >
            <img
              :src="
                'http://38.242.229.113:8055/assets/' +
                p.image.id +
                '?width=210&height=218&fit=cover'
              "
              alt=""
            />
            <p>{{ p.title }}</p>
            <div class="forPrice">
              <p style="color:#aac6de; font-weight: bold;">PRICE:</p>
              <p style="color: #2c5592; font-weight: bold; font-size: 21.5px;">{{ p.price }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
    </div>
  </div>
</template>

<script>
import { useQuery } from "@urql/vue";
import { ref } from "@vue/reactivity";
import { useRouter, useRoute } from "vue-router";

export default {
  setup() {
    const search = ref(null);
    const router = useRouter();
    const route = useRoute();
    const result = useQuery({
      query: `
        query($search: String) {
          products(search: $search) {
            id
            title
            price
            spec
            image {
              id
            }
          }
        }
      `,
      variables: { search },
    });
    function searchProducts() {
      result.executeQuery();
    }

    function move(id) {
      router.push("/products/" + id);
    }

    return {
      search,
      fetching: result.fetching,
      data: result.data,
      error: result.error,
      searchProducts,
      move,
    };
  },
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Varela+Round&display=swap');
.backgroundin{ 
  background-color: #ffffff;
  padding: 10px 0px 0px 0px; 
  height: 600px;
  display: flex;
  justify-content: flex-start;
  align-items: flex-end;

}
.background {
  background-image: url(https://www.apple.com/v/iphone/home/bd/images/overview/hero/iphone_13_pro__en2q051lfus2_large.jpg);
  width: 819px;
  background-size: 819px 515px;
  background-repeat: no-repeat;
  position: relative;
  left: 50%;
  margin-left: -409.5px;
}
.h1 {
  height: 548px;
  display: flex;
  justify-content: center;
  align-items: flex-end;
  margin-top: 35px;
  
}
.h1 h1 {
  color: #2c5592;
  font-size: -webkit-xxx-large;
  text-transform: uppercase;
  margin: 0px;
}
h1 {
  color: #2f313d;
}
.product_card {
  width: 266px;
  border: 1px solid #ffffff00;
  border-radius: 6px;
  margin: 56px 35px 0px 35px;
  padding: 25px 11px 5px 15px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-evenly;
  transition: all .2s ease-in-out;
  background-color: #f6f6f6;
}
.product_card:hover{ 
  	transform: scale(1.1); 
    cursor: pointer;
}

.flex {
  display: flex;
  flex-wrap: wrap;
  align-items: stretch;
}
input {
  margin: 20px 0px 0px 0px;
  height: 24px;
  width: 249px;
  margin-right: 19px;
  border-color: #aac6de;
  border-radius: 7px;
}
input[type="text"]::-webkit-input-placeholder {
    color: #2c5592;
   } 
.flx {
  display: flex;
  justify-content: flex-end;
}
.forPrice {
  display: flex;
  align-items: baseline;
}

</style>