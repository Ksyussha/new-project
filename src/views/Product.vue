<template>
  <div>
    <div v-if="fetching">Loading...</div>
    <div v-else-if="error">Oh no... {{ error }}</div>
    <div v-else>
      <div v-if="data">
        <div class="cont" style="width: 1465px; margin:0 auto; background-color: #dee6e8; padding-bottom: 10%;">
          <div class="h1"><h1>Product Page</h1> <a href="#" class="h1a">♡</a></div>
          <div class="product-card">
            <img :src="'http://38.242.229.113:8055/assets/' + data.products_by_id.image.id" alt="">
          <div class="card-text">
          <h2 class="title">{{ data.products_by_id.title }}</h2>
          <p class="description">{{ data.products_by_id.description }}</p>
          <div class="price-and-cart">
          <p class="price">{{ data.products_by_id.price }} $</p>
          <a href="#"><button class="card-text-button">add to cart</button></a>
          </div>
          </div></div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { useQuery } from "@urql/vue";
import { useRouter, useRoute } from 'vue-router'

export default {
  setup() {
    const router = useRouter();
    const route = useRoute();
    const id = +route.params.id;
    const result = useQuery({
      query: `
        query getProduct($id: ID!) {
          products_by_id(id: $id) {
            id
            title
            price
            spec
            description
            image {
              id
            }
          }
        }
      `, variables: { id }
    });
    return {
      fetching: result.fetching,
      data: result.data,
      error: result.error,
      route
    }
  },
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Varela+Round&display=swap');
.h1 {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 52px 50px 0px 50px;
  color: black;
}
.h1a {
  font-size: 24px;
  color: black;
  text-decoration: none;
}
.product-card {
  display: flex;
  padding: 30px 50px;
  background-color: white;
}
.product-card img {
  width: 400px;
  margin-right: 50px;
  border: 1px solid #2c5592;
      padding: 30px 0px;
}
.price {
  font-size: 33px;
  font-weight: 700;
  color: #2c5592;
  margin-right: 15px;
}
.title {
  font-size: 28px;
  font-weight: 700;
  margin-bottom: 32px;
}
.card-text-button {
  padding: 10px 20px;
  border: #ffffff solid 1px;
  background-color: #2c5592;
  border-radius: 4%;
  color: #f6f6f2;
  font-weight: 700;
  opacity: 0.8;
  cursor: pointer;
}
.price-and-cart {
  display: flex;
  align-items: center;
  margin: 20px 0px;
  justify-content: space-between;
}
.card-text-button:hover {
  background-color: #f6f6f2;
  color: #2c5592;
  border: 1px solid #2c5592;
}
.description{
  color: black;
  line-height: 1.6;
  font-size: 20.5px;
}
</style>