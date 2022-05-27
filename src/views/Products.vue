<template>
  <div >
    <input type="text" class="search" v-model="search" placeholder="search"/>
    <!-- <button @click="searchProducts">search</button> -->
    <div v-if="fetching">Loading...</div>
    <div v-else-if="error">Oh no... {{ error }}</div>
    <div v-else>
      <div v-if="data">
        <div v-for="p in data.products" :key="p.id" @click="move(p.id)" class="product_card">
          <p>{{ p.title }}</p>
          <p>{{ p.price }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { useQuery } from "@urql/vue";
import { ref } from "@vue/reactivity";
import { useRouter, useRoute } from 'vue-router'

export default {
  setup() {
    const search = ref(null);
    const router = useRouter()
    const route = useRoute()
    const result = useQuery(
      {
        query: `
        query($search: String) {
          products(search: $search) {
            id
            title
            price
          
          }
        }
      `, variables: { search }
      },
    );
    function searchProducts() {
      result.executeQuery()
    }

    function move(id) {
      router.push("/products/" + id)
    }

    return {
      search,
      fetching: result.fetching,
      data: result.data,
      error: result.error,
      searchProducts,
      move
    };
  },
};
</script>

<style scoped>
.product_card {
  border: 3px black solid;
  margin: 1rem
}
.search {
  margin: 20px 0px 0px 0px;
    height: 24px;
    width: 249px;
    margin-right: 19px;
}

</style>