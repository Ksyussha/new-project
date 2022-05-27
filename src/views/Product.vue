<template>
  <div>
    <div v-if="fetching">Loading...</div>
    <div v-else-if="error">Oh no... {{ error }}</div>
    <div v-else>
      <div v-if="data">
        <div>
          <p>{{ data.products_by_id }}</p>
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
    const id = 4;
    const router = useRouter();
    const route = useRoute();
    const result = useQuery({
      query: `
        query {
          products_by_id(id: 4) {
            id
            title
            price

          }
        }
      `, variables: { id }
    });
    return {
      fetching: result.fetching,
      data: result.data,
      error: result.error,
    }
  },
};
</script>

<style>
</style>