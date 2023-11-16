<template>
  <section class="admin">
    <div class="titles">
      <h1>
        <a class="title" href="#">Products</a>
      </h1>
      <h1>
        <a class="title" href="#">Categories</a>
      </h1>
      <h1>
        <a class="title" href="#">Users</a>
      </h1>
    </div>
    <div class="product-grid">
      <div class="product-grid-name">
        <p class="cat">Name</p>
        <p class="cat">Description</p>
        <p class="cat">Price</p>
        <p class="cat">Id</p>
        <p class="cat">Categories</p>
        <p class="cat">Actions</p>
      </div>
      <article
        v-for="product in getProducts.data['hydra:member']"
        :key="product.id"
        class="colonne"
      >
        <p class="col">{{ product.name }}</p>
        <p class="col">{{ product.description }}</p>
        <p class="col">{{ product.price }}</p>
        <p class="col">{{ product.id }}</p>
        <p class="col">{{ product.categories }}</p>
        <button class="col" @click="editItem(product.id)">Edit</button>
        <button class="col" @click="deleteItem(product.id)">Delete</button>
      </article>
    </div>
  </section>
</template>

<script>
import { useProducts } from "../stores/counter.js";
import { mapActions, mapState } from "pinia";

export default {
  data() {
    return {
      products: [],
    };
  },
  async mounted() {
    this.products = await this.fetchProduct;
  },
  computed: {
    ...mapActions(useProducts, ["fetchProduct"]),
    ...mapState(useProducts, ["getProducts"]),
  },
  methods: {
    deleteItem(id) {
      const requestOptions = {
        method: "DELETE",
        headers: {
          Authorization:
            "Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJpYXQiOjE3MDAxNDE0NjMsImV4cCI6MTcwMDE0NTA2Mywicm9sZXMiOlsiUk9MRV9BRE1JTiIsIlJPTEVfVVNFUiJdLCJ1c2VybmFtZSI6Im1hcnRpbi5waW5hdWRAZXBpdGVjaC5kaWdpdGFsIn0.R8X-EFLsdPnRF-jDDHdIt71X8fnUG0TGtFqhrQuLx-0w-slP0m9Cvr_fKSVUJg5c06kJzoECCLMTzTRSd80PAj-_DBJmbLhIT6NEgQLNEhCqnwVoo5n-JK8iaoO1yk9JPhwnSGrMK7GEtnfmXX_hUTqw1BoCpcVSnsf0OMcXaajBNlBw8nJkwq3D96MBhJzk9hv5sWe0h4vHgqWfJpVTH51cv8GptYMw6p9Zorj0Sa8kN5SaSo0Xq8Ew2XoQ_3fkxlHzdFTP2CdrEOsZX_aUMCVuwgOEs-68eBzYmxZ-aTOe9kZ8FGht4-3iq2NvhtluFABx5rnv5KAH3u-IphNu0g",
        },
      };
      fetch("http://localhost/api/products/" + id, requestOptions).then(
        () => this.products
      );
    },
  },
};
</script>

<style scoped>
.admin {
  height: 35vw;
}
.titles {
  display: flex;
  justify-content: center;
  gap: 20px;
}
.product-grid {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.product-grid-name {
  display: flex;
  gap: 150px;
}

.colonne {
  display: flex;
  justify-content: space-between;
  border-top: 1px solid #ccc;
  padding-top: 20px;
}
</style>
